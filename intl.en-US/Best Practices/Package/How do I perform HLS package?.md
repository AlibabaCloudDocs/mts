# How do I perform HLS package?

## Description

HLS package refers to the process in which multi-subtitle, multi-track and multi-bitstream are integrated into a Master Playlist file. The process includes creating HLS package workflow and calling AddMedia interface to specify video and the ID of the HLS package workflow for video processing.

1.  When you use [AddMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/AddMediaWorkflow.md) interface to add workflow, pay attention to the following objects:
    -   Topology

        The business process that can be defined by users using directed acyclic graphs \(DAGs\).

    -   Activity

        Activity refers to the processing nodes which constitute the topology. While creating HLS package workflow, pay attention to the following activities:

        -   [PackageConfig](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md)

            Specify HLS package configuration, and configure the output location for the Master Playlist file

            .

            -   The front node allows: Start.

            -   The back node allows: SubtitleGroup, AudioGroup, and Transcode \(only video\).

        -   [SubtitleGroup](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md)

            Specify the subtitle group ID

            .

            -   The front node allows: PackageConfig.

            -   The back node allows: Transcode \(for subtitles only\).

        -   [AudioGroup](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md)

            Specify the audio group ID

            .

            -   The front node allows: PackageConfig.

            -   The back node allows: Transcode \(only audio\).

        -   [Transcode](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md)

            Transcode nodes are used to extract video, audio, or subtitle streams.

            .

            -   The front node allows: PackageConfig, SubtitleGroup, and AudioGroup.

            -   The back node allows: GenerateMasterPlayList.

        -   [GenerateMasterPlayList](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md)

            HLS package generation activity specifies multi-ratestream configuration, audio group and subtitle group

            .

            -   The front node allows: Transcode.

            -   The back node allows: Report.

    -   Dependencies

        The edges in the topology, which indicates the dependency between activities.

2.  To add media to MPS, call the [AddMedia](/intl.en-US/API Reference/Media APIs/AddMedia.md)operation.
    -   Specify Media workflow ID.

    -   If subtitle extraction exists, you can configure in the way that the subtitle file address overwrites the WebVTTSubtitleURL parameter in the Transcode activity, and only subtitle files of WebVTT are supported.

    -   Set the Workflow triggering mode as NotInAuto.


## Scenarios

The mxf format of the source file, also supports such formats as mp4, flv and m3u8\(ts\), extracts three audio tracks, two video streams and two groups of WebVTT subtitles from the source file, and then combine and package into a Master Playlist:

Configure HLS package output location and name of Master Playlist.

-   Set up the bucket.

-   Specify Location for the Master Playlist file.

-   Specify the name of the Master Playlist file.

-   The activity is defined as follows:

```

{
"Parameters" : {
"Output" : "{\"Bucket\": \"processedmediafile\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"{MediaId}/{RunId}/hls/master.m3u8\"}"
},
"Type" : "PackageConfig"
}
```

    -   Output indicates the output location and the name of the Master Playlist file. For more information, see [Parameters supported for the PackageConfig activity](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md).

    -   Set Type to PackageConfig.


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


Extract audio streams

-   To extract audio streams from the mxf source file, you must remove the video streams.

-   Output audio parameters:

    -   Codec: AAC

    -   SampleRate:48000 Hz

    -   Format:Stereo

-   The activity is defined as follows:

```

{
"Name" : "audio-extract-1",
"Parameters" : {
"Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"}}]",
"ExtXMedia" : "{\"URI\": \"sd/audio-en.m3u8\",\"Name\": \"audio-en\",\"Language\": \"en-US\"}"
}
```

    -   [Preset static templates](/intl.en-US/API Reference/Appendix/Preset template details.md) ID: S00000001-100020 indicates that the audio output is m3u8\(ts\), and the audio bitrate configured in the preset templates is 80kbps.

    -   AudioStreamMap: The sequence number of the audio stream. For more information, see [Output](/intl.en-US/API Reference/Appendix/Parameter details.md).

    -   Remove the video streams from the output. For more information, see [Video](/intl.en-US/API Reference/Appendix/Parameter details.md).

    -   [ExtXMedia](/intl.en-US/API Reference/Appendix/Parameter details.md) defines Media Playlist, and URI specifies the name of Media Playlist.

    -   Type is configured as Transcode, which is transcode activity.


Video extraction

-   To extract video streams from the mxf source file, you must remove the audio streams.

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

    -   Custom transcoding template ID: 1fe5393bdb7b2b883f0a0fc91e81344a, you can log on to the MPS console, and configure the video transcoding parameter in **Settings** \> **Transcoding Templates**:

        -   Codec:H. 264

        -   Resolution:384x216

        -   Profile:Main

        -   Bitrate:240 Kbps

        -   Fps:25

        -   PixelFormat:YUV420P Max GOP size:1 segment length \(4 seconds\)

        -   Output format: m-3u8

    -   Remove audio streams from the output. For more information [Audio](/intl.en-US/API Reference/Appendix/Parameter details.md).

    -   [MultiBitrateVideoStream](/intl.en-US/API Reference/Appendix/Parameter details.md) defines the multi-bitrate video streams in Master Playlist, and URI specifies the name of Media Playlist.

    -   Set Type to Transcode, which indicates transcoding activities.


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

    -   [WebVTTSubtitleURL](/intl.en-US/API Reference/Appendix/Workflow activity introduction.md) specified the subtitle address. The subtitle address is overwritten dynamically while calling [AddMedia](/intl.en-US/API Reference/Media APIs/AddMedia.md). For more information about this parameter, see OverrideParams.

    -   [ExtXMedia](/intl.en-US/API Reference/Appendix/Parameter details.md) defines Media Playlist, and URI specifies the name of Media Playlist.

    -   Type is configured as Transcode, which is transcode activity.


Output a Master Playlist file

-   Package all the output audio, video, and subtitle streams into a Master Playlist file.

-   The activity is defined as follows:

```

{
"Parameters" : {
"MasterPlayList" : "{\"MultiBitrateVideoStreams\": [{\"RefActivityName\": \"video-extract\",\"ExtXStreamInfo\": {\"BandWidth\": \"1110000\",\"Audio\": \"audios\",\"Subtitles\": \"subtitles\"}}]}"
},
"Type" : "GenerateMasterPlayList"
}
```

    -   [MasterPlayList](/intl.en-US/API Reference/Appendix/Parameter details.md) defines Master Playlist.

    -   [MultiBitrateVideoStreams](/intl.en-US/API Reference/Appendix/Parameter details.md) refers to multi-bitrate video streams group.

    -   RefActivityName specifies the activity name of video streams.

    -   [ExtXStreamInfo](/intl.en-US/API Reference/Appendix/Parameter details.md) defines the attributes of the multi-bitrate video streams, Audio specifies the audio group, and Subtitles specifies the subtitle group.

    -   Type is set as GenerateMasterPlayList, that is generating Master Playlist activity.


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

## Code example

1.  Create HLS package workflow

    [Create workflow-Java](/intl.en-US/SDK Reference/Transcoding SDKs/Java SDK/Add media workflow.md)

    [Create a workflow - Python](/intl.en-US/SDK Reference/Transcoding SDKs/Python SDK/Add media workflow.md)

    [Create workflow-PHP](/intl.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Add media workflow.md)

2.  Add media

    [Add media-Java](/intl.en-US/SDK Reference/Transcoding SDKs/Java SDK/Add media.md)

    [Add media to MPS library - Python](/intl.en-US/SDK Reference/Transcoding SDKs/Python SDK/Add media.md)

    [Add media to MPS library - PHP](/intl.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Add media.md)


