# 如何进行HLS打包

HLS打包是指将多字幕、多音轨、多码率视频流生成一个Master Playlist文件的过程。包括两个步骤：新建HLS打包工作流、调用AddMedia接口指定视频及HLS打包工作流ID进行视频的处理。

## 操作步骤

1.  在创建工作流时，请关以下对象。创建工作流API接口，请参见[新增媒体工作流](/cn.zh-CN/API参考/媒体工作流接口/新增媒体工作流.md)。
    -   Topology

        拓扑结构是指可自定义的业务处理流程，DAG。

    -   Activity

        活动是指组成拓扑结构的处理节点，在新建HLS打包工作流时要注意以下几个活动：

        -   [PackageConfig活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)

            指定HLS打包配置，设置Master Playlist文件输出位置。

            前后依赖：

            -   前置节点允许：Start。

            -   后置节点允许：SubtitleGroup、AudioGroup、Transcode（仅视频）。

        -   [SubtitleGroup活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)

            指定字幕分组ID。

            前后依赖：

            -   前置节点允许：PackageConfig。

            -   后置节点允许：Transcode（仅字幕）。

        -   [AudioGroup活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)

            指定音频分组ID。

            前后依赖：

            -   前置节点允许：PackageConfig。

            -   后置节点允许：Transcode （仅音频）。

        -   [Transcode活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)

            用于提取视频流、音频流、字幕流。

            前后依赖：

            -   前置节点允许：PackageConfig、SubtitleGroup、AudioGroup。

            -   后置节点允许：GenerateMasterPlayList。

        -   [GenerateMasterPlayList活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)

            HLS打包生成活动，指定视频多码率配置，指定音频，字幕分组。

            前后依赖：

            -   前置节点允许：Transcode。

            -   后置节点允许：Report。

    -   Dependencies

        依赖关系是拓扑结构中的边，指明活动之间的依赖。

2.  调用[新增媒体](/cn.zh-CN/API参考/媒体接口/新增媒体.md)接口，需要注意以下几点：
    -   指定媒体工作流ID。

    -   若存在字幕提取，可以设置字幕文件地址覆盖Transcode活动中的参数WebVTTSubtitleURL，只支持WebVTT的字幕文件。

    -   工作流触发模式设置为：NotInAuto。


## 场景

源文件mxf格式（也可其它格式如mp4、flv、m3u8（ts）），从源文件中提取3路音轨，提取2路视频流。提取2路WebVTT字幕，最终组合打包成一个Master Playlist：

设置HLS打包输出Master Playlist的位置及名称。

-   设置Bucket。
-   设置Location。
-   设置Master Playlist的名称。

    示例代码如下：

    ```
    {
    "Parameters" : {
    "Output" : "{\"Bucket\": \"processedmediafile\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"{MediaId}/{RunId}/hls/master.m3u8\"}"
    },
    "Type" : "PackageConfig"
    }
    ```

    -   Output设置Master Playlist的存储位置及名称，请参见[PackageConfig活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)。

    -   Type指定活动类型为PackageConfig。


音频分组。

设置音频分组ID，两个音频流同属于一个音频分组。示例代码如下：

```
{
"Parameters" : {
"GroupId" : "audios"
},
"Type" : "AudioGroup"
}
```

-   GroupId：指定音频分组ID为audios。
-   Type：类型为AudioGroup活动。

提取音轨。

-   从mxf源文件中提取音频流，需要去掉视频流。
-   输出的音频流参数：

    -   Codec：AAC
    -   SampleRate：48000 Hz
    -   Format：Stereo
    示例代码如下：

    ```
    
    {
    "Name" : "audio-extract-1",
    "Parameters" : {
    "Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"}}]",
    "ExtXMedia" : "{\"URI\": \"sd/audio-en.m3u8\",\"Name\": \"audio-en\",\"Language\": \"en-US\"}"
    }
    ```

    -   TemplateId：S00000001-100020表示音频输出为m3u8\(ts\)，预置模板内设置的音频码率为80kbps。更多详情，请参见[预置模版详情](/cn.zh-CN/API参考/附录/预置模版详情.md)。
    -   AudioStreamMap：音频流选择字。更多详情，请参见[Output详情](/cn.zh-CN/API参考/附录/参数详情.md)。
    -   Remove：在输出中移除掉视频流。更多详情，请参见[Video详情](/cn.zh-CN/API参考/附录/参数详情.md)。
    -   ExtXMedia：定义Media Playlist，URI指定Media Playlist的名称。更多详情，请参见[ExtXMedia详情](/cn.zh-CN/API参考/附录/参数详情.md)。
    -   Type设置为Transcode，即转码活动。

提取视频。

从mxf源文件中提取视频流，需要去掉音频流。示例代码如下：

```

{
"Name" : "video-extract",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"1fe5393bdb7b2b883f0a0fc91e81****\",\"Audio\":{\"Remove\":\"true\"}}]",
"MultiBitrateVideoStream" : "{\"URI\": \"sd/video1.m3u8\"}"
},
"Type" : "Transcode"
}
```

-   自定义转码模板ID：1fe5393bdb7b2b883f0a0fc91e81\*\*\*\*，登录[媒体处理控制台](https://mps.console.aliyun.com/overview)，在左侧导航栏选择**全局设置** \> **转码模版**中创建自定义模板，设置视频转码参数：
    -   Codec：H.264
    -   Resolution：384x216
    -   Profile：Main
    -   Bitrate：240 Kbps
    -   Fps：25
    -   PixelFormat：YUV420P Max GOP size：1 segment length （4 seconds）
    -   输出格式：m3u8
-   在输出中移除掉音频流，请参见[Audio详情](/cn.zh-CN/API参考/附录/参数详情.md)。
-   [MultiBitrateVideoStream详情](/cn.zh-CN/API参考/附录/参数详情.md)定义Master Playlist中的多码率视频流，URI指定Media Playlist的名称。
-   Type设置为Transcode，即转码活动。

字幕分组。

设置字幕分组ID，两个字幕流同属于一个字幕分组。示例代码如下：

```

{
"Parameters" : {
"GroupId" : "subtitles"
},
"Type" : "SubtitleGroup"
}
```

-   GroupId：指定音频分组ID为subtitles。
-   Type：类型为SubtitleGroup活动。

提取字幕。

上传WebVtt格式的字幕到OSS中。示例代码如下：

```

{
"Name" : "subtitle-extract-1",
"Parameters" : {
"WebVTTSubtitleURL" : "http://mts-video.oss-cn-hangzhou.aliyun-inc.com/ShawshankRedemption.vtt",
"ExtXMedia" : "{\"URI\": \"zh/subtitle1-cn.m3u8\",\"Name\": \"subtitle-cn\",\"Language\": \"cn\"}"
},
"Type" : "Transcode"
}
```

-   [Transcode活动](/cn.zh-CN/API参考/附录/媒体工作流活动介绍.md)中的`WebVTTSubtitleURL`参数是指定字幕地址，字幕地址在调用[AddMedia](/cn.zh-CN/API参考/媒体接口/新增媒体.md)时可以被动态覆盖，见参数OverrideParams。
-   [ExtXMedia](/cn.zh-CN/API参考/附录/参数详情.md)定义Media Playlist，URI指定Media Playlist的名称。
-   Type设置为Transcode，即转码活动。

输出Master Playlist。

通过提取音频、视频、字幕，将所有提取转换后的资源打包成一个Master Playlist。示例代码如下：

```

{
"Parameters" : {
"MasterPlayList" : "{\"MultiBitrateVideoStreams\": [{\"RefActivityName\": \"video-extract\",\"ExtXStreamInfo\": {\"BandWidth\": \"1110000\",\"Audio\": \"audios\",\"Subtitles\": \"subtitles\"}}]}"
},
"Type" : "GenerateMasterPlayList"
}
```

-   MasterPlayList：定义Master Playlist。更多详情，请参见[MasterPlayList详情](/cn.zh-CN/API参考/附录/参数详情.md)。
-   MultiBitrateVideoStreams：多码率视频流数组。更多详情，请参见[MasterPlayList详情](/cn.zh-CN/API参考/附录/参数详情.md)。
-   RefActivityName指定提取视频流的活动名称。
-   ExtXStreamInfo：定义多码率视频流的属性，Audio指定音频分组，Subtitles指定字幕分组。更多详情，请参见[ExtXStreamInfo详情](/cn.zh-CN/API参考/附录/参数详情.md)。
-   Type设置为GenerateMasterPlayList，即生成Master Playlist活动。

拓扑示意图：

![拓扑](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0549482161/p10114.png)

完整的场景示例用拓扑结构。示例代码如下：

```

{
"Activities" : {
"package-node" : {
"Name" : "package-node",
"Parameters" : {
"Output" : "{\"Bucket\": \"processedmediafile\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"{MediaId}/{RunId}/hls/master.m3u8\"}"
},
"Type" : "PackageConfig"
},
"audioGroupNode" : {
"Name" : "audioGroupNode",
"Parameters" : {
"GroupId" : "audios"
},
"Type" : "AudioGroup"
},
"subtitleGroupNode" : {
"Name" : "subtitleGroupNode",
"Parameters" : {
"GroupId" : "subtitles"
},
"Type" : "SubtitleGroup"
},
"video-extract-1" : {
"Name" : "video-extract-1",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"1fe5393bdb7b2b883f0a0fc91e81344a\",\"Audio\":{\"Remove\":\"true\"}}]",
"MultiBitrateVideoStream" : "{\"URI\": \"sd/video1.m3u8\"}"
},
"Type" : "Transcode"
},
"video-extract-2" : {
"Name" : "video-extract-1",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"1fe5393bdb7b2b883f0a0fc91e81344b\",\"Audio\":{\"Remove\":\"true\"}}]",
"MultiBitrateVideoStream" : "{\"URI\": \"sd/video2.m3u8\"}"
},
"Type" : "Transcode"
},
"audio-extract-1" : {
"Name" : "audio-extract-1",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:0\"}]",
"ExtXMedia" : "{\"URI\": \"sd/audio-en-1.m3u8\",\"Name\": \"audio-en\",\"Language\": \"en-US\"}"
},
"Type" : "Transcode"
},
"audio-extract-2" : {
"Name" : "audio-extract-2",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:1\"}]",
"ExtXMedia" : "{\"URI\": \"sd/audio-cn.m3u8\",\"Name\": \"audio-cn\",\"Language\": \"cn\"}"
},
"Type" : "Transcode"
},
"audio-extract-3" : {
"Name" : "audio-extract-3",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:2\"}]",
"ExtXMedia" : "{\"URI\": \"sd/audio-de.m3u8\",\"Name\": \"audio-de\",\"Language\": \"de\"}"
},
"Type" : "Transcode"
},
"subtitle-extract-1" : {
"Name" : "subtitle-extract-1",
"Parameters" : {
"WebVTTSubtitleURL" : "http://mts-video-daily-bucket.oss-test.aliyun-inc.com/1.vtt",
"ExtXMedia" : "{\"URI\": \"zh/subtitle1-cn.m3u8\",\"Name\": \"subtitle-cn\",\"Language\": \"cn\"}"
},
"Type" : "Transcode"
},
"subtitle-extract-2" : {
"Name" : "subtitle-extract-2",
"Parameters" : {
"WebVTTSubtitleURL" : "http://mts-video.oss-cn-hangzhou.aliyun-inc.com/ShawshankRedemption.vtt",
"ExtXMedia" : "{\"URI\": \"zh/subtitle1-en.m3u8\",\"Name\": \"subtitle-en\",\"Language\": \"en-US\"}"
},
"Type" : "Transcode"
},
"masterPlayListGenerate" : {
"Name" : "masterPlayListGenerate",
"Parameters" : {
"MasterPlayList" : "{\"MultiBitrateVideoStreams\": [{\"RefActivityName\": \"video-extract-1\",\"ExtXStreamInfo\": {\"BandWidth\": \"1110000\",\"Audio\": \"audios\",\"Subtitles\": \"subtitles\"}}, {\"RefActivityName\": \"video-extract-2\",\"ExtXStreamInfo\": {\"BandWidth\": \"5000000\",\"Audio\": \"audios\",\"Subtitles\":\"subtitles\"}}]}"
},
"Type" : "GenerateMasterPlayList"
},
"activityEnd" : {
"Name" : "activityEnd",
"Parameters" : {
"PublishType" : "Manual"
},
"Type" : "Report"
},
"activityStart" : {
"Name" : "activityStart",
"Parameters" : {
"PipelineId" : "900ededca77641ecbecd4f44cc3a2965",
"Role" : "AliyunMTSDefaultRole",
"InputFile" : "{\"Bucket\":\"videouploaded\",\"Location\":\"oss-cn-hangzhou\",\"ObjectPrefix\":\"uploaded/\"}"
},
"Type" : "Start"
}
},
"Dependencies" : {
"video-extract-1" : [ "masterPlayListGenerate" ],
"video-extract-2" : [ "masterPlayListGenerate" ],
"audio-extract-1" : [ "masterPlayListGenerate" ],
"audio-extract-2" : [ "masterPlayListGenerate" ],
"audio-extract-3" : [ "masterPlayListGenerate" ],
"subtitle-extract-1" : [ "masterPlayListGenerate" ],
"subtitle-extract-2" : [ "masterPlayListGenerate" ],
"package-node" : [ "video-extract-1", "video-extract-2","subtitleGroupNode", "audioGroupNode" ],
"audioGroupNode" : [ "audio-extract-1", "audio-extract-2","audio-extract-3"],
"subtitleGroupNode" : [ "subtitle-extract-1", "subtitle-extract-2" ],
"masterPlayListGenerate" : [ "activityEnd" ],
"activityEnd" : [ ],
"activityStart" : [ "package-node" ]
}
}
```

## 示例代码

1.  新建HLS打包工作流

    [新建工作流-Java](/cn.zh-CN/SDK参考/媒体转码SDK/Java SDK/新增媒体工作流.md)

    [新建工作流-Python](/cn.zh-CN/SDK参考/媒体转码SDK/Python SDK/添加媒体工作流.md)

    [新建工作流-PHP](/cn.zh-CN/SDK参考/媒体转码SDK/PHP SDK/新增媒体工作流.md)

2.  新增媒体

    [新增媒体-Java](/cn.zh-CN/SDK参考/媒体转码SDK/Java SDK/新增媒体.md)

    [新增媒体-Python](/cn.zh-CN/SDK参考/媒体转码SDK/Python SDK/添加媒体.md)

    [新增媒体-PHP](/cn.zh-CN/SDK参考/媒体转码SDK/PHP SDK/新增媒体.md)


