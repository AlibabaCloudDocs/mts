# DASH打包 {#concept_jdp_m1m_x2b .concept}

## 简介 {#section_oxm_bjm_x2b .section}

DASH打包是指将多字幕、多音轨、多码率视频流生成一个Master Playlist文件的过程。包括两个步骤：新建DASH打包工作流、调用AddMedia接口指定视频及DASH打包工作流ID进行视频的处理。

1.  [新建工作流](https://help.aliyun.com/document_detail/44437.html) 时，有几个需要关注的对象：
    -   Topology

        拓扑结构是指可自定义的业务处理流程，DAG。

    -   Activity

        活动是指组成拓扑结构的处理节点，在新建DASH打包工作流时要注意以下几个活动：

        -   [PackageConfig](https://help.aliyun.com/document_detail/68494.html?#h2-6-packageconfig-6)

            指定DASH打包配置，设置Master Playlist文件输出位置。

            前后依赖：

            -   前置节点允许：Start。

            -   后置节点允许：SubtitleGroup、AudioGroup、VideoGroup。

        -   [SubtitleGroup](https://help.aliyun.com/document_detail/68494.html?spm=a2c4g.11186623.6.685.9OSYL9#h2-7-subtitlegroup-7)

            指定字幕分组ID和语言。

            前后依赖：

            -   前置节点允许：PackageConfig。

            -   后置节点允许：Transcode（仅字幕）。

        -   [AudioGroup](https://help.aliyun.com/document_detail/68494.html?#h2-8-audiogroup-8)

            指定音频分组ID和语言。

            前后依赖：

            -   前置节点允许：PackageConfig。

            -   后置节点允许：Transcode （仅音频）。

        -   [VideoGroup](https://help.aliyun.com/document_detail/68494.html?#h2-8-audiogroup-8)

            指定视频分组ID。

            前后依赖：

            -   前置节点允许：PackageConfig。

            -   后置节点允许：Transcode （仅视频）。

        -   [Transcode](https://help.aliyun.com/document_detail/68494.html?#h2-2-transcode-2)

            用于提取视频流、音频流、字幕流。

            前后依赖：

            -   前置节点允许：SubtitleGroup、AudioGroup、VideoGroup。

            -   后置节点允许：GenerateMasterPlayList。

        -   [GenerateMasterPlayList](https://help.aliyun.com/document_detail/68494.html?#h2-9-generatemasterplaylist-9)

            打包生成活动。

            前后依赖：

            -   前置节点允许：Transcode。

            -   后置节点允许：Report。

    -   Dependencies

        依赖关系是拓扑结构中的边，指明活动之间的依赖。

2.  调用 [新增媒体](https://help.aliyun.com/document_detail/44458.html)，需要注意以下几点：

    -   指定媒体工作流ID。

    -   若存在字幕提取，可以设置参数OverrideParams，以覆盖字幕Transcode活动中的固定字幕文件地址参数，如`{"subtitleTransNode":{"InputConfig":{"Format":"stl","InputFile":{"URL":"http://subtitleBucket.oss-cn-hangzhou.aliyuncs.com/package/subtitle/CENG.stl"}}}}` 其中 sutitleTransNode为工作流定义中的字幕抽取结点

    -   工作流触发模式设置为：NotInAuto。


## 场景 {#section_bws_cjm_x2b .section}

源文件mxf格式（也可是其它格式如mp4、flv、m3u8\(ts\)），从源文件中提取3路音轨，提取2路视频流。提取2路WebVTT字幕，最终组合打包成一个Master Playlist：

设置DASH打包输出Master Playlist的位置及名称。

-   设置Bucket。

-   设置Location。

-   设置Master Playlist的名称。

-   活动定义如下：

    ```
    
    {
    "Parameters" : {
    "Output" : "{\"Bucket\": \"processedmediafile\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"{MediaId}/{RunId}/dash/master.mpd\"}"
    },
    "Type" : "PackageConfig"
    }
    ```

    -   Output设置Master Playlist的存储位置及名称，参见 [PackageConfig活动支持的参数](https://help.aliyun.com/document_detail/68494.html?#h2-6-packageconfig-6)。
    -   Type指定活动类型为PackageConfig。

音频分组。

-   活动定义：

    ```
    
    "audio-cn-group" : {
    "Name" : "audio-cn-group",
    "Parameters" : {
    "AdaptationSet" : "{\"Lang\":\"chinese\",\"Group\":\"AudioGroupChinese\"}"
    },
    "Type" : "AudioGroup"
    }
    ```

    -   Group：指定音频分组Id为AudioGroupChinese。
    -   Type：类型为AudioGroup活动。

提取音轨。

-   从mxf源文件中提取音频流，需要去掉视频流。

-   输出的音频流参数：

-   活动定义：

    ```
    
    "audioCNTransNode" : {
    "Name" : "audioCNTransNode",
    "Parameters" : {
    "Outputs" : "[{\"TemplateId\":\"d053297fc44f9DashTemplateId\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"}}]",
    "Representation" : "{\"Id\":\"chinese128k\",\"URI\":\"audiocn/cn-abc.mpd\"}"
    },
    "Type" : "Transcode"
    }
    ```

    -   URI：音频流提取后的输出地址。
    -   AudioStreamMap：音频流选择字，参见 [Output详情](https://help.aliyun.com/document_detail/29253.html?#h2-2-output-2) 中的说明。

    -   在输出中移除掉视频流，参见 [Video详情](https://help.aliyun.com/document_detail/29253.html?#h2-8-video-8)。

    -   Type设置为Transcode，即转码活动。


视频分组。

```

"video-group" : {
"Name" : "video-group",
"Parameters" : {
"AdaptationSet" : "{\"Group\":\"VideoGroup\"}"
},
"Type" : "VideoGroup"
}
```

提取视频。

-   从mxf源文件中提取视频流，需要去掉音频流。

-   活动定义：

    ```
    
    "videoTransSD" : {
    "Name" : "videoTransSD",
    "Parameters" : {
    "Outputs" : "[{\"TemplateId\":\"d861b90f6c0aed8f81095e5c5b857cba\",\"Audio\":{\"Remove\":\"true\"}}]",
    "Representation" : "{\"Id\":\"476pSD\",\"URI\":\"videoSD/xx.mpd\"}"
    },
    "Type" : "Transcode"
    } 
    ```

    -   自定义转码模板ID：d861b90f6c0aed8f81095e5c5b857cba，可调用接口进行创建，容器格式为mpd

    -   在输出中移除掉音频流，参见 [Audio详情](https://help.aliyun.com/document_detail/29253.html?#h2-10-audio-9)。

    -   URI: 视频流提取后的名称及存储地址。

    -   Type设置为Transcode，即转码活动。


字幕分组。

-   设置字幕分组ID

-   活动定义：

    ```
    
    "subtitle-cn-group" : {
    "Name" : "subtitle-cn-group",
    "Parameters" : {
    "AdaptationSet" : "{\"Lang\":\"Chinese\", \"Group\":\"SubtitleENGroup\"}"
    },
    "Type" : "SubtitleGroup"
    }
    ```

    -   Group：指定音频分组名称为SubtitleENGroup。
    -   Lang: 指定此字幕组的语言
    -   Type：类型为SubtitleGroup活动。

提取字幕。

-   上传STL、TTML、WebVtt格式的字幕到OSS中。

-   活动定义：

    ```
    
    "subtitleCNNode" : {
    "Name" : "subtitleCNNode",
    "Parameters" : {
    "InputConfig" : "{\"Format\":\"vtt\",\"InputFile\":{\"URL\":\"http://bucketname.oss-cn-hangzhou.aliyuncs.com/test/Audio-SiHD.chs.vtt\"}}",
    "Representation" : "{\"Id\":\"subtitle-chinese\", \"URI\":\"subtitle/cn-xx.vtt\"}"
    },
    "Type" : "Transcode"
    }
    ```

    -   InputConfig 指定字幕地址，字幕地址在调用 [AddMedia](https://help.aliyun.com/document_detail/44458.html) 时可以被动态覆盖，见参数OverrideParams。

    -   URI: 字幕流提取后的名称及输出目录。

    -   Type设置为Transcode，即转码活动。


输出Master Playlist。

-   通过提取音频、视频、字幕，将所有提取转换后的资源打包成一个Master Playlist。

-   活动定义：

    ```
    
    {
    "Parameters" : {
    },
    "Type" : "GenerateMasterPlayList"
    }
    ```

    -   Type设置为GenerateMasterPlayList，即生成Master Playlist活动。

拓扑图示意：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18607/154045690210186_zh-CN.png)

完整的场景示例用拓扑结构表示：

```

{
"Activities": {
"act-package": {
"Name": "act-package",
"Parameters": {
"Output": "{\"Bucket\": \"outputbucketname\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"dashpackage/{MediaId}/{RunId}/master.mpd\"}",
"Protocol": "dash"
},
"Type": "PackageConfig"
},
"video-group": {
"Name": "video-group",
"Parameters": {
"AdaptationSet": "{\"Group\":\"VideoGroup\"}"
},
"Type": "VideoGroup"
},
"audio-en-group": {
"Name": "audio-en-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"english\", \"Group\":\"AudioGroupEnglish\"}"
},
"Type": "AudioGroup"
},
"audio-cn-group": {
"Name": "audio-cn-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"chinese\", \"Group\":\"AudioGroupChinese\"}"
},
"Type": "AudioGroup"
},
"subtitle-en-group": {
"Name": "subtitle-en-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"english\", \"Group\":\"SubtitleENGroup\"}"
},
"Type": "SubtitleGroup"
},
"subtitle-cn-group": {
"Name": "subtitle-cn-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"chinese\", \"Group\":\"SubtitleCNGroup\"}"
},
"Type": "SubtitleGroup"
},
"videoTransLD": {
"Name": "videoTransLD",
"Parameters": {
"Outputs": "[{\"TemplateId\":\"d053297fc44f9dd6becd4a98d1c42f50\",\"Audio\":{\"Remove\":\"true\"}}]",
"Representation": "{\"Id\":\"270pLD\", \"URI\":\"videoLD/xx.mpd\"}"
},
"Type": "Transcode"
},
"videoTransSD": {
"Name": "videoTransSD",
"Parameters": {
"Outputs": "[{\"TemplateId\":\"d861b90f6c0aed8f81095e5c5b857cba\",\"Audio\":{\"Remove\":\"true\"}}]",
"Representation": "{\"Id\":\"480pSD\", \"URI\":\"videoSD/xx.mpd\"}"
},
"Type": "Transcode"
},
"videoTransHD": {
"Name": "videoTransHD",
"Parameters": {
"Outputs": "[{\"TemplateId\":\"117b3ae88efbc97df372cfd9a0e1ff4c\",\"Audio\":{\"Remove\":\"true\"}}]",
"Representation": "{\"Id\":\"720pHD\", \"URI\":\"videoHD/xx.mpd\"}"
},
"Type": "Transcode"
},
"audioCNTransNode": {
"Name": "audioCNTransNode",
"Parameters": {
"Outputs": "[{\"TemplateId\":\"d053297fc44f9dd6becd4a98d1c42f50\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"}}]",
"Representation": "{\"Id\":\"chinese128k\", \"URI\":\"audiocn/cn-abc.mpd\"}"
},
"Type": "Transcode"
},
"audioENTransNode": {
"Name": "audioENTransNode",
"Parameters": {
"Outputs": "[{\"TemplateId\":\"d053297fc44f9dd6becd4a98d1c42f50\",\"AudioStreamMap\":\"0:a:1\",\"Video\":{\"Remove\":\"true\"}}]",
"Representation": "{\"Id\":\"english128k\", \"URI\":\"audioen/en-abc.mpd\"}"
},
"Type": "Transcode"
},
"subtitleENNode": {
"Name": "subtitleENNode",
"Parameters": {
"InputConfig": "{\"Format\":\"vtt\",\"InputFile\":{\"URL\":\"http://bucketname.oss-cn-hangzhou.aliyuncs.com/dashpackage/subtitle/Subtitle.EN.vtt\"}}",
"Representation": "{\"Id\":\"subtitle-english\", \"URI\":\"subtitle/en-xx.vtt\"}"
},
"Type": "Transcode"
},
"subtitleCNNode": {
"Name": "subtitleCNNode",
"Parameters": {
"InputConfig": "{\"Format\":\"vtt\",\"InputFile\":{\"URL\":\"http://bucketname.oss-cn-hangzhou.aliyuncs.com/dashpackage/subtitle/Subtitle.CN.vtt\"}}",
"Representation": "{\"Id\":\"subtitle-chinese\", \"URI\":\"subtitle/cn-xx.vtt\"}"
},
"Type": "Transcode"
},
"act-report": {
"Name": "act-report",
"Parameters": {
"PublishType": "Auto"
},
"Type": "Report"
},
"act-start": {
"Name": "act-start",
"Parameters": {
"PipelineId": "cc7fcef2562e4abc9332d491f93399d2",
"InputFile": "{\"Bucket\":\"inputbucketname\",\"Location\":\"oss-cn-hangzhou\",\"ObjectPrefix\":\"package/dash/\"}"
},
"Type": "Start"
},
"generateMasterPlayListAct": {
"Name": "generateMasterPlayListAct",
"Parameters": {},
"Type": "GenerateMasterPlayList"
}
},
"Dependencies": {
"audio-en-group": ["audioENTransNode"],
"video-group": ["videoTransLD", "videoTransSD", "videoTransHD"],
"audio-cn-group": ["audioCNTransNode"],
"audioCNTransNode": ["generateMasterPlayListAct"],
"subtitleENNode": ["generateMasterPlayListAct"],
"act-package": ["audio-en-group", "audio-cn-group", "subtitle-cn-group", "subtitle-en-group", "video-group"],
"act-report": [],
"videoTransSD": ["generateMasterPlayListAct"],
"videoTransHD": ["generateMasterPlayListAct"],
"subtitle-en-group": ["subtitleENNode"],
"subtitle-cn-group": ["subtitleCNNode"],
"subtitleCNNode": ["generateMasterPlayListAct"],
"act-start": ["act-package"],
"videoTransLD": ["generateMasterPlayListAct"],
"generateMasterPlayListAct": ["act-report"],
"audioENTransNode": ["generateMasterPlayListAct"]
}
}
```

## 示例代码 {#section_rlg_clm_x2b .section}

1.  新建HLS打包工作流。

    [新建工作流-Java](https://help.aliyun.com/document_detail/68528.html?spm=a2c4g.11186623.2.17.154f50fehZi0uv)

    [新建工作流-Python](https://help.aliyun.com/document_detail/68533.html?spm=a2c4g.11186623.2.18.154f50fehZi0uv)

    [新建工作流-PHP](https://help.aliyun.com/document_detail/68535.html?spm=a2c4g.11186623.2.19.154f50fehZi0uv)

2.  新增媒体。

    [新增媒体-Java](https://help.aliyun.com/document_detail/68527.html?spm=a2c4g.11186623.2.20.154f50fehZi0uv)

    [新增媒体-Python](https://help.aliyun.com/document_detail/68530.html?spm=a2c4g.11186623.2.21.154f50fehZi0uv)

    [新增媒体-PHP](https://help.aliyun.com/document_detail/68534.html?spm=a2c4g.11186623.2.22.154f50fehZi0uv)


