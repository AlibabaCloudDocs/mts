# Data types {#reference_add_crh_y2b .reference}

You can view the following data types.

## AliyunProperties {#section_xhb_rsh_y2b .section}

Attribute type

|Name|Type|Description|
|:---|:---|:----------|
|Format|AliyunFormatInfo|Format information.|
|Streams|AliyunStreamsInfo|Streaming information.|

## AliyunFormatInfo {#section_fdv_tsh_y2b .section}

Format information type

|Name|Type|Description|
|:---|:---|:----------|
|NumStreams|String|Total number of media streams|
|NumPrograms|String|Total number of program streams|
|FormatName|String|Brief name of the container/encapsulation format|
|FormatLongName|String|Long name of the container/encapsulation format|
|StartTime|String|Start time|
|Duration|String|Total time|
|Size|String|File size|
|Bitrate|String|Total bit rate|

## AliyunStreamsInfo {#section_twx_tsh_y2b .section}

Stream information type

|Name|Type|Description|
|:---|:---|:----------|
|VideoStreamList|AliyunVideoStream\[\]|Video stream list|
|AudioStreamList|AliyunAudioStream\[\]|Audio stream list|
|SubtitleStreamList|AliyunSubtitleStream\[\]|Subtitle stream list|

## AliyunVideoStream {#section_abz_tsh_y2b .section}

Video stream information type

|Name|Type|Description|
|:---|:---|:----------|
|Index|String|Video stream number, used to identify the position of the video stream in the whole media streams|
|CodecName|String|Brief name of the encoding format|
|CodecLongName|String|Long name of the encoding format|
|Profile|String|Encoding preset|
|CodecTimeBase|String|Encoding time baseEncoding time base.|
|CodecTagString|String|Mark text of the encoding format|
|CodecTag|String|Encoding format mark|
|Width|String|Video resolution width, numbers.|
|Height|String|Video resolution height|
|HasBFrames|String|Whether the video has B frames|
|Sar|String|Encoding signal resolution ratio.|
|Dar|String|Encoding display resolution ratio|
|PixFmt|String|Pixel format|
|Level|String|Encoding level|
|Fps|String|Frame rate, number.|
|AvgFPS|String|Average frame rate|
|Timebase|String|Time base|
|StartTime|String|Start time|
|Duration|String|Time length|
|Bitrate|String|Bit rate|
|NumFrames|String|Total number of frames|
|Lang|String|Language.For more information, see [FFmpeg language definition](https://www.ffmpeg.org/ffmpeg-all.html#Metadata) and [ISO-639](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).

|
|Rotate|String|Video rotation angle|

## AliyunAudioStream {#section_etz_tsh_y2b .section}

Audio stream information type

|Name|Type|Description|
|:---|:---|:----------|
|Index|String|Audio stream number, used to identify the position of the audio stream in the whole media streams|
|CodecName|String|Brief name of the encoding format|
|CodecLongName|String|Long name of the encoding format|
|CodecTimeBase|String|Encoding time base|
|CodecTagString|String|Mark text of the encoding format|
|CodecTag|String|Encoding format mark|
|SampleFmt|String|Sample format|
|Samplerate|String|Sampling rate|
|Channels|String|Number of audio channels|
|ChannelLayout|String|Audio channel output layout|
|Timebase|String|Time base|
|StartTime|String|Start time|
|Duration|String|Time length|
|Bitrate|String|Bit rate|
|NumFrames|String|Total number of frames|
|Lang|String|Language.For more information, see [FFmpeg language definition](https://www.ffmpeg.org/ffmpeg-all.html#Metadata) and [ISO-639](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).

|

## AliyunSubtitleStream {#section_wl1_5sh_y2b .section}

Subtitle stream information type

|Name|Type|Description|
|:---|:---|:----------|
|Index|String|Subtitle stream number, used to identify the position of the subtitle stream in the whole media streams|
|Lang|String|Language.For more information, see [FFmpeg language definition](https://www.ffmpeg.org/ffmpeg-all.html#Metadata) and [ISO-639](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).

|

## AliyunTemplate {#section_icb_5sh_y2b .section}

Transcoding template type

|Name|Type|Description|
|:---|:---|:----------|
|Id|String|Transcoding template ID|
|Name|String|Template name|
|Container|AliyunContainer|Container|
|Audio|AliyunAudioCodec|Audio codec configurations|
|Video|AliyunVideoCodec|Video codec configurations|
|TransConfig|AliyunTransConfig|General transcoding configurations|
|MuxConfig|AliyunMuxConfig|Transcoding encapsulation configurations|
|State|String|Template status, which has the following options: Normal and Deleted.|

## AliyunContainer {#section_vzp_pth_y2b .section}

Container type

|Name|Type|Description|
|:---|:---|:----------|
|Format|String|Container format.Supported formats are FLV, MP4, TS, M3U8, GIF, MP3, OGG, and FLAC.

|

## AliyunAudioCodec {#section_pxv_qth_y2b .section}

Audio codec configuration type

|Name|Type|Description|
|:---|:---|:----------|
|Codec|String|Audio codec format.-   Supported formats are AAC, MP3, Vorbis, and FLAC.
-   Default value: aac

|
|Profile|String|Audio encoding preset.If Codec is set to aac, Profile has the following options: aac\_low, aac\_he, aac\_he\_v2, aac\_ld, and aac\_eld

|
|Samplerate|String|Sampling rate,-   which has the following options: 22050, 32000, 44100, 48000, and 96000.
-   Unit: Hz.
-   Default Value: 44100.

|
|Bitrate|String|Audio bit rate of the output file.-   Value range: \[8，1000\]
-   Unit: Kbps
-   Default Value: 128

|
|Channels|String|Number of audio channels,-   which has the following options: 1, 2. 3, 4, 5, 6, 7, and 8.
-   Default Value: 2

|

## AliyunVideoCodec {#section_tnw_qth_y2b .section}

Video codec configuration type

|Name|Type|Description|
|:---|:---|:----------|
|Codec|String|Codec format,-   which has the following options: H.264, and H. 265.
-   Default Value: H. 264

|
|Profile|String|Encoding level,which has the following options: baseline, main, and high.

-   baseline: applicable to mobile devices.
-   main: applicable to SD devices.
-   high: applicable to HD devices.
-   Default Value: high

|
|Bitrate|String|Average video bit rate.-   Default Value: \[10，50000\]
-   Unit: Kbps

|
|Crf|String|Bit rate, which is a quality control factor.-   Value range: \[0，51\]
-   Default Value: 26
-   If CRF is set, the setting of Bitrate becomes invalid.

|
|Width|String|Width.-   Value range: \[128,4026\]
-   Unit: Px
-   Default value: Original video width.

|
|Height|String|Height.-   Value range: \[128,4026\]
-   Unit: Px
-   Default value: Original video height

|
|Fps|String|Frame rate.-   Value range: \(0, 60\]
-   If the frame rate of the input file is greater than 60, 60 is used.
-   Default value: frame rate of the input file.

|
|Gop|String|Maximum number of frames between two key frames.-   Value range: \[1, 1080000\]
-   Default value: 250

|
|Preset|String|Video algorithm preset,-   which has the following options: veryfast, fast, medium, slow, and slower.
-   Default value: medium

|
|ScanMode|String|Scan mode,which has the following options: interlaced and progressive.

|
|Bufsize|String|Size of the buffer area.-   Value range: \[1000,128000\]
-   Unit: Kb
-   Default value: 6000

 |
|Maxrate|String|Peak video bit rate.-   Default value: \[10，50000\]
-   Unit: Kbps

|
|BitrateBnd|AliyunBitrateBnd|Range of the average video bit rate.|
|PixFmt|String|Video color format.The value options are standard color formats, such as yuv420p and yuvj420p.

|

## AliyunTransConfig {#section_ddx_qth_y2b .section}

General transcoding configuration type

|Name|Type|Description|
|:---|:---|:----------|
|TransMode|String|Transcoding mode,-   which has the following options: onepass, twopass, and CBR.
-   Default value: onepass

|

## AliyunBitrateBnd {#section_npx_qth_y2b .section}

Range of the average bit rate

|Name|Type|Description|
|:---|:---|:----------|
|Max|String|Maximum total bit rate.-   Value range: \[10，50000\]
-   Unit: Kbps

|
|Min|String|Minimum total bit rate.-   Value range: \[10, 50000\]
-   Unit: Kbps

|

## AliyunOSSFile {#section_wtr_rwh_y2b .section}

OSS file type

|Name|Type|Description|
|:---|:---|:----------|
|Bucket|String|OSS bucket,which can contain 3 to 63 bytes.

|
|Location|String|OSS service region,up to 64 bytes.

|
|Object|String|OSS object,up to 1024 bytes.

|

## Aliyunjob {#section_fh4_5wh_y2b .section}

Task

|Name|Type|Description|
|:---|:---|:----------|
|JobId|String|Task ID|
|Input|AliyunJobInput|Task input.|
|Output|AliyunOutput|Task output.|
|State|String|Task status,-   Submitted indicates that the task is submitted,
-   Transcoding indicates that the task is being transcoded,
-   Transcodesuccess said transcoding success,
-   TranscodeFail indicates that the transcoding fails,
-   and TranscodeCancelled indicates that transcoding is canceled.

|
|Code|String|Error code of transcoding failure.|
|Message|String|Message of transcoding failure.|
|Percent|String|Transcoding progress.Value range: \[0, 100\].

|
|UserData|String|Custom data.|
|PipelineId|String|MPS queue ID.|
|CreationTime|String|Time of adding the task.|
|MNSMessageResult|AliyunMNSMessageResult|Message result sent by Message Service to notify the user of task completion.|

## AliyunJobInput {#section_rcg_vwh_y2b .section}

Transcoding task input type

|Name|Type|Description|
|:---|:---|:----------|
|Bucket|String|OSS bucket of the input task,which can contain 3 to 63 bytes.

|
|Location|String|OSS service region,up to 64 bytes.

|
|Object|String|OSS object of the of the input task,up to 1024 bytes.

|
|Audio|AliyunInputAudio|Configurations of the audio in the source transcoding media.|
|Container|AliyunInputContainer|Configurations of the transcoding source media container.|

## AliyunInputContainer {#section_v1z_wwh_y2b .section}

Source media container configuration type.

**Note:** If the input file is in ADPCM or PCM format, this parameter is required.

|Name|Type|Description|
|:---|:---|:----------|
|Format|String|Source media audio format,-   which has the following options: alaw, f32be, f32le, f64be, f64le, mulaw, s16be, s16le,s24be, s24le, s32be, s32le, s8, u16be, u16le, u24be, u24le, u32be, u32le, and u8.

|

## AliyunInputAudio {#section_iwz_wwh_y2b .section}

Source media audio configuration type.

**Note:** If the input file is in ADPCM or PCM format, this parameter is required.

|Name|Type|Description|
|:---|:---|:----------|
|Channels|String|Number of source media audio channels.Value range: \[1,8\]

|
|Samplerate|String|Source media audio sampling rate.-   Value range: \[0，320000\].
-   Unit: Hz.

|

## AliyunOutput {#section_rl1_xwh_y2b .section}

Task output type

|Name|Type|Description|
|:---|:---|:----------|
|OutputFile|AliyunOSSFile|Output file.|
|TemplateId|String|Template ID.|
|WaterMarkList|AliyunWaterMark\[ \]|Watermark list.|
|Clip|AliyunClip|Video clip|
|Rotate|String|Video rotation angle.Value range: \[0,360\)

|
|Properties|AliyunProperties|Media properties.|
|Priority|String|Task priority in the MPS queue.-   Value range: \[1, 10\]
-   Highest priority: 10
-   Default value: 6

|
|Container|AliyunContainer|Container.If this parameter is set, the parameter setting replaces the AliyunContainer setting of the template specified by the TemplateId.

|
|Video|AliyunVideoCodec|Video configuration.If this parameter is set, the parameter setting replaces the AliyunVideoCodec setting of the template specified by the TemplateId.

|
|Audio|AliyunAudioCodec|Audio configuration.If this parameter is set, the parameter setting replaces the AliyunAudioCodec setting of the template specified by the TemplateId.

|
|TransConfig|AliyunTransConfig|General transcoding configuration.If this parameter is set, the parameter setting replaces the AliyunTransConfig setting of the template specified by the TemplateId.

|
|MuxConfig|AliyunMuxConfig|Transcoding encapsulation configurations.If this parameter is set, the parameter setting replaces the AliyunMuxConfig setting of the template specified by the TemplateId.

|
|UserData|String|Custom data.|

## AliyunClip {#section_wcb_xwh_y2b .section}

Editing type

|Name|Type|Description|
|:---|:---|:----------|
|TimeSpan|AliyunTimeSpan|Edited time period.|

## AliyunTimeSpan {#section_crb_xwh_y2b .section}

Edited time period type

|Name|Type|Description|
|:---|:---|:----------|
|Seek|String|Start time.|
|Duration|String|Duration.|
|End|String|Truncation time at the end.-   For example, 5.23 indicates that the 5.23 seconds at the end will be cut.
-   If this parameter is set, the Duration parameter becomes invalid.

|

## AliyunMuxConfig {#section_clc_xwh_y2b .section}

Encapsulation configuration type

|Name|Type|Description|
|:---|:---|:----------|
|Segment|AliyunSegment|Slice configurations.|

## AliyunSegment {#section_sdd_xwh_y2b .section}

Slice configuration type

|Name|Type|Description|
|:---|:---|:----------|
|Duration|String|Slice length.-   Value range: \[1,60\]
-   Unit: seconds

|

## AliyunJobResult {#section_qxd_xwh_y2b .section}

Task result submission type

|Name|Type|Description|
|:---|:---|:----------|
|Success|String|Whether the task is successfully submitted.The following options are available: true or false.

|
|Code|String|Error code displayed when the task fails to be created.|
|Message|String|Error message displayed when the task fails to be created.|
|Job|AliyunJob|Task.If the task fails to be submitted, the task ID is not generated.

|

## AliyunWaterMark {#section_hp2_xwh_y2b .section}

Task output type

|Name|Type|Description|
|:---|:---|:----------|
|InputFile|AliyunOSSFile|Watermark input file.|
|WaterMarkTemplateId|String|Watermark template ID.|

## AliyunWaterMarkTemplate {#section_zff_xwh_y2b .section}

Watermark template type

|Name|Type|Description|
|:---|:---|:----------|
|Id|String|Watermark template ID.|
|Name|String|Watermark template name.|
|Width|Number|Width.-   Value range: \[8,4096\]
-   Unit: Px

|
|Height|Number|Height.-   Value range: \[8,4096\]
-   Unit: Px

|
|DX|Number|Horizontal offset.-   Value range: \[-4096,4096\]
-   Unit: Px

|
|Dy|Number|Vertical offset.-   Value range: \[-4096,4096\]
-   Unit: Px

|
|ReferPos|String|Watermark position,-   which has the following options: TopRight, TopLeft, BottomRight, and BottomLeft.

|
|Type|String|Watermark type,which has the following options: Image and Text.

**Note:** Currently, only the Image type is supported.

|
|State|String|Watermark template status,which has the following options: Normal and Deleted.

|

## AliyunPipeline {#section_ovf_xwh_y2b .section}

MPS queue type

|Name|Type|Description|
|:---|:---|:----------|
|Id|String|MPS queue ID.|
|Name|String|MPS queue name.|
|Speed|String|MPS queue type,-   which has the following options: Boost, Standard, NarrowBandHDV2, AIVideoCover, AIVideoRecogni, AIVideoSummary, AIVideoPorn, AIAudioKWS, and AIAudioASR.
-   Default value: Standard

|
|State|String|MPS queue status,which has the following options: Active and Paused.

-   Active: Tasks in the MPS queue will be scheduled, transcoded, and run by Media Transcoding.
-   Paused: The MPS queue is paused, and tasks in the MPS queue will not be scheduled, transcoded, and run by Media Transcoding. The status of all tasks in the MPS queue is Submitted. Ongoing transcoding tasks are not paused.

|
|NotifyConfig|String|Message Service notification configurations.|

## AliyunMediaInfoJob {#section_vjg_xwh_y2b .section}

Media information analysis task type

|Name|Type|Description|
|:---|:---|:----------|
|Id|String|Metadata analysis task ID.|
|Input|AliyunOSSFile|Task input.|
|State|String|Job status,which has the following options: Analyzing, Success, and Fail.

|
|Code|String|Error code displayed when the metadata analysis fails.|
|Message|String|Error message displayed when the metadata analysis fails.|
|Properties|AliyunProperties|Properties.|
|UserData|String|Custom data.|
|CreationTime|String|Time of adding the task.|

## AliyunAnalysisJob {#section_hwg_xwh_y2b .section}

Template analysis task type

|Name|Type|Description|
|:---|:---|:----------|
|Id|String|Template analysis task ID.|
|Input|AliyunOSSFile|Task input.|
|AnalysisConfig|AliyunAnalysisConfig|Task configurations.|
|TemplateList|AliyunTemplate\[ \]|List of preset task output templates.|
|State|String|Task status,which has the following options: Submitted, Analyzing, Success, and Fail

|
|Code|String|Error code displayed when the analysis fails.|
|Message|String|Error message displayed when the analysis fails.|
|Percent|String|Transcoding progress.Value range: \[0, 100\].

|
|Priority|String|Task priority in the MPS queue.-   Value range: \[1, 10\]
-   Highest priority: 10
-   Default value: 10.

|
|UserData|String|Custom data.|
|PipelineId|String|MPS queue ID.|
|CreationTime|String|Time of adding the task.|
|MNSMessageResult|AliyunMNSMessageResult|Result sent by Message Service to notify the user of task completion.|

## AliyunSnapshotJob {#section_njh_xwh_y2b .section}

Screenshot task type

|Name|Type|Description|
|:---|:---|:----------|
|Id|String|Screenshot task ID.|
|Input|AliyunOSSFile|Task input.|
|SnapshotConfig|AliyunSnapshotConfig|Screenshot configuration.|
|Count|String|Number of screenshots.|
|State|String|Screenshot status,which has the following options: Analyzing, Success, and Fail.

|
|Code|String|Error code displayed when the analysis fails.|
|Message|String|Error message displayed when the analysis fails.|
|UserData|String|Custom data.|
|MNSMessageResult|AliyunMNSMessageResult|Result sent by Message Service to notify the user of task completion.|

## AliyunSnapshotConfig {#section_m5h_xwh_y2b .section}

Screenshot configurations

|Name|Type|Description|
|:---|:---|:----------|
|OutputFile|String|Screenshot output OSS configurations.|
|TileOutputFile|String|Output OSS configurations of tile task.|
|Time|String|Screenshots start time.Unit: milliseconds.

|
|Interval|String|Time interval of screenshots.-   If this parameter is set, screenshots are taken at intervals. The value must be greater than 0.
-   Unit: seconds
-   Default value: 10.

|
|Num|String|Number of screenshots.If this parameter is set, screenshots are taken at intervals.

|
|Width|String|Width of the screenshot output image.Value range: \[8,4096\]

|
|Height|String|Width of the screenshot output image.Value range: \[8,4096\]

|
|FrameType|String|Type of screenshots, which has the following options:-   normal: indicates normal frame,
-   intra: indicates I frames.

Default value: intra

|
|TileOut|String|Tile configuration.|

## AliyunFailReason {#section_rg3_xwh_y2b .section}

Failure cause type

|Name|Type|Description|
|:---|:---|:----------|
|Code|String|Error code displayed upon failure.|
|Message|String|Error message displayed upon failure.|

## AliyunMNSMessageResult {#section_er3_xwh_y2b .section}

Type of Message Service notifications of user's task completion result

|Name|Type|Description|
|:---|:---|:----------|
|ErrorCode|String|Error code displayed upon failure.|
|ErrorMessage|String|Error message displayed upon failure.|
|MessageId|String|ID of the success message.|

## Activity {#section_vbj_xwh_y2b .section}

Media workflow activity

|Name|Type|Description|
|:---|:---|:----------|
|Name|String|Media workflow activity name,**Note:** which is unique in the same workflow.

|
|Type|String|Media workflow activity type,which has the following options: Start, Snapshot, Transcode, Analysis, and Report.

|
|JobId|String|Task ID \(for example, analysis task ID, transcoding task ID, and screenshot task ID\) that is generated when the activity is run.|
|State|String|Status,which has the following options: Running, Success, Fail, and Skipped.

-   Skipped indicates that the activity is skipped.
-   For example, HD or SD transcoding activity is run after the analysis activity. The system determines to run which activity based on the actual conditions. If the resolution of the original video is low, the HD transcoding activity may be skipped.

|
|StartTime|String|Start time of running the activity|
|EndTime|String|End time of running the activity|
|Code|String|Error code.An error code is returned if the activity status is Fail.

|
|Message|String|Error message.An error message is returned if the activity status is Fail.

|

## MediaWorkflow {#section_tdk_xwh_y2b .section}

Media workflow

|Name|Type|Description|
|:---|:---|:----------|
|MediaWorkflowId|String|Media workflow ID.|
|Name|String|Media workflow name.|
|Topology|String|Topology of the media workflow.|
|State|String|Status,which has the following options: Inactive, Active, and Deleted.

|
|CreationTime|String|Creation time.|

## InputFile {#section_lwk_xwh_y2b .section}

Input file

|Name|Type|Description|
|:---|:---|:----------|
|Bucket|String|OSS Bucket|
|Location|String|OSS Location|
|Object|String|OSS Object|

## MediaWorkflowExecutionInput {#section_d4l_xwh_y2b .section}

Input of a media workflow execution instance

|Name|Type|Description|
|:---|:---|:----------|
|InputFile|[InputFile](https://help.aliyun.com/document_detail/29251.html#InputFile)|Input file of the media workflow.|
|UserData|String|Custom data.|

## MediaWorkflowExecution {#section_p2m_xwh_y2b .section}

Media workflow execution instance

|Name|Type|Description|
|:---|:---|:----------|
|RunId|String|Execution instance ID.|
|Input|[MediaWorkflowExecutionInput](https://help.aliyun.com/document_detail/29251.html#MediaWorkflowExecutionInput)|Input of the media workflow.|
|MediaWorkflowId|String|Media workflow ID.|
|Name|String|Media workflow name.|
|MediaId|String|Media ID.All information generated by the media workflow belongs to this media ID.

|
|ActivityList|[Activity](https://help.aliyun.com/document_detail/29251.html#Activity)|List of media workflow activities.|
|State|String|Status,-   which has the following options: Running, Completed, and Fail.
-   Completed only indicates that the execution of workflow completes. Whether each activity \(such as Transcode or Screenshot\) is successful depends on the specific status value of each activity.

|
|CreationTime|String|Creation time.|

## MediaInfo {#section_jwm_xwh_y2b .section}

Attribute type

|Name|Type|Description|
|:---|:---|:----------|
|Format|[FormatInfo](https://help.aliyun.com/document_detail/29251.html#FormatInfo)|Format information.|
|Streams|[StreamsInfo](https://help.aliyun.com/document_detail/29251.html#StreamsInfo)|Streaming information.|

## Formatinfo {#section_mln_xwh_y2b .section}

Container and general information type

|Name|Type|Description|
|:---|:---|:----------|
|NumStreams|String|Total number of media streams.|
|NumPrograms|String|Total number of program streams.|
|FormatName|String|Brief name of the container/encapsulation format.|
|FormatLongName|String|Long name of the container/encapsulation format|
|StartTime|String|The start time.|
|Duration|String|Total time.|
|Size|String|File size.|
|Bitrate|String|Total bit rate.|

## StreamsInfo {#section_jb4_xwh_y2b .section}

Stream information type

|Name|Type|Description|
|:---|:---|:----------|
|VideoStreamList|[VideoStream](https://help.aliyun.com/document_detail/29251.html#VideoStream)\[\]|Video stream list,containing up to four video streams.

|
|AudioStreamList|[AudioStream](https://help.aliyun.com/document_detail/29251.html#AudioStream)\[\]|Audio stream list,containing up to four audio streams.

|
|SubtitleStreamList|[SubtitleStream](https://help.aliyun.com/document_detail/29251.html#SubtitleStream)\[\]|Subtitle stream list,containing up to four subtitle streams.

|

## VideoStream {#section_ir4_xwh_y2b .section}

Video stream information type

|Name|Type|Description|
|:---|:---|:----------|
|Index|String|Video stream number,used to identify the position of the video stream in the whole media streams.

|
|CodecName|String|Brief name of the encoding format.|
|CodecLongName|String|Long name of the encoding format.|
|Profile|String|Encoding preset.|
|CodecTimeBase|String|Encoding time base.|
|CodecTagString|String|Mark text of the encoding format.|
|CodecTag|String|Encoding format mark.|
|Width|String|Video resolution width, numbers.|
|Height|String|Video resolution height.|
|HasBFrames|String|Whether the video has B frames.|
|Sar|String|Encoding signal resolution ratio.|
|Dar|String|Encoding display resolution ratio.|
|PixFmt|String|Pixel format.|
|Level|String|Encoding level.|
|Fps|String|Target frame rate.|
|AvgFPS|String|Average frame rate.|
|Timebase|String|Time base.|
|StartTime|String|The start time.|
|Duration|String|Time length.|
|NumFrames|String|Total number of frames.|
|Lang|String|Language.|
|NetworkCost|[NetworkCost](https://help.aliyun.com/document_detail/29251.html#NetworkCost)|Network bandwidth consumption.|

## NetworkCost {#section_d2p_xwh_y2b .section}

Video network bandwidth consumption type

|Name|Type|Description|
|:---|:---|:----------|
|PreloadTime|String|Preload time.|
|CostBandwidth|String|Maximum bandwidth consumption.|
|AvgBitrate|String|Average bit rate.|

## AudioStream {#section_zsp_xwh_y2b .section}

Audio stream information type

|Name|Type|Description|
|:---|:---|:----------|
|Index|String|Audio stream number,used to identify the position of the audio stream in the whole media streams.

|
|CodecName|String|Brief name of the encoding format.|
|CodecLongName|String|Long name of the encoding format.|
|CodecTimeBase|String|Encoding time base.|
|CodecTagString|String|Mark text of the encoding format.|
|CodecTag|String|Encoding format mark.|
|SampleFmt|String|Sample format.|
|Samplerate|String|Sampling rate.|
|Channels|String|Number of audio channels.|
|ChannelLayout|String|Audio channel output layout.|
|Timebase|String|Time base.|
|StartTime|String|The start time.|
|Duration|String|Time length.|
|Bitrate|String|Bit rate.|
|NumFrames|String|Total number of frames.|
|Lang|String|Language.|

## SubtitleStream {#section_k2q_xwh_y2b .section}

Subtitle stream information type

|Name|Type|Description|
|:---|:---|:----------|
|Index|String|Subtitle stream number,used to identify the position of the subtitle stream in the whole media streams.

|
|Lang|String|Language.|

## Media {#section_aqq_xwh_y2b .section}

Media

|Name|Type|Description|
|:---|:---|:----------|
|MediaId|String|Media ID.|
|File|[File](https://help.aliyun.com/document_detail/29251.html#File)|Original file.|
|Title|String|Title.|
|Description|String|Description.|
|CateId|String|Category ID.|
|CateName|String|Category name.|
|Tags|String\[\]|Tag list.|
|RiskFactor|String|Risk factors.-   Value range: \[0,1\].
-   A higher value of risk factor indicates a higher possibility of involvement in pornography and violence.
-   The recognition accuracy reaches 80%.

|
|CoverURL|String|Cover URL.|
|PublishState|String|Media publishing status, indicating whether to publish the media.The options are as follows:

-   Initiated \(initial state\),
-   UnPublish \(not published, and the OSS playback file permission is Private\),
-   Published \(published, and the OSS playback file permission is Default\),
-   and Deleted \(deleted\).

|
|RunIdList|String\[\]|Media task stream list.|
|CreationTime|String|Creation time.|
|Duration|String|Time length.|
|Format|String|Format .|
|Size|String|Size.|
|Bitrate|String|Bit rate.|
|Fps|String|Frame rate.|
|Width|String|Width.|
|Height|String|Height.|
|PlayList|[Play](https://help.aliyun.com/document_detail/29251.html#Play)\[\]|Playlist.|
|SnapshotList|[Snapshot](https://help.aliyun.com/document_detail/29251.html#Snapshot)\[\]|Screenshot list|
|MediaInfo|[MediaInfo](https://help.aliyun.com/https://help.aliyun.com/document_detail/29251.html#MediaInfo)|Media information.|

## Category {#section_acr_xwh_y2b .section}

Category

|Name|Type|Description|
|:---|:---|:----------|
|CateId|String|Category ID.|
|ParentId|String|Parent node ID.The value of the top-level node is -1.

|
|CateName|String|Category name.|
|Level|String|Level.The top-level node value is 0.

|

## File {#section_tnr_xwh_y2b .section}

File

|Name|Type|Description|
|:---|:---|:----------|
|URL|String|File URL.|
|State|String|File status,which has the following options: Normal and Deleted.

|

## Play {#section_c1s_xwh_y2b .section}

Playback information

|Name|Type|Description|
|:---|:---|:----------|
|MediaWorkflowId|String|ID of the workflow that generates the playback file.|
|MediaWorkflowName|String|Workflow that generates the playback file.|
|ActivityName|String|Media workflow activity name.|
|Duration|String|Time length.|
|Format|String|Format.|
|Size|String|Size.|
|Bitrate|String|Bit rate.|
|Fps|String|Frame rate.|
|Width|String|Width.|
|Height|String|Height.|
|File|[File](https://help.aliyun.com/document_detail/29251.html#File)|Playback file.|

## Snapshot {#section_mms_xwh_y2b .section}

Screenshot information

|Name|Type|Description|
|:---|:---|:----------|
|MediaWorkflowId|String|ID of the workflow that generates the screenshot file.|
|MediaWorkflowName|String|Workflow that generates the screenshot file|
|ActivityName|String|The name of the workflow activity that generated the screenshot file.|
|File|[File](https://help.aliyun.com/document_detail/29251.html#File)|Screenshot files.|
|Type|String|Snapshot type,which has the following options: Single and Sequence.

|
|Count|Number|Number of screenshots.This parameter is valid only when Type is set to Sequence.

|

## MediaBucket {#section_dys_xwh_y2b .section}

Media bucket

|Name|Type|Description|
|:---|:---|:----------|
|Bucket|String|The bucket name.|
|Type|String|Media bucket type,which has the following options: Input,

and Output.|

## AliyunMediaCensorJob {#section_tmx_bys_2fb .section}

Media audit jobs

|Name|Type|描述|
|:---|:---|:-|
|Id|String|Job ID|
|Input|AliyunOSSFile|Operation Input|
|Videocensorconfig|Aliyunvideocensorconfig|Video review Configuration|
|PipelineId|String|Pipe ID|
|state|String|which has the following options: Submitted, Analyzing, Success, and Fail|
|Code|String|Error Code on job failure|
|-|-|Error message on job failure|
|-|-|Custom data.|
|Result|String|Job overall audit results. Valid value:-   -
-   Review: manual retrial-
-   -Block: intercept.

-When any type of audit result is review, the overall result is review, when any type of audit result is block, the overall result is block.|
|-Titlecensorresult|-Aliyuncommoncensorresult|-Title audit results|
|-Desccensorresult|-Aliyuncommoncensorresult|-Describe audit results|
|-Barragecensorresult|-Aliyuncommoncensorresult|Test results of elastic curtain|
|-Imagecensorcensorresult|-Aliyunimagecensorresult \[\]|-Cover review results|
|-Videocensorresult|Aliyunvideocensorresult|-Video review results|

## -Aliyunvideocensorconfig {#section_jcg_pys_2fb .section}

-Video Audit Configuration

|Name-|Type-|Required-|Description-|
|:----|:----|:--------|:-----------|
|OutputFile-|String-|Yes-|-The Save address of the result of the video capture.For example: "\{" Bucket ":" Test-bucket "," location ": "OSS-CN-Shanghai", "object "\}".

其中\{Count\}是占位符,图片Object依次为output00001.jpg,output00002.jpg etc.

|
|-Videocensor|String-|No-|Whether you need to audit video content.Default value: true.-

-When set to false, you must ensure that the same media input file has been submitted before, and it is the execution of the successful state, otherwise the request will be rejected.

|
|-Maid type|String|No|The default common. -|
|-Resultrange|String-|No-|-Scope of audit results, including:-   Abnormal: contains only audit problematic results,
-   ALL: contains all results.

Default: abnormal.

|

## Aliyuncommoncensorresult {#section_inx_bys_2fb .section}

General purpose audit results

|Name|-|-|
|:---|:-|:-|
|Score|String|Score value.Value range: \[0, 100\].

Example: 99.91.

|
|-|String|Handle recommendations. Valid value:-   Pass: pass,-
-   -Review: manual retrial,
-   Block: intercept.

 |
|Scene|String|Audit scenario.-   Antispam: Text anti-spam,
-   Porn: porn,
-   Terrorism: violence against politics.

|
|Label|String|The label of the audit result.-   Normal: normal,
-   Spam: Contains junk information,
-   AD: advertising,
-   Politics: politics,
-   Terrorism: violent fear,
-   Abuse: abuse,
-   Flood: irrigation,
-   Contraband: prohibited,
-   Meiingless: meaningless,
-   Porn: porn,
-   Sexy: sexy,
-   Outfit: special outfit,
-   Logo: special logo,
-   Weapon: weapon,
-   Political: political,
-   Others: others.

 |

## Aliyunimagecensorresult {#section_nnx_bys_2fb .section}

Cover page \(picture\) audit results

|Name|类型|描述|
|:---|:-|:-|
|Location|String|Top features of the video cover OSS location|
|Bucket|String-|Video cover OSS Bucket|
|Object|String|Video cover OSS object|
|Result-|Aliyuncommoncensorresult|Review Result-|

## Aliyunvideocensorresult {#section_snx_bys_2fb .section}

Video audit results

|Name-|类型-|描述-|
|:----|:--|:--|
|Censorresult|Aliyuncommoncensorresult \[\]|A collection of audit results that contains summary information about a variety of scenes \(yellow, fear, storm, politics.|
|Videotimelines|Aliyuntimelinecensorresult \[\]|Detailed point-in-time audit results, sorted from small to large by time.|
|Nextpagetoken|String-|The next page identifies 32-bit UUID.|
|Maximumpagesize|String-|Maximum number of returns per page.Default: 30

Value range: \[1, 200\].-

|

## Aliyuntimelinecensorresult {#section_bdk_pzs_2fb .section}

Timeline audit results

|Name-|类型-|描述-|
|:----|:--|:--|
|Timestamp-|String-|The location in the video.Format: hh: mm: ss \[. Sss\].

Example: 00:02:59. 999

|
|Object|String-|Capture the OSS storage path.|
|Censorresult|Aliyuncommoncensorresult \[\]|Contains labels, score values, and so on for various types of audit results.|

## Aliyuncensorjobnotify {#section_a4x_bys_2fb .section}

Content Audit job notification

|Name-|类型-|描述-|
|:----|:--|:--|
|Typ|String-|Notification Type, mediacensor: Media audit job.|
|UserData|Stromg|Userdata when the user submits the job for the return parameter.|
|JobI|Strin|JobID|
|Inpu|AliyunOSSFile|Operation Input|
|stat|Strin|Job status, success, fail|
|Cod|Strin|Error Code on job failure|
|Messag|Strin|Error message on job failure|
|Resul|Strin|Job overall audit results. Valid value: -   Pass: pass,-
-   -Review: manual retrial,
-   Block: intercept.

-When any type of audit result is review, the overall result is review, when any type of audit result is block, the overall result is block.

|
|-Titlecensorresult|Aliyuncommoncensorresult|-Title audit results|
|-Desccensorresult|Aliyuncommoncensorresult|-Describe audit results|
|-Barragecensorresult|Aliyuncommoncensorresult|Test results of elastic curtain|
|-Imagecensorcensorresult|-Aliyunimagecensorresult \[\]|-Cover review results|
|Topvideocensorresult|Aliyunvideocensorresult|Includes top results with the highest score for each audit type in the video, the corresponding timelines contain up to 10 pieces of data, and, if not, the timelines are empty.|

