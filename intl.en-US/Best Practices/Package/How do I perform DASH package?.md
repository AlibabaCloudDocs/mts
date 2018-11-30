# How do I perform DASH package? {#concept_jdp_m1m_x2b .concept}

## Description {#section_oxm_bjm_x2b .section}

Dynamic Adaptive Streaming Over HTTP \(DASH\) packaging allows you to package one or more video streams at different bit rates, subtitles in different languages, and audio tracks into a Master Playlist file. The process includes creating a DASH packaging workflow and calling the AddMedia operation by specifying the media and the workflow ID.

1.  To create a new workflow, call the [AddMediaWorkflow](../../../../reseller.en-US/API Reference/Media workflow APIs/AddMediaWorkflow.md#)operation.
    -   Topology

        The business process that can be defined by users using directed acyclic graphs \(DAGs\).

    -   Activity

        The type of processing nodes that constitute the topology. When you create a DASH packaging workflow, pay attention to the following activity types.

        -   [PackageConfig](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#)

            PackageConfig nodes are used to specify a location for the output Master Playlist file.

            Topological sort:

            -   PackageConfig nodes can follow the Start node.

            -   PackageConfig nodes can precede SubtitleGroup, AudioGroup, or VideoGroup nodes.

        -   [SubtitleGroup](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#)

            SubtitleGroup nodes are used to specify the ID and language of each subtitle group.

            Topological sort:

            -   SubtitleGroup nodes can follow PackageConfig nodes.

            -   SubtitleGroup nodes can precede Transcode nodes \(for subtitles only\).

        -   [AudioGroup](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#)

            AudioGroup nodes are used to specify the ID and language of each audio group.

            Topological sort:

            -   AudioGroup nodes can follow PackageConfig nodes.

            -   AudioGroup nodes can precede Transcode nodes \(for audio only\).

        -   [VideoGroup](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#)

            VideoGroup nodes are used to specify the ID of each video group.

            Topological sort:

            -   VideoGroup nodes can follow PackageConfig nodes.

            -   VideoGroup nodes can precede Transcode nodes \(for video only\).

        -   [Transcode](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#)

            Transcode nodes are used to extract video, audio, or subtitle streams.

            Topological sort:

            -   Transcode nodes can follow SubtitleGroup, AudioGroup, or VideoGroup nodes.

            -   Transcode nodes can precede GenerateMasterPlayList nodes.

        -   [GenerateMasterPlayList](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#)

            GenerateMasterPlayList nodes are used to generate a Master Playlist file.

            Topological sort:

            -   GenerateMasterPlayList nodes can follow Transcode nodes.

            -   GenerateMasterPlayList nodes can precede Report nodes.

    -   Dependencies

        The edges in the topology, which indicates the dependency between activities.

2.  To add media to MPS, call the [AddMedia](../../../../reseller.en-US/API Reference/Media APIs/AddMedia.md#) operation.

    -   You must specify the ID of the media workflow.

    -   If you need to extract subtitles, you can configure the OverrideParams parameter to override the default URL of the subtitle files in the Transcode activity. For example, `{"subtitleTransNode":{"InputConfig":{"Format":"stl","InputFile":{"URL":"http://subtitleBucket.oss-cn-hangzhou.aliyuncs.com/package/subtitle/CENG.stl"}}}}`. In this example, sutitleTransNode is the node indicating subtitle extraction.

    -   Set TriggerMode to NotInAuto.


## Scenario {#section_bws_cjm_x2b .section}

Assume that you need to extract two video streams which contain three audio streams and two WebVTT subtitle streams from an mxf source file, and package them into a Master Playlist file. The source file also supports mp4, flv and m3u8 \(ts\) formats.

Configure the output location and the name of the Master Playlist file.

-   Set the bucket.

-   Specify Location for the Master Playlist file.

-   Specify the name of the Master Playlist file.

-   The activity is defined as follows:

    ```
    
    {
    "Parameters" : {
    "Output" : "{\"Bucket\": \"processedmediafile\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"{MediaId}/{RunId}/dash/master.mpd\"}"
    },
    "Type" : "PackageConfig"
    }
    ```

    -   Output indicates the output location and the name of the Master Playlist file. For more information, see [Parameters supported for the PackageConfig activity](../../../../reseller.en-US/API Reference/Appendix/Workflow activity introduction.md#).
    -   Set Type to PackageConfig.

Group audio streams

-   The activity is defined as follows:

    ```
    
    "audio-cn-group" : {
    "Name" : "audio-cn-group",
    "Parameters" : {
    "AdaptationSet" : "{\"Lang\":\"chinese\",\"Group\":\"AudioGroupChinese\"}"
    },
    "Type" : "AudioGroup"
    }
    ```

    -   Group: Specify the audio group name as AudioGroupChinese.
    -   Type: Specify the type as AudioGroup.

Extract audio streams

-   To extract audio streams from the mxf source file, you must remove the video streams.

-   Output audio parameters:

-   The activity is defined as follows:

    ```
    
    "audioCNTransNode" : {
    "Name" : "audioCNTransNode",
    "Parameters" : {
    "Outputs" : "[{\"TemplateId\":\"S00000001-100020\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"}}]",
    "Representation" : "{\"Id\":\"chinese128k\",\"URI\":\"audiocn/cn-abc.mpd\"}"
    },
    "Type" : "Transcode"
    }
    ```

    -   URI: The location for the output audio streams.
    -   AudioStreamMap: The sequence number of the audio stream. For more information, see [Output](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#).

    -   Remove the video streams from the output. For more information, see [Video](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#).

    -   Set Type to Transcode, which indicates transcoding activities.


Group Video streams

```

"video-group" : {
"Name" : "video-group",
"Parameters" : {
"AdaptationSet" : "{\"Group\":\"VideoGroup\"}"
},
"Type" : "VideoGroup"
}
```

Extract video streams

-   To extract video streams from the mxf source file, you must remove the audio streams.

-   The activity is defined as follows:

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

    -   In this example, the ID of the user-defined transcoding template is d861b90f6c0aed8f81095e5c5b857cba. You can call the corresponding API operation to create a transcoding template, and the container format is mpd.

    -   Remove audio streams from the output. For more information, see [Audio](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#).

    -   URI: The name and location of the output video streams.

    -   Set Type to Transcode, which indicates transcoding activities.


Group subtitle streams

-   Specify the ID of the subtitle group.

-   The activity is defined as follows:

    ```
    
    "subtitle-cn-group" : {
    "Name" : "subtitle-cn-group",
    "Parameters" : {
    "AdaptationSet" : "{\"Lang\":\"Chinese\", \"Group\":\"SubtitleENGroup\"}"
    },
    "Type" : "SubtitleGroup"
    }
    ```

    -   Group: Specify the subtitle group name as SubtitleENGroup.
    -   Lang: Specify a language for the subtitle group.
    -   Type: Specify the type as SubtitleGroup.

Extract subtitle streams

-   Upload STL, TTML, and WebVTT subtitles to OSS.

-   The activity is defined as follows:

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

    -   InputConfig specifies the URL of the subtitle. The URL can be overridden by configuring the OverrideParams parameter when you call the [AddMedia](../../../../reseller.en-US/API Reference/Media APIs/AddMedia.md#) operation.

    -   URI: The location for the output subtitle streams.

    -   Set Type to Transcode, which indicates transcoding activities.


Output a Master Playlist file

-   Package all the output audio, video, and subtitle streams into a Master Playlist file.

-   The activity is defined as follows:

    ```
    
    {
    "Parameters" : {
    },
    "Type" : "GenerateMasterPlayList"
    }
    ```

    -   Set Type to GenerateMasterPlayList, which indicates generating a Master Playlist file.

The topology is as follows:

![](images/10186_en-US.png)

The sample scenario shown in topology:

```

{
"Activities": {
"act-package": {
"Name": "act-package",
"Parameters": {
"Output": "{\"Bucket\": \"outputbucketname\",\"Location\": \"oss-cn-hangzhou\",\"MasterPlayListName\": \"dashpackage/{MediaId}/{RunId}/master.mpd\"}",
"Protocol": "dash"
},
"Type" : "PackageConfig"
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
"Type" : "AudioGroup"
},
"audio-cn-group": {
"Name": "audio-cn-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"chinese\", \"Group\":\"AudioGroupChinese\"}"
},
"Type" : "AudioGroup"
},
"subtitle-en-group": {
"Name": "subtitle-en-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"english\", \"Group\":\"SubtitleENGroup\"}"
},
"Type" : "SubtitleGroup"
},
"subtitle-cn-group": {
"Name": "subtitle-cn-group",
"Parameters": {
"AdaptationSet": "{\"Lang\":\"chinese\", \"Group\":\"SubtitleCNGroup\"}"
},
"Type" : "SubtitleGroup"
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

## Sample code {#section_rlg_clm_x2b .section}

1.  Create an HLS packaging workflow

    [Create a workflow - Java](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Java SDK/Add media workflow.md#)

    [Create a workflow - Python](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Python SDK/Add media workflow.md#)

    [Create a workflow - PHP](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Add media workflow.md#)

2.  Add media to MPS library

    [Add media to MPS library - Java](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Java SDK/Add media.md#)

    [Add media to MPS library - Python](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Python SDK/Add media.md#)

    [Add media to MPS library - PHP](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Add media.md#)


