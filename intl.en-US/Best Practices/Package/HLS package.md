# HLS package {#concept_dmc_3lg_x2b .concept}

## Introduction {#section_inx_tpk_x2b .section}

HLS package refers to the process in which multi-subtitle, multi-track and multi-bitstream are integrated into a Master Playlist file. The process includes creating HLS package workflow and calling AddMedia interface to specify video and the ID of the HLS package workflow for video processing.

1.  When you use [AddMediaWorkflow](https://help.aliyun.com/document_detail/44437.html) interface to add workflow, pay attention to the following objects:
    -   Topology

        Topology refers to the business processing procedure, Directed Acyclic Graph \(DAG\).

    -   Activity

        Activity refers to the processing nodes which constitute the topology. While creating HLS package workflow, pay attention to the following activities:

        -   [PackageConfig](https://help.aliyun.com/document_detail/68494.html?#h2-6-packageconfig-6)

            Specify HLS package configuration, and configure the output location for the Master Playlist file

            .

            -   The front node allows: Start.

            -   The back node allows: SubtitleGroup, AudioGroup, and Transcode \(only video\).

        -   [SubtitleGroup](https://help.aliyun.com/document_detail/68494.html?spm=a2c4g.11186623.6.685.9OSYL9#h2-7-subtitlegroup-7)

            Specify the subtitle group ID

            .

            -   The front node allows: PackageConfig.

            -   The back node allows: Transcode \(only subtitle\).

        -   [AudioGroup](https://help.aliyun.com/document_detail/68494.html?#h2-8-audiogroup-8)

            Specify the audio group ID

            .

            -   The front node allows: PackageConfig.

            -   The back node allows: Transcode \(only audio\).

        -   [Transcode](https://help.aliyun.com/document_detail/68494.html?#h2-2-transcode-2)

            Extract video streams/audio stream/subtitle stream.

            .

            -   The front node allows: PackageConfig, SubtitleGroup, and AudioGroup.

            -   The back node allows: GenerateMasterPlayList.

        -   [GenerateMasterPlayList](https://help.aliyun.com/document_detail/68494.html?#h2-9-generatemasterplaylist-9)

            HLS package generation activity specifies multi-ratestream configuration, audio group and subtitle group

            .

            -   The front node allows: Transcode.

            -   The back node allows: Report.

    -   Dependencies

        Dependencies refer to the edges of the topology, indicating the dependency between activities.

2.  When you use the [AddMedia](https://help.aliyun.com/document_detail/44458.html) interface to add media, pay attention to the following aspects:
    -   Specify Media workflow ID.

    -   If subtitle extraction exists, you can configure in the way that the subtitle file address overwrites the WebVTTSubtitleURL parameter in the Transcode activity, and only subtitle files of WebVTT are supported.

    -   Set the Workflow triggering mode as NotInAuto.


## Scenarios {#section_m3g_tqk_x2b .section}

The mxf format of the source file, also supports such formats as mp4, flv and m3u8\(ts\), extracts three audio tracks, two video streams and two groups of WebVTT subtitles from the source file, and then combine and package into a Master Playlist:

Configure HLS package output location and name of Master Playlist.

-   Configure Bucket.

-   Configure Location.

-   Configure the name of Master Playlist.

-   The activity is defined as follows:

```

{
"Parameters" : {
"Output" : "{\"Bucket\": \"processedmediafile\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"{MediaId}/{RunId}/hls/master.m3u8\"}"
},
"Type" : "PackageConfig"
}
```

    -   Output configures the storage location and name of Master Playlist. For more information, see [Parameters supported by the PackageConfig activity](https://help.aliyun.com/document_detail/68494.html?#h2-6-packageconfig-6).

    -   Type specifies the activity type as PackageConfig.


Audio group

-   Configure the audio group ID, wherein two audio streams belongs to the same audio group.

-   The activity is defined as follows:

```

{
"Parameters" : {
"GroupId" : "audios"
},
"Type" : "AudioGroup"
}
```

    -   GroupId: Specify the audio group Id as audios.

    -   Type: Specify the type as AudioGroup activity.


Audio extraction

-   Extract audio streams from mxf source file, and the video streams must be removed.

-   Output audio parameters:

    -   Codec: AAC

    -   SampleRate：48000 Hz

    -   Format：Stereo

-   The activity is defined as follows:

```

{
"Name" : "audio-extract-1",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"}}]",
"ExtXMedia" : "{\"URI\": \"sd/audio-en.m3u8\",\"Name\": \"audio-en\",\"Language\": \"en-US\"}"
}
```

    -   [Preset static templates](https://help.aliyun.com/document_detail/29256.html?#h2-u9884u7F6Eu9759u6001u6A21u677F2) ID: S00000001-100020 indicates that the audio output is m3u8\(ts\), and the audio bitrate configured in the preset templates is 80kbps.

    -   AudioStreamMap: Audio stream sequence number. For more information, see [Output](https://help.aliyun.com/document_detail/29253.html?#h2-2-output-2).

    -   Remove the video streams from the output. For more information, see [Video](https://help.aliyun.com/document_detail/29253.html?#h2-8-video-8).

    -   [ExtXMedia](https://help.aliyun.com/document_detail/29253.html?#h2-41-extxmedia-37) defines Media Playlist, and URI specifies the name of Media Playlist.

    -   Type is configured as Transcode, which is transcode activity.


Video extraction

-   Extract video streams from the mxf source file, and the audio streams must be removed.

-   The activity is defined as follows:

```

{
"Name" : "video-extract",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"1fe5393bdb7b2b883f0a0fc91e81344a\",\"Audio\":{\"Remove\":\"true\"}}]",
"MultiBitrateVideoStream" : "{\"URI\": \"sd/video1.m3u8\"}"
},
"Type" : "Transcode"
}
```

    -   Custom transcoding template ID: 1fe5393bdb7b2b883f0a0fc91e81344a, you can log on to the [MPS console](https://mts.console.aliyun.com/), and configure the video transcoding parameter in **Settings** \> **Transcoding Templates**:

        -   Codec：H. 264

        -   Resolution：384x216

        -   Profile：Main

        -   Bitrate：240 Kbps

        -   Fps：25

        -   PixelFormat：YUV420P Max GOP size：1 segment length \(4 seconds\)

        -   Output format: m-3u8

    -   Remove audio streams from the output. For more information [Audio](https://help.aliyun.com/document_detail/29253.html?#h2-10-audio-9).

    -   [MultiBitrateVideoStream](https://help.aliyun.com/document_detail/29253.html?#h2-40-multibitratevideostream-36) defines the multi-bitrate video streams in Master Playlist, and URI specifies the name of Media Playlist.

    -   Type is configured as Transcode, which is transcode activity.


Subtitle group

-   Configure subtitle group ID, wherein two subtitle streams belong to the same subtitle group.

-   The activity is defined as follows:

    ```
    
    {
    "Parameters" : {
    "GroupId" : "subtitles"
    },
    "Type" : "SubtitleGroup"
    }
    ```

    -   GroupId: Specify the audio group Id as subtitles.

    -   Type: Specify the type as SubtitleGroup activity.


Subtitle extraction

-   Upload subtitles in the WebVtt format to OSS.

-   The activity is defined as follows:

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

    -   [WebVTTSubtitleURL](https://help.aliyun.com/document_detail/68494.html?#h2-2-transcode-2) specified the subtitle address. The subtitle address is overwritten dynamically while calling [AddMedia](https://help.aliyun.com/document_detail/44458.html) For more information about this parameter, see OverrideParams.

    -   [ExtXMedia](https://help.aliyun.com/document_detail/29253.html?#h2-41-extxmedia-37) defines Media Playlist, and URI specifies the name of Media Playlist.

    -   Type is configured as Transcode, which is transcode activity.


Master Playlist output

-   By means of audio, video and subtitle extraction, all the resources after extraction conversion are packaged into a Master Playlist.

-   The activity is defined as follows:

```

{
"Parameters" : {
"MasterPlayList" : "{\"MultiBitrateVideoStreams\": [{\"RefActivityName\": \"video-extract\",\"ExtXStreamInfo\": {\"BandWidth\": \"1110000\",\"Audio\": \"audios\",\"Subtitles\": \"subtitles\"}}]}"
},
"Type" : "GenerateMasterPlayList"
}
```

    -   [MasterPlayList](https://help.aliyun.com/document_detail/29253.html?#h2-42-masterplaylist-38) defines Master Playlist.

    -   [MultiBitrateVideoStreams](https://help.aliyun.com/document_detail/29253.html?#h2-43-multibitratevideostream-39) refers to multi-bitrate video streams group.

    -   RefActivityName specifies the activity name of video streams.

    -   [ExtXStreamInfo](https://help.aliyun.com/document_detail/29253.html?#h2-44-extxstreaminfo-40) defines the attributes of the multi-bitrate video streams, Audio specifies the audio group, and Subtitles specifies the subtitle group.

    -   Type is set as GenerateMasterPlayList, that is generating Master Playlist activity.


Topology:

![](images/10114_en-US.png)

Complete scenario example shown in topology:

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

## Code example {#section_q2q_4sk_x2b .section}

1.  Create HLS package workflow

    [Create workflow-Java](https://help.aliyun.com/document_detail/68528.html?spm=a2c4g.11186623.2.25.762b15ffPkSMUP)

    [Create workflow-Python](https://help.aliyun.com/document_detail/68533.html?spm=a2c4g.11186623.2.26.762b15ffPkSMUP)

    [Create workflow-PHP](https://help.aliyun.com/document_detail/68535.html?spm=a2c4g.11186623.2.27.762b15ffPkSMUP)

2.  Add media

    [Add media-Java](https://help.aliyun.com/document_detail/68527.html?spm=a2c4g.11186623.2.28.762b15ffPkSMUP)

    [Add media-Python](https://help.aliyun.com/document_detail/68530.html?spm=a2c4g.11186623.2.29.762b15ffPkSMUP)

    [Add media-PHP](https://help.aliyun.com/document_detail/68534.html?spm=a2c4g.11186623.2.30.762b15ffPkSMUP)


