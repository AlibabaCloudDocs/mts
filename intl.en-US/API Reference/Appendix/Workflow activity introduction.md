# Workflow activity introduction {#reference_i5h_gqn_y2b .reference}

Workflow activity types are listed as follows: Start, Transcode, Snapshot, Analysis, Cover, Summary, Censor, Report, UploadVerify, GenerateMasterPlayList, AudioGroup, SubtitleGroup and PackageConfig. This document introduces the parameters supported by the following activity types:

## Start activity {#section_hbf_3qn_y2b .section}

You can set the trigger conditions and overall configurations of the Media workflow. This activity acquires media information. If the acquisition fails, directly jump to perform Report activity.

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|InputFile|String|Yes|Input position. For more information, see [Matching rule for workflow file](reseller.en-US/API Reference/Appendix/Matching rule for workflow file triggering.md#).Example: \{“Bucket”: “example-001”,”Location”: “oss-cn-hangzhou”, “ObjectPrefix”: “test/“\}.

|
|PipelineId|String|Yes|ID of the MPS queue, which is global.In the workflow scenario, the message configuration for the MPS queue is invalid, but the message configuration of the QueueName/TopicName is valid.

|
|MessageType|String|No|Message Type.-   Range: Queue and Topic.
-   Default value: Queue.

|
|QueueName|String|No|Name of the Message Service queue, which is global.|
|TopicName|String|No|Topic name, which is global.|
|RoleName|String|No|Authorization role name, which is global.Default value: AliyunMTSDefaultRole

|

## Transcode activity {#section_jt3_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Outputs|String|No|Optional while extracting subtitles.-   For more information, see [Output](https://help.aliyun.com/document_detail/29253.html?#h2-2-output-2).
-   Example: \[\{“OutputObject”:”transcode%2F%7BObjectPrefix%7D%2F%7BFileName%7D. %7BExtName%7D”,”TemplateId”: “S00000001-000070”\}\]。

|
|OutputBucket|String|No|Output bucket.Output bucket. During HLS package, it is overwritten by the Bucket in PackageConfig.

|
|OutputLocation|String|No|Output region.During HLS package, it is overwritten by the Location in PackageConfig.

|
|MultiBitrateVideoStream|String|No|During HLS package, this parameter is required while extracting video streams.-   For more information about this parameter, see [MultiBitrateVideoStream](https://help.aliyun.com/document_detail/29253.html).
-   Example: \{“URI”: “c/d/video1.m3u8”\}.

|
|ExtXMedia|String|No|During HLS package, this parameter is requried while extracting audio streams or subtitle streams.-   For more information about this parameter, see [ExtXMedia](https://help.aliyun.com/document_detail/29253.html?#h2-41-extxmedia-37).
-   Example: \{“Name”: “english”,”Language”: “en-US”,”URI”:”c/d/audio-1.m3u8”\}.

|
|WebVTTSubtitleURL|String|No|HLS package exclusive parameter, subtitle address,-   which currently only supports WebVTT subtitle file, must comply with URL standard, and can overwrite subtitle address while calling AddMedia.
-   Example: [http://test.oss-cn-hangzhou.aliyuncs.com/subtitles-en.vtt.](http://test.oss-cn-hangzhou.aliyuncs.com/subtitles-en.vtt%E3%80%82)

|
|Representation|String|No|During DASH package, it is required to be set when extract audio stream, video stream, or subtitle stream.-   For more information, see [Representation](https://help.aliyun.com/document_detail/29253.html?spm=a2c4g.11186623.2.9.VYtiOD#h2-48-representation-44).
-   Example: \{\\”Id\\”:\\”480p\\”, \\”URI\\”:\\”videoSD/xx.mpd\\”\}.

|
|InputConfig|String|No|Dash package exclusive parameter, and is required to be set when extract sutitle streams.-   For more information, see [InputConfig](https://help.aliyun.com/document_detail/29253.html?spm=a2c4g.11186623.2.9.VYtiOD#h2-49-inputconfig-45).
-   Example: ”\{\\”Format\\”:\\”vtt\\”,\\”InputFile\\”:\{\\”URL\\”:\\”[http://subtitlebucket.oss-cn-hangzhou.aliyuncs.com/subtitle/subtitle-en.vtt\\"\}\}](http://subtitlebucket.oss-cn-hangzhou.aliyuncs.com/subtitle/subtitle-en.vtt/%22%7D%7D)"

|

## Screenshot activity {#section_i5k_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|SnapshotConfig|String|Yes| -   For more information, see [SnapshotConfig](https://help.aliyun.com/document_detail/29253.html?#h2-11-snapshotconfig-10).
-   Example: \{“OutputFile”: \{“Bucket”: “example-001”, “Location”: “oss-cn-hangzhou”, “Object”:”snapshot%2F%7BObjectPrefix%7D%2F%7BFileName%7D. %7BExtName%7D%2F1.jpg”\},”Time”: “5”\}。

 |
|MediaCover|String|No|Whether the screenshot is set as the media cover,-   only for a single screenshot.
-   Range: true, false.
-   Default value: false.

|

## Analysis activity {#section_y5m_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|KeepOnlyHighestDefinition|String|No|Whether to keep only the highest definition analysis results.-   Range: True, False.
-   Default value: False.

|

## Report activity {#section_zs4_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|PublishType|String|No|Media publication type.Range: Auto, Manual, and TranscodeCompletedAuto.

-   Auto: the media set is automatically published after the workflow is executed.
-   Manual: the media set is not published.
-   TranscodeCompletedAuto: the media set is automatically published after any Transcode activity is completed \(use the message configuration of the Start node to notify users of transcoding completion and use the Play Service to play the activity output\).

Default value: Manual.

**Note:** When the type is TranscodeCompletedAuto, the message will not be sent if the status of the transcoding activity is Skipping.

|

## PackageConfig activity {#section_r4r_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Output|String|Yes|JSON string.Example: \{“Bucket”:”output”,”Location”:”oss-cn-hangzhou”,”MasterPlayListName”:”a/b/c.m3u8”\}.

**Note:** Placeholders that can be used in MasterPlayListName:

-   \{ObjectPrefix\}: the original file path not including Bucket information,
-   \{FileName\}: the original file name not including extension,
-   \{ExtName\}: extension of the original file,
-   \{RunId\}: the ID of the workflow execution,
-   \{MediaId\}: the MediaID processed by the workflow.

All these placeholders can be dynamically replaced.

|
|Protocol|String|Yes|Value: hls, dash|

## SubtitleGroup activity {#section_j2v_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|GroupId|String|No|Group ID.-   HLS package exclusive parameters, required.
-   The length cannot exceed 32 characters.

|
|AdaptationSet|String|No| -   DASH packages exclusive parameters, required. For more information, see [AdaptationSet](https://help.aliyun.com/document_detail/29253.html?#h2-47-adaptationset-43)
-   Example: ”\{\\”Lang\\”:\\”english\\”, \\”Group\\”:\\”SubtitleENGroup\\”\}”

 |

## AudioGroup activity {#section_mnw_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|GroupId|String|No|Group ID.-   Hls package exclusive parameters, required.
-   The length cannot exceed 32 characters;

|
|AdaptationSet|String|No| -   DASH package exclusive parameters, required. For more information, see [AdaptationSet](https://help.aliyun.com/document_detail/29253.html?#h2-47-adaptationset-43).
-   Example: ”\{\\”Lang\\”:\\”english\\”, \\”Group\\”:\\”AudioGroupEnglish\\”\}”, one language one subtitle group.

 |

## VideoGroup activity {#section_brx_lqn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|AdaptationSet|String|No| -   DASH package exclusive parameters, required. For more information, see [AdaptationSet](https://help.aliyun.com/document_detail/29253.html?#h2-47-adaptationset-43).
-   Example: ”AdaptationSet”: “\{\\”Group\\”:\\”VideoGroup\\”\}”

 |

## GenerateMasterPlayList activity {#section_eys_xvn_y2b .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|MasterPlayList|String|No| -   HLS exclusive parameters, required. Multi-bitstream list. For more information, see [MasterPlayList](https://help.aliyun.com/document_detail/29253.html?#h2-42-masterplaylist-38).
-   Example: \{“MultiBitrateVideoStreams”: \[\{“RefActivityName”: “video-1”,”ExtXStreamInf”: \{“BandWidth”: “111110”,”Audio”: “auds”,”Subtitles”: “subs” \}\}\]\}.

 |

