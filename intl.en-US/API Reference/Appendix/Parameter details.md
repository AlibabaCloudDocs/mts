# Parameter details {#reference_hhy_xc4_y2b .reference}

This article introduces the details of the parameters.

## Input {#section_f3p_d24_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|:-------|:----------|
|Bucket|String|Yes|OSS bucket that stores the input file.You must assign the read and write permissions on this bucket to Media Processing on the bucket authorization page in the resource control channel of the console. This parameter complies with the OSS bucket definition. For more information, see the definition of “bucket” in the glossary.

|
|Location|String|Yes|Data center \(also called OSS location\) where the OSS bucket that stores the input file is located.This parameter complies with the OSS location definition. For more information, see the definition of “location” in the glossary.

|
|Object|String|Yes|Name of the input file \(an OSS object\),which must be subject to URL encoding and UTF-8 encoding. This parameter complies with the OSS object definition. For more information, see the definition of “object” in the glossary.

|

## Output {#section_l1z_h24_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|OutputObject|String|Yes|Name of the output file \(an OSS object\),-   which must be subject to URL encoding and UTF-8 encoding.
-   Example of placeholder replacement: If the input file for transcoding is a/b/c.flv and OutputObject is set to %7BObjectPrefix%7D%7BFileName%7Dtest.mp4, then the output file is a/b/ctest.mp4.
-   The placeholder replacement rules are applicable to output file naming.
    -   The following placeholders are supported by workflows: \{ObjectPrefix\} indicates the prefix of the input file name; \{FileName\}, the input file name; \{ExtName\}, the input file name extension; \{DestMd5\}, the MD5 value of the output file; \{DestAvgBitrate\}, the average bit rate of the output file; \{RunId\}, the ID of a media workflow execution instance; and \{MediaId\}, the ID of the media file processed by a workflow. These placeholders can be replaced dynamically.
    -   The following placeholders are supported by non-workflows: \{ObjectPrefix\}, \{FileName\}, \{ExtName\}, \{DestMd5\}, and \{DestAvgBitrate\}.
-   Rules related to file name extension:
    -   Workflow: A file name extension is automatically appended to OutputObject according to the container format of the transcoding template.
    -   Non-workflow: A file name extension is not automatically added. However, if the container type is M3U8, Media Transcoding automatically adds the file name extension .m3u8 to the playlist file name. For slice naming, the playlist file name is automatically added with a suffix of 5-digit serial number starting from 00001.
-   The serial number and playlist file name are connected by a hyphen`-`. The file name extension is .ts.
-   For example, if the playlist file is filename.m3u8, the first slice .ts to be output is named in the format of filename-00001.ts.

|
|TemplateId|String|Yes|The transcoding template ID.Media Processing supports custom transcoding templates and preset transcoding templates.

|
|WaterMarks|WaterMark\[\]|No|A list of watermarks formatted as a JSON array. For more information, see “5. Transcoding watermark parameters.”-   The watermark array size limit is 20, indicating that up to 20 watermarks can be included in one output.
-   Example: `[{``"InputFile":{``"Bucket":"example-bucket",``"Location":"oss-cn-hangzhou",``"Object":"example-logo.png"``},``"WaterMarkTemplateId":"88c6ca184c0e47098a5b665e2a126797"``}]`

|
|Clip|String|No|Video clip, which is a JSON object. For more information, see “3. Clip.”Example: `{``"TimeSpan":{``"Seek":"123.45",``"Duration":"3.45"``}``}`

|
|Rotate|String|No|Video rotation angle.Value range: \[0, 360\). The rotation is clockwise.

|
|Container|String|No|If this parameter is set, it overwrites the Container parameter in the specified transcoding template. For more information, see “7. Container.”|
|Video|String|No|If this parameter is set, it overwrites the Video parameter in the specified transcoding template. For more information, see [Video](reseller.en-US/API Reference/Appendix/Parameter details.md#) .|
|Audio|String|No|If this parameter is set, it overwrites the Audio parameter in the specified transcoding template. For more information, see [Audio](reseller.en-US/API Reference/Appendix/Parameter details.md#) .|
|Audiostreammap|String|No|Audio stream sequence number.-   Format: 0:a:\{sequence number\}.
-   The sequence starts with zero.
-   The sequence number indicates the subscript of the audio streams list.
-   Example: 0:a:0.
-   If this parameter is not set, the default audio stream is selected.

|
|TransConfig|String|No|Transcoding process configuration. If this parameter is set, it overwrites the TransConfig parameter in the specified transcoding template. For more information, see “16. TransConfig.”|
|MergeList|String|No|Merging setting. Up to four MergeURLs. For more information, see “ Merging.”-   Example of a single merged part: `[{"MergeURL":"http://jvm.oss-cn-hangzhou.aliyuncs.com/tail_comm_01.mp4"}]`
-   Example of two merged parts: `[{"MergeURL":"http://jvm.oss-cn-hangzhou.aliyuncs.com/tail_comm_01.mp4","Start":"1","Duration":"20"},{"MergeURL":"http://jvm.oss-cn-hangzhou.aliyuncs.com/tail_comm_02.mp4","Start":"5.4","Duration":"10.2"}]`

 |
|MergeConfigUrl|String|No|MergeConfigUrl and MergeList are mutually exclusive.-   MergeConfigUrl supports up to 100 merged parts.
-   MergeConfigUrl indicates the URL of a merging configuration file.
-   Example: `http://jvm.oss-cn-hangzhou.aliyuncs.com/mergeConfigfile`
-   The merging configuration file must be stored in OSS and its access permission must be granted to Media Processing. For more information about the file content, see “27. Merging.”
-   The following is the sample content of mergeConfigfile: `{``"MergeList":[{"MergeURL":"http://jvm.oss-cn-hangzhou.aliyuncs.com/tail_comm.mp4"}]``}`

|
|MuxConfig|String|No|If this parameter is set, it overwrites the MuxConfig parameter in the specified transcoding template. For more information, see “MuxConfig.”|
|Priority|String|No|Task priority in the MPS queue.-   Value range: \[1, 10\]
-   Highest priority: 10
-   Default value: 6

 |
|UserData|String|No|Custom data, up to 1,024 bytes.|
|M3U8NonStandardSupport|String|No|M3U8 custom parameter support. The parameter value is a JSON object. For more information, see “ M3U8 custom parameters.” Example: `{``"TS":{"Md5Support":true,"SizeSupport":true}``}`|
|Encryption|String|No|Data encryption, which only supports output in M3U8 format.-   Example: `{``"Type":"hls-aes-128",``"Key":"ZW5jcnlwdGlvbmtleTEyMw",``"KeyType":"Base64",``"KeyUri":"aHR0cDovL2FsaXl1bi5jb20vZG9jdW1lbnQvaGxzMTI4LmtleQ=="``}`
-   For more information, see “ Encryption parameters.”

 |
|SubtitleConfig|String|No|Subtitle configuration, which is a JSON object.-   For more information, see “SubtitleConfig.”
-   Example: \{“ExtSubtitleList”:\[\{“Input”:\{“Bucket”:”example-bucket”,“Location”:”oss-cn-hangzhou”,“Object”:”example.srt”\},“CharEnc”:”UTF-8”\}\]\}

|
|OpeningList|String|No|Opening list. JSON format.-   For more information, see “ Opening.
-   Example: `[{"OpenUrl":"http://test-bucket.oss-cn-hangzhou.aliyuncs.com/opening.flv","Start":"1","Width":"1920","Height":"1080"}]`

|
|TailSlateList|String|No|Tail slate list, in JSON format.-   For more information, see “ TailSlate.”
-   Example: `[{"TailUrl":"http://test-bucket.oss-cn-hangzhou.aliyuncs.com/tail.flv","Start":"1","BlendDuration":"2","Width":"1920","Height":"1080","IsMergeAudio":false,"BgColor":"White"}]`

|
|DeWatermark|String|No|Blurring watermark, JSON object. For more information, see DeWatermark.|
|Amix|String|否|Audio mixing. Scenarios: for example, to add background music; and to mix two audio tracks of a video.

Use the AudioStreamMap parameter to select the audio track of the input video for audio mixing.

JSON list format, example: \[\{“AmixURL”:“http://test-bucket.oss-cn-hangzhou.aliyuncs.com/audio.mp3",“Map”:“0:a:0”,“MixDurMode”:"longest”\}\]|

## Clip {#section_b5z_h24_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|TimeSpan|String|No|Time span of a clip.For more information, see TimeSpan.

|
|ConfigToClipFirstPart|Boolean|No|Whether to clip the first part.-   false: \(Default\) Clip after merging
-   true: Merge after clipping the first part|

|

## TimeSpan {#section_pk1_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Seek|String|No|Start time,-   Format: hh: mm: ss \[. SSS\]，
-   Value range is \[00:00:00.000, 23:59:59.999\],

or,

-   Format: sssss \[. SSS\]，
-   Value range: \[0.000, 86399.999\]

Example: 01:59:59.999 or 32000.23

|
|Duration|String|No|Duration.-   Format: hh: mm: ss \[. SSS\]，
-   Value range is \[00:00:00.000, 23:59:59.999\],

or,

-   Format: sssss\[. SSS\],
-   Value range is \[0.000, 86399.999\].

Example: 01:00:59.999 or 32000.23

|
|End|String|No|Duration truncated in the end.The Duration parameter is invalid if this parameter is set.

-   Format: hh:mm:ss\[. SSS\]
-   Value range: \[00:00:00.000, 23:59:59.999\],

or

-   Format: sssss\[. SSS\],
-   Value range: \[0.000, 86399.999\].

Example: 01:00:59.999 or 32000.23

|

## Transcoding watermark parameter {#section_dy1_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|WaterMarkTemplateId|String|No|Watermark template ID.If this parameter is not set, the following default settings are applied:

-   The watermark position is TopRight;
-   offsets Dx and Dy are 0;
-   The watermark width is 0.12 times the resolution width of the output video;
-   The watermark height scales proportionally relative to watermark width.

|
|InputFile|String|Yes|Input watermark file.-   For more information, see the description of InputFile.
-   Currently, images in PNG format and files in MOV format can be input as watermarks.

|
|Width|String|No|If this parameter is set, it overwrites the watermark width setting of the watermark template. The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the watermark image width in pixels;
    -   Value range: \[8, 4096\].
    -   Unit: Px
-   In decimal number form, this parameter indicates a ratio relative to the resolution width of the output video;
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|Height|String|No|If this parameter is set, it overwrites the watermark height setting of the watermark template. The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the watermark image height in pixels.
    -   Value range is \[8, 4096\].
    -   Unit: Px.
-   In decimal number form, this parameter indicates a ratio relative to the resolution height of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|Dx|String|No|If this parameter is set, it overwrites the Dx parameter of the watermark template. This parameter indicates the horizontal offset of the watermark image relative to the output video.Default value: 0.

The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the number of offset pixels.
    -   Value range: \[8, 4096\].
    -   Unit: Px,
-   In decimal number form, this parameter indicates the ratio of horizontal offset to the resolution width of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|Dy|String|No|If this parameter is set, it overwrites the Dy parameter of the watermark template. This parameter indicates the vertical offset of the watermark image relative to the output video.Default value: 0.

The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the number of offset pixels.
    -   Value range: \[8, 4096\].
    -   Unit: Px,
-   In decimal number form, this parameter indicates the ratio of vertical offset to the resolution height of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|ReferPos|String|No|If this parameter is set, it overwrites the ReferPos parameter of the watermark template.It indicates the watermark position and can be set to TopRight, TopLeft, BottomRight, or BottomLeft.

|
|Type|String|No|If this parameter is set, it overwrites the Type parameter of the watermark template. It indicates the watermark type and can be set to Image or Text.-   Image: image watermark,
-   Text \(text watermark\).

-   Default value: Image.

**Note:** If it is set to Text, the TextWaterMark parameter must be set.Text: Text watermark.

|
|Timeline|String|No|If this parameter is set, it overwrites the Timeline parameter of the watermark template. It indicates a dynamic watermark.For more information, see the description of Timeline.

|
|TextWaterMark|String|No|Text watermark configuration, which is a JSON object. This parameter must be set if Type is set to Text.-   For more information, see “37. Text watermark parameters.” Example: \{“Content”:”5rWL6K+V5paH5a2X5rC05Y2w”,”Top”:2,”Left”:10\}
-   Example: \{“Content”:”5rWL6K+V5paH5a2X5rC05Y2w”,”Top”:2,”Left”:10\}

|

## Watermark template configuration {#section_bjb_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Width|String|No|Width of the watermark image in the output video.The parameter value can be an integer or a decimal number.

-   In integer form, this parameter indicates the watermark image width in pixel.
    -   Value range: \[8, 4096\].
    -   Unit: Px;
-   In decimal number form, this parameter indicates a ratio relative to the resolution width of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|Height|String|No|Height of the watermark image in the output video. The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the watermark image height in pixels.
    -   Value range: \[8, 4096\], unit: px.
-   In decimal number form, this parameter indicates a ratio relative to the resolution height of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|Dx|String|No|Horizontal offset of the watermark image relative to the output video.Default value: 0.

 The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the number of offset pixels.
    -   Value range: \[8, 4096\].
    -   Unit: Px;
-   In decimal number form, this parameter indicates the ratio of horizontal offset to the resolution width of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|Dy|String|No|Vertical offset of the watermark image relative to the output video.Default value: 0.

The parameter value can be an integer or a decimal number.-   In integer form, this parameter indicates the number of offset pixels.
    -   Value range: \[8, 4096\].
    -   Unit: Px;
-   In decimal number form, this parameter indicates the ratio of vertical offset to the resolution height of the output video.
    -   Value range: \(0, 1\).
    -   Up to four digits are allowed after the decimal point, for example, 0.9999, and excessive digits are automatically dropped.

|
|ReferPos|String|No|Watermark position.-   This parameter can be set to TopRight, TopLeft, BottomRight, or BottomLeft.
-   Default value: TopRight.

|
|Type|String|No|Watermark type. This parameter can be set to Image or Text.-   Default value: Image.
-   Currently, only the Image type is supported.

|
|Timeline|String|No|Dynamic watermark.For more information, see the description of Timeline.

|

Description of the Width and Height parameters:

-   When neither the Width nor the Height parameter is set, the watermark width is 0.12 times the resolution width of the output video and the watermark height scales proportionally according to the aspect ratio of the original watermark image.
-   When either the Width or the Height parameter is set, the unspecified side scales proportionally according to the aspect ratio of the original watermark image.
-   When the Width and Height parameters are set, the watermark image is set based on actual values.

Description of watermark coordinates:

![](images/10495_en-US.png)

## Container {#section_fqc_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Format|String|No|Container format.-   Default value: MP4
-   Video transcoding supports the FLV, MP4, HLS（m3u8+ts）and MPEG-DASH（MPD+fMP4）formats.
-   Audio transcoding supports the MP3, MP4, OGG, FLAC, and m4a formats.
-   Image supports gif and webp formats.
-   When the container format is gif, Video Codec can only be set as GIF.
-   When the container format is webp, Video Codec can only be set as WEBP.
-   When the container format is flv, Video Codec cannot be set as H. 265.

|

## Video {#section_pfd_324_y2b .section}

|Parameter|Type|Required|Meaning|Description|
|:--------|:---|:-------|:------|:----------|
|Codec|String|No|Codec format|Optional values: H. 264, H. 265, GIF, webp.Default value: H. 264

|
|Profile|String|No|Encoding level|Optional values: baseline, main, and high.Default value: high

-   baseline: applicable to mobile devices.
-   main: applicable to standard-definition \(SD\) devices.
-   high: applicable to high-definition \(HD\) devices.

Best practice: If multiple definitions exist, we recommend that you set Profile to baseline for the lowest definition to guarantee normal play on low-end devices, and set Profile to main or high for other definitions.

**Note:** Currently, this parameter is only supported by H. 264.

|
|Bitrate|String|No|Bit rate of the output video file| -   Value range: \[10,50000\]
-   Unit: kbps

 |
|Crf|String|No|which is a quality control factor.| -   Value range: \[0, 51\]
-   Default value: 26

 **Note:** The Bitrate parameter is invalid if the Crf parameter is set.

 |
|Width|String|No|Width| -   Default value: original video width.
-   Value range: \[128, 4096\].
-   Unit: Px

 |
|Height|String|No|Height| -   Default value: original video height.
-   Value range: \[128, 4096\].
-   Unit: Px

 |
|Fps|String|No|Frame rate| -   Default value: frame rate of the input file.
-   If the frame rate of the input file is greater than 60, the value still takes 60.
-   Value range: \(0, 60\].
-   Unit: fps.

 |
|GOP|String|No|Maximum time interval or maximum number of frames between two key frames.|Maximum time interval, the unit second is required to be entered.-   Default value: 10s.
-   Maximum number of frames between two key frames: no unit.
-   Value range: \[1,100000\]

|
|Preset|String|No|Preset video algorithm|Optional values: veryfast, fast, medium, slow, and slower.Default value: medium

**Note:** Currently, this parameter is only supported by H. 264.

|
|ScanMode|String|No|Scan mode|Optional values: interlaced and progressive.|
|Bufsize|String|No|Buffer size| -   Value range: \[1000,128000\]
-   Default value: 6000
-   Unit: Kb

 |
|Maxrate|String|No|Peak video bit rate|Value range \[10,50000\], in kbps.|
|PixFmt|String|No|Video color format|Optional values: yuv420p, yuvj420p, and other standard color formats.Default value: yuv420p or original color format.

|
|Remove|String|No|Whether to delete video streams| -   true \(delete video streams\),
-   and false \(retain video streams\).
-   Default value: false.

 |
|Crop|String|No|Video cropping|Two cropping methods are supported.-   Automatically detect and crop black borders \(Crop is set to “border”\);
-   Custom cropping, in which case the parameter value is in the format of width:height:left:top.

Example: 1280:800:0:140


|
|Pad|String|No|Pad video with black borders|Parameter value format: width:height:left:top. Example: 1280:800:0:140

|
|Longfig Mode|String|No|Whether to enable auto-rotate screen \(that is long edge and short edge mode\).| -   The width of the transcoding output corresponds to the long edge of the input source \(The vertical screen is height of the source\).
-   The height corresponds to the short edge of the input video \(The vertical screen is width of the source \).
-   True indicates enabled.
-   False indicates disabled.

 Default value: false.

 |

The following table lists the supported combinations of video transcoding codec formats and container formats.

|Container|Audio codecs|Video Codecs|
|:--------|:-----------|:-----------|
|flv|AAC, MP3|H.264|
|mp4|AAC, MP3|H.264, H. 265|
|ts|AAC, MP3|H.264, H. 265|
|m3u8|AAC, MP3|H.264, H. 265|
|gif|Not supported|GIF|

The following table lists the supported combinations of video codec formats and video stream parameters.

|Video/Codec|H.264|H.265|GIF|
|:----------|:----|:----|:--|
|Profile|Y|N|N|
|Bitrate|Y|Y|N|
|Crf|Y|Y|N|
|Width|Y|Y|Y|
|Height|Y|Y|Y|
|Fps|Y|Y|Y|
|Gop|Y|Y|N|
|Preset|Y|N|N|
|ScanMode|Y|Y|Y|
|Bufsize|Y|Y|N|
|Maxrate|Y|Y|N|
|PixFmt|Y|Y|bgr8|

## Audio {#section_htd_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Codec|String|No|Audio codec format: AAC, MP3, VORBIS, and FLAC.Default value: AAC.

|
|Profile|String|No|Preset audio encoding.Optional values when Codec is set to AAC: aac\_low, aac\_he, aac\_he\_v2, aac\_ld, and aac\_eld.

|
|Samplerate|String|No|Sampling rate.-   Default value: 44100.
-   Optional value: 22050, 32000, 44100, 48000, and 96000.
-   Unit: Hz.

**Note:** 

-   When the video container format is FLV and the audio codec format is MP3, Samplerate cannot be set to 32000, 48000, or 96000.
-   When the audio codec format is MP3, Samplerate cannot be set to 96000.

|
|Bitrate|String|No|Audio bit rate of the output file.-   Value range: \[8,1000\],
-   Unit: kbps
-   Default value: 128

|
|Channels|String|No|Number of sound channels.Default value: 2

**Note:** 

-   It can be set to either 1 or 2 when Codec is set to mp3.

 Or it can be set to 1, 2, 4, 5, 6, or 8 when Codec is set to acc.|
|Remove|String|No|Whether to delete audio streams.-   true \(delete video streams\),
-   and false \(retain video streams\).
-   Default value: false.

|

The following table lists the supported combinations of audio transcoding codec formats and container formats.

|Container|Audio Codecs|
|:--------|:-----------|
|mp3|MP3|
|mp4|AAC|
|ogg|VORBIS, FLAC|
|flac|FLAC|

## Snapshopconfig {#section_zh2_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Format|String|No|Screenshots data type.-   Default value: null.
-   VTT can be specified to represent output webvtt.

|
|BlackLevel|String|No|This parameter specifies the black pixel threshold that is used to detect black frames in the first screenshot for multi-screenshot capture.

-   No default value is available.
-   Value range: \[30,100\]

The smaller the value, the fewer black pixels in a frame.

-   If the screenshot capture time specified by the Time parameter is greater than 0, the BlackLevel setting does not take effect and black frame filtering is not performed.
-   If the screenshot capture time is 0 and the number of screenshots specified by the Num parameter is greater than 1, the BlackLevel setting takes effect. If theblack pixel proportion of the captured frame is lower than the threshold, the frame is used directly. If the black pixel proportion of the captured frame is greater than or equal to the threshold, the frame is filtered out. Black frame filtering continues to check the first five seconds to locate a frame with a black pixel proportion lower than the threshold.
-   If the screenshot capture time is 0 and the number of screenshots is 1, the BlackLevel setting does not take effect but black frame filtering will still be performed.

To filter frames that contain only black pixels, set the BlackLevel parameter to 100.

Example:

 When the screenshot capture time is 0 and the number of screenshots is 10, set the BlackLevel parameter to 100 to filter out frames that contain only black pixels in the first screenshot.|
|OutputFile|String|Yes|Output file, which is a JSON object.For more information, see “38. Screenshot OutputFile.”

|
|TileOutputFile|String|No|The output file, which is a JSON object, and the structure is the same as the OutputFile.-   The format of the screenshot output file is jpg, if the asynchronous mode sequence tile is used, and the value of Num does not equal 1, then the Object of TileOutputFile must include \{TileCount\}, so as to differentiate the output address of multiple output images in sequence screenshot. For example: 3 images are output in sequence screenshot, the Object of TileOutputFile is \{TileCount\}.jpg, then the Object of output screenshot are 00001.jpg, 00002.jpg, and 00003.jpg respectively.
-   This parameter is required in the tile configuration. TileOutputFile indicates the large image address that is finally tiled out.

|
|Time|String|Yes|Time for screenshots.Unit: milliseconds.

|
|Interval|String|No|Screenshot interval.-   If this parameter is set, screenshots are taken in sequence asynchronously. The value must be greater than 0.
-   Default value: 10.
-   Unit: seconds
-   If Interval is set to 0, screenshots are taken at even intervals based on the video duration.

 |
|Num|String|No|Screenshot quantity.If this parameter is set, screenshots are taken in sequence asynchronously. The value must be greater than 0.

-   When the duration calculated by Time + Interval x Num exceeds the video duration, screenshots are no longer taken beyond the calculated duration and the number of actual screenshots taken is returned.
-   When num = 1, the interval parameter is ignored, representing an asynchronous single capture.

|
|Width|String|No|Width of the output screenshot image.-   Unit: Px
-   Value range: \[8, 4096\].

|
|Height|String|No|Height of the output screenshot image.-   Unit: Px
-   Value range: \[8, 4096\].

|
|FrameType|String|No|Screenshot type.-   normal \(normal frame\),
-   and intra \(I frame\).

Default value: intra|
|Tileout.|String|No|Tile configuration. JSON object.For more information, see TileOut.

|
|SubOut|String|No|Webvtt tile configuration, JSON object.For more information, see SubOut.

|

## Segment {#section_it2_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Duration|String|No|Segment time length.-   Integer.
-   Unit: seconds
-   Value range: \[1,60\]

Default value: 10 seconds

|
|ForceSegTime|String|No|A list of up to 10 segment time points, separated by commas \(,\).-   Decimal, support three decimal digits
-   Unit: seconds
-   For example, 23,55,60 indicates processing segments at the 23th, 55th, and 60th seconds.

|

## TransConfig {#section_cdf_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|TransMode|String|No|Transcoding mode.-   Default value: onepass
-   Optional value: onepass, twopass, CBR.

|
|AdjDarMethod|String|No|Resolution rewrite mode.-   Default value: none
-   Optional value: rescale, crop, pad, none.

|
|IsCheckReso|String|No|Whether to check resolution.-   The output resolution is equal to the input resolution if the former is greater than the latter \(which is determined based on width or height\). true indicates check resolution.
-   false indicates not check resolution.
-   Default value: false.

|
|IsCheckResoFail|String|No|Whether to check resolution.-   An error indicating transcoding failure is returned if the output resolution is greater than the input resolution \(which is determined based on width or height\).
-   true: indicates check resolution.
-   false indicates not check resolution.
-   Default value: false.

|
|IsCheckVideoBitrate|String|No|Whether to check video bit rate.-   The output video bit rate is equal to the input video bit rate if the former is greater than the latter.
-   true indicates check resolution.
-   false indicates not check resolution.
-   Default value: false.

|
|IsCheckAudioBitrate|String|No|Whether to check the audio bit rate.-   The output audio bit rate is equal to the input audio bit rate if the former is greater than the latter.
-   true: indicates check resolution.
-   false: indicates not check resolution.
-   Default value: false.

|
|isCheckAudioBitrateFail|String|No|This parameter indicates the processing when the output video bit rate is greater than the media source video bit rate.-   If it is set to “true”, transcoding is not performed;
-   if it is set to “false”, checking is not performed.
-   Default value: false.
-   This parameter takes precedence over IsCheckVideoBitrate.

|
|isCheckVideoBitrateFail|String|No|This parameter indicates the processing when the output video bit rate is greater than the media source video bit rate.-   If it is set to “true”, transcoding is not performed;
-   if it is set to “false”, checking is not performed.
-   Default value: false.
-   This parameter takes precedence over IsCheckVideoBitrate.

|

Position of the AdjDarMethod parameter:

![](images/10548_en-US.png)

## MuxConfig {#section_enf_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Segment|String|No|Segment configuration, which is a JSON object.-   For more information, see “14. Segment.”
-   Example: `{``"Duration":"34"``}`

|

## NotifyConfig {#section_ayf_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|QueueName|String|No|MNS queue created in Alibaba Cloud Message Service.-   Media Processing allows you to bind an MNS queue to an MPS queue. After a task is executed in the MPS queue, the results are sent to the bound MNS queue.
-   For more information about how to acquire messages in the MNS queue, see [Queue message operation](../../../../reseller.en-US/Developer Guide/Receive message notifications/Receive notification through queues.md#).
-   Before you configure an MNS queue in the MPS queue, create the MNS queue in [Message Service](https://partners-intl.aliyun.com/login-required#/mns).

|
|Topic|String|No|Topic created in Alibaba Cloud Message Service.-   Media Processing allows you to bind a topic to an MPS queue. After a task is executed in the MPS queue, the results are sent to the bound topic,
-   and then the topic pushes the results in the form of a message to the subscribed address.
-   Before you configure a topic in a message queue, create a topic in Message Service.

**Note:** This function is currently under a public beta test.

|

## Transcoding task input {#section_r3g_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Bucket|String|Yes|OSS bucket that stores the input file.-   You must assign the read and write permissions on this bucket to Media Processing on the bucket authorization page in the resource control channel of the console.
-   This parameter complies with the OSS bucket definition. For more information, see the definition of “bucket” in the glossary.

|
|Location|String|Yes|Data center \(also called OSS location\) where the OSS bucket that stores the input file is located.This parameter complies with the OSS location definition. For more information, see the definition of “location” in the glossary.

|
|Object|String|Yes|Name of the input file \(an OSS object\),-   which must be subject to URL encoding and UTF-8 encoding.
-   This parameter complies with the OSS object definition. For more information, see the definition of “object” in the glossary.

|
|Audio|String|No|Audio configuration of the source media file, which is a JSON object.**Note:** This parameter must be set when the input file is in ADPCM or PCM format.

-   For more information, see “InputAudio.”
-   Example: `{``"Channels":"2",``"Samplerate":"44100"``}`

|
|Container|String|No|Container configuration of the source media file, which is a JSON object.**Note:** This parameter must be set when the input file is in ADPCM or PCM format.

-   For more information, see “InputContainer.”
-   Example: `{``"Format":"u8"``}`

|

## InputContainer {#section_n5g_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Format|String|Yes|Source media audio format.Optional values: alaw, f32be, f32le, f64be, f64le, mulaw, s16be, s16le, s24be, s24le, s32be, s32le, s8, u16be, u16le, u24be, u24le, u32be, u32le, and u8.

|

## InputAudio {#section_dhh_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Channels|String|Yes|Number of source media audio channels.Value range: \[1,8\]

|
|Samplerate|String|Yes|Source media audio sampling rate.-   Value range: \(0, 320000\].
-   Unit: Hz.

|

## AnalysisConfig {#section_lth_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|QualityControl|String|No|Output quality control, which is a JSON object.For more information, see “QualityControl.”

|
|PropertiesControl|String|No|Attribute control, which is a JSON object.For more information, see “PropertiesControl.”

|

## QualityControl {#section_vf3_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|RateQuality|String|No|Output quality level.-   Value range: \(1,51\].
-   The value is an integer.
-   Default value: 25.

|
|MethodStreaming|String|No|Play mode; optional values: network and local.Default value: network

|

## PropertiesControl {#section_it3_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Deinterlace|String|No|Forced scan mode determination.-   Auto: Automatic.
-   Force: Force the Deinterlace action.
-   None: Disable the Deinterlace action.

|
|Crop|String|No|Video cropping configuration.-   Default value: auto
-   The Mode parameter is required if this parameter is set \(not a blank JOSN\{\}\).
-   For more information, see “Crop.”

 |

## Crop {#section_v2j_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Mode|String|No|Value:-   Auto: automatic,
-   Force: force the Crop action,
-   None: disable the Crop action.

This parameter is required if the Crop parameter is set \(not a blank JOSN\{\}\).

|
|Width|Integer|No|Width after cutting.-   Value range: \[8, 4096\].
-   This parameter is invalid if Mode is set to Auto or None.

|
|Height|Integer|No|Height after cropping.-   Value range: \[8, 4096\].
-   This parameter is invalid if Mode is set to Auto or None.

 |
|Top|Integer|No|Top margin for cropping.-   Value range: \[8, 4096\].
-   This parameter is invalid if Mode is set to Auto or None.

 |
|Left|Integer|No|Left margin for cropping.-   Value range: \[8, 4096\].
-   This parameter is invalid if Mode is set to Auto or None.

 |

## TransFeatures {#section_k4j_324_y2b .section}

|TransFeatures|Type|Required|Description|
|:------------|:---|--------|:----------|
|MergeList|String|No|Video merging setting,-   which is formatted as a JSON array.A json array that supports up to four MergeURLs.
-   For more information, see “Merging.”
-   Example: \[\{“MergeURL”:”http://example-bucket.oss-cn-hangzhou.aliyuncs.com/k/mp4.mp4"\},\{"MergeURL":"http://example-bucket.oss-cn-hangzhou.aliyuncs.com/c/ts.ts","Start":"1:14","Duration":"29"\}\]

|

## Merging {#section_nyj_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|MergeURL|String|Yes|Merged part address.-   Example: [http://example-bucket.oss-cn-hangzhou.aliyuncs.com/example-object.flv](http://example-bucket.oss-cn-hangzhou.aliyuncs.com/example-object.flv%EF%BC%8CObject%E9%9C%80%E8%A6%81%E7%BB%8F%E8%BF%87url?spm=a2c4g.11186623.2.12.452f40f7IEM1RZ&file=example-object.flv%EF%BC%8CObject%E9%9C%80%E8%A6%81%E7%BB%8F%E8%BF%87url)
-   The object name must be subject to URL encoding and UTF-8 encoding.

|
|Start|String|No|Start time.-   Format: hh:mm:ss\[. SSS\] or sssss\[. SSS\],
-   Example: 01:59:59.999 or 32000.23

|
|Duration|String|No|Duration.-   Format: hh:mm:ss\[. SSS\] or sssss\[. SSS\],
-   Example: 01:59:59.999 or 32000.23

|

## Task output file {#section_r3k_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|URL|String|No|OSS URL of the input file.-   Example: http://example-bucket.oss-cn-hangzhou.aliyuncs.com/example.flv
-   The Bucket, Location, and Object parameters are required if this parameter is not set.

 |
|Bucket|String|No| -   This parameter is required if the URL parameter is not set.
-   If the URL parameter is set, this parameter is invalid. You must assign the read and write permissions on this bucket to Media Processing on the bucket authorization page in the resource control channel of the console.
-   This parameter complies with the OSS bucket definition. For more information, see the definition of “bucket” in the glossary.

 |
|Location|String|No| -   This parameter is required if the URL parameter is not set.
-   If the URL parameter is set, this parameter is invalid. Data center \(also called OSS location\) where the OSS bucket that stores the output file is located.
-   This parameter complies with the OSS location definition. For more information, see the definition of “location” in the glossary.

 |
|Object|String|No| -   This parameter is required if the URL parameter is not set.
-   If the URL parameter is set, this parameter is invalid. Name of the output file \(an OSS object\), which must be subject to URL encoding and UTF-8 encoding.
-   This parameter complies with the OSS object definition. For more information, see the definition of “object” in the glossary.

 |

## Support for M3U8 custom parameters {#section_atk_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|TS|String|No|Custom parameter support related to TS files. The parameter value is a JSON object.For more information, see “30. TS parameter support.”

|

## TS parameter support {#section_gcl_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Md5Support|Boolean|No|Whether to support TS-specific MD5 value output to M3U8 files.|
|SizeSupport|Boolean|No|Whether to support TS file size output to M3U8 files.|

## Timeline parameters {#section_yll_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Start|String|No|Start time of watermark appearance.-   Unit: seconds
-   Value range: number.
-   Default value: 0.

 |
|Duration|String|No|Duration when the watermark persists. -   Value range: \[number, ToEND\]
-   Default value: ToEND

|

## Encryption parameters {#section_fvl_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Type|String|Yes|Value: hls-aes-128|
|Key|String|Yes|Video encryption key.-   The parameter value must be encrypted using the method indicated by the KeyType parameter.
-   For example, if the key is “encryptionkey128”, it is encrypted into \(“encryptionkey128”\) by Base64 or into \(Base64\(“encryptionkey128”\)\) by KMS.

|
|KeyUri|String|Yes|Key access URL, which is encrypted by Base64|
|KeyType|String|Yes|The encryption key must be encrypted by Base64 or KMS when being transferred to Media Processing.**Note:** If you use KMS, contact us to acquire the primary key. Base64 is the basic encryption mode, whereas KMS performs encryption based on Base64.

|

## SubtitleConfig {#section_o2m_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|ExtSubtitleList|ExtSubtitle\[\]|No|A list of up to four external subtitles, which is a JSON array.-   For more information, see “ ExtSubtitle.”
-   Example: \[\{“Input”:\{“Bucket”:”example-bucket”,“Location”:”oss-cn-hangzhou”,“Object”:”example.srt”\},“CharEnc”:”UTF-8”\}\]

|

## ExtSubtitle {#section_tpm_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Input|String|Yes|External input subtitle file, which is a JSON object.-   The supported formats include SRT and ASS.
-   For more information, see “Input.”
-   Example: \{“Bucket”:”example-bucket”,“Location”:”oss-cn-hangzhou”,“Object”:”example.srt”\}

**Note:** 

-   Currently, \{ObjectPrefix\}, \{FileName\}, and \{ExtName\} can be dynamically replaced.
-   For example, if the input file object for transcoding is a/b/c/test.flv,
-   the subtitle file can be expressed as \{ObjectPrefix\}\{FileName\}-cn.srt based on dynamic rules. URL encoding is required. The Object parameter is set to %7bObjectPrefix%7d%7bFileName%7d-cn.srt. Media Processing considers the path to the external subtitle file address as a/b/c/test-cn.srt.

|
|CharEnc|String|No|External subtitle character encoding.-   Optional values: UTF-8, GBK, BIG5, and Auto.
-   Default value: auto,

**Note:** A check error may occur if this parameter is set to Auto; We recommend that you specify a character encoding method.

|

## Opening {#section_wym_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|OpenUrl|String|Yes|Opening URL, which is an OSS address.|
|Start|String|No|Start time relative to the main video.-   The opening video is displayed after how long starting from 0.
-   Unit: seconds
-   Default value: 0.

|
|Width|String|No|Width.-   Value range: \(0, 4096\).
-   -1, full
    -   -1 indicates the value of the program source,
    -   and “full” indicates filling up the screen.
-   Default value: -1.

|
|Height|String|No|Height-   Value range: \(0, 4096\).
-   -1, full,
    -   -1 indicates the value of the program source,
    -   and “full” indicates filling up the screen.
-   Default value: -1.

|

## TailSlate {#section_p3n_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|TailUrl|String|Yes|Tail slate URL, which is an OSS address.|
|BlendDuration|String|No|The duration of transition from the main video to the ending scene. The effect of transition is fade-in and fade-out: The last frame of the main video is displayed, and the ending scene is played at the same time. The last frame of the main video gradually fades out while the ending scene fades in. Unit: seconds, default value: 0.|
|Width|String|No|Width; optional values: \(0, 4096\), -1, and full. -1 indicates the value of the program source, and “full” indicates filling up the screen. Default value: -1.|
|Height|String|No|High, range \(0,,\),-1, full,-1 represent the value of the source, full indicates the fill screen. The default value is -1.|
|IsMergeAudio|Boolean|No|Whether to merge sample audios. Default value: true.|
|BgColor|String|No|Specifies the background color to fill up the blank when the width or height of the ending scene is smaller than that of the main video. Default color: White. For more information, see [bgcolor](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/29253/cn_zh/1502784952344/color.txt?spm=a2c4g.11186623.2.14.452f40f7IEM1RZ&file=color.txt).|

## Text watermark parameters {#section_e5n_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Content|String|Yes|Text watermark content, which must be Base64 encoded.For example, if you want to add the text watermark “test text watermark”, set this parameter to 5rWL6K+V5paH5a2X5rC05Y2w.

|
|FontName|String|No|Default value: “SimSun”.For more information, see [Supported font](reseller.en-US/API Reference/Font name.md#).

|
|FontSize|Int|No|Font size.-   Default value: 16.
-   Value range: \(4,120\).

|
|FontColor|String|No|Font color.For more information about the optional values, see [FontColor](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/29253/cn_zh/1502784952344/color.txt?spm=a2c4g.11186623.2.16.452f40f7IEM1RZ&file=color.txt).

|
|FontAlpha|Int|No|Font transparency.-   Value range: \(0, 1\].
-   Default value: 1.0

|
|Top|Int|No|Top margin of the text.-   Default value: 0.
-   Value range: \[8, 4096\].

|
|Left|Int|No|Left margin of text.-   Default value: 0
-   Value range: \[8, 4096\].

|
|BorderWidth|Int|No|Stroke width.-   Default value: 0
-   Value range: \[8, 4096\].

|
|BorderColor|String|No|Stroke color.-   Default value: Black
-   For more information about the optional values, see [BorderColor](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/29253/cn_zh/1502784952344/color.txt?spm=a2c4g.11186623.2.17.452f40f7IEM1RZ&file=color.txt).

|

## Screenshot OutputFile {#section_td4_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Bucket|String|Yes|OSS bucket that stores the output screenshot file.This parameter complies with the OSS bucket definition. For more information, see the definition of “bucket” in the glossary.

|
|Location|String|Yes|Data center \(also called OSS location\) where the OSS bucket that stores the output screenshot file is located.This parameter complies with the OSS location definition. For more information, see the definition of “location” in the glossary.

|
|Object|String|Yes|Name of the output screenshot file \(an OSS object\).-   JPG format, which must be subject to URL encoding and UTF-8 encoding.

Example of placeholder replacement: If the input screenshot file is a/b/c.flv and Object is set to %7BObjectPrefix%7D%7BFileName%7D%7BCount%7D.jpg, then the output screenshot files are a/b/c00001.jpg, a/b/c00002.jpg, and so on.The placeholder replacement rules are applicable to output screenshot file naming.

-   The following placeholders are supported by workflows: \{ObjectPrefix\} indicates the prefix of the input file name; \{FileName\}, the input file name; \{ExtName\}, the input file name extension; \{SnapshotTime\}, the screenshot taking time; \{Count\}, a specific screenshot in a batch of screenshot files; \{RunId\}, the ID of a media workflow execution instance; and \{MediaId\}, the ID of the media file processed by a workflow. These placeholders can be replaced dynamically.
-   The following placeholders are supported by non-workflows: \{ObjectPrefix\} indicates the prefix of the input file name; \{FileName\}, the input file name; \{ExtName\}, the input file name extension; \{SnapshotTime\}, the screenshot taking time; \{Count\}, a specific screenshot in a batch of screenshot files.

Batch screenshot taking: If screenshots are taken in sequence asynchronously and Num is not set to 1, then Object of OutputFile must contain %7BCount%7D to identify the addresses of multiple screenshot images that are taken in sequence. If three screenshot images are output and Object of OutputFile is %7BCount%7D.jpg, then the output images \(indicated by Object\) are 00001.jpg, 00002.jpg, and 00003.jpg in sequence.

|

## TileOut {#section_j44_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Lines|String|No|Picture-tiling lines.-   Integer.
-   Value range: \(0, 1,000\]
-   Default value: 10

 |
|Columns|String|No|Picture-tiling columns.-   Integer.
-   Value range: \(0, 1,000\]
-   Default value: 10.

 |
|CellWidth|String|No|The width of a single picture.The width of the screenshot output resolution by default.

|
|CellHeight|String|No|The height of a single picture.The height of the screenshot output resolution by default.

|
|Margin|String|No|The width of the margin.-   Default value: 0.
-   Unit: Px.

|
|Padding|String|No|The picture space, default value: 0, unit: px.|
|Color|String|No|Background color.-   Value range: color keyword, random.
-   Default value: Black.
-   Color keyword supports three formats. For example, for black, “Black”, “black” and “\#000000” are supported.

|
|IsKeepCellPic|String|No|Whether the picture is kept.-   Value range: true, false.
-   Default value: true.

|

## MultiBitrateVideoStream {#section_uy4_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|URI|String|No|The output name of the video bitstream, which must end with .m3u8. For example, a/b/test.m3u8, format: ^\[a-z\]\{1\}\[a-z0-9. /-\]+$|

## ExtXMedia {#section_q3p_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Name|String|Yes|Required, description, corresponding to NAME of HLS V5 protocol, 64 bytes at most, UTF-8.|
|Language|String|No|Optional, language type, RFC5646, corresponding to LANGUAGE of HLS V5 protocol.|
|URI|String|Yes|Required, resource path.Example: a/b/c/d/audio-1.m3u8, Format: ^\[a-z\]\{1\}\[a-z0-9. /-\]+$

|

## MasterPlayList {#section_ctp_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|MultiBitrateVideoStreams|JsonArray|Yes|Multi-bitstream array.-   For more information, see MultiBitrateVideoStream.

Example: \[\{“RefActivityName”: “video-1”,”ExtXStreamInfo”: \{“BandWidth”: “111110”,”Audio”: “auds”,”Subtitles”: “subs” \}\}\]|

## MultiBitrateVideoStream {#section_pdq_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|RefActivityName|String|Yes|The name of the associated activity.|
|ExtXStreamInfo|Json|Yes|The bitstream feature.-   For more information, see ExtXStreamInfo.
-   Example: \{“BandWidth”: “111110”,”Audio”: “auds”,”Subtitles”: “subs” \}

|

## ExtXStreamInfo {#section_zsq_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|BandWidth|String|Yes|Bandwidth.The upper limit of the total bitrate, required, which corresponds to BANDWIDTH of HLS V5 protocol.

|
|Audio|String|No|The ID of the audio streams group.Optional, which corresponds to AUDIO of HLS V5 protocol.

|
|Subtitles|String|No|The ID of the subtitile stream groups.Optional, which corresponds to SUBTITLES of HLS V5 protocol.

|

## SubOut Webvtt {#section_zfr_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|IsSptFrag|String|No|Whether the picture is tiled out.-   True indicates tiling out.
-   Default value: false.

|

## DeWatermark {#section_jsr_324_y2b .section}

JSON:

```
"0": [
        {
            "L": 10,
            "T": 10,
            "W": 10,
            "H": 10
        },
        {
            "L": 100,
            "T": 0.1,
            "W": 10,
            "H": 10
        }
    ],
    "128000": [],
    "250000": [
        {
            "L": 0.2,
            "T": 0.1,
            "W": 0.01,
            "H": 0.05
        }
    ]
}
```

pts: Character, indicating the timestamp of object frame. Unit: millisecond \(s\).

-   L: Number, indicating the left margin of the region to be blurred.
-   T: Number, indicating the top margin of the region to be blurred.
-   W: Number, indicating the width of the region to be blurred.
-   H: Number, indicating the height of the region to be blurred.

When values of T, L, W and H are larger than one, they indicate absolute pixel value. Otherwise, they indicates percentage values corresponding to source video resolution. Whether the values of T, L, W and H are percentage values or absolute values, they are rounded down in the final treatment.

In the previous demo, the corresponding descriptions of the pts（0, 128000, 250000）are as follows:

-   Starting from 0ms, the system performs dewatermarking treatment on the Logo which is 10✖️10 pixel in size and 10X10 pixel from the upper-left corner, as well as on the Logo which is 10X10 pixel in size and has a left margin of 100 pixel and top margin of 0.1✖️\(src\_height\).
-   Until 128000ms, the system doesnot stop performing dewatermarking treatment on the Logo, that is, \[0~128000\] is the time range when the Logo is blurred.
-   Starting from 250000ms, the system performs dewatermarking treatment on the Logo which is 0.01✖️\(src\_width\) in width, 0.05✖️\(src\_height\) in height, and has a left margin of 0.2✖️\(src\_width\) and top margin of 0.1✖️\(src\_height\).

## AdaptationSet {#section_rhs_324_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Group|String|Yes|Required, group name, as in Dash File:```
<AdaptationSet group="videostreams" mimeType="video/mp4" par="4096:1744"
              minBandwidth="258157" maxBandwidth="10285391" minWidth="426" maxWidth="4096"
              minHeight="180" maxHeight="1744" segmentAlignment="true"
              startWithSAP="1">
```

|
|Lang|String|No|Language.Can be set in audio and subtitle activity.

|

## Representation {#section_h4c_vxp_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Id|String|Yes|Required, flow ID, as in Dash File:```
<Representation id="240p250kbps" frameRate="24" bandwidth="258157"
              codecs="avc1.4d400d" width="426" height="180">
```

|
|URI|String|Yes|Required, resource path.Example: a/b/c/d/video-1.mpd，格式：^\[a-z\]\{1\}\[a-z0-9. /-\]+$

|

## InputConfig {#section_itd_vxp_y2b .section}

|Parameter|Type|Required|Description|
|:--------|:---|--------|:----------|
|Format|String|Yes|Required, the input format of the subtitle file.Supports stl, ttml, and vtt formats.

|
|InputFile|String|Yes| ```
{"Bucket":"example-bucket","Location":"oss-cn-hangzhou","Object":"example-logo.png"}
              Or
              {"URL":"http://bucketname.oss-cn-hangzhou.aliyuncs.com/subtitle/test.chs.vtt"}
```

 |

## Volume {#section_hv4_k3t_qfb .section}

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Method|String|No|Volume regulation mode.Optional value: auto, dynamic, linear.

|
|IntegratedLoudnessTarget|String|No|Target volume, number.-   Value range: \[-70, -5\]
-   You must specify Method as dynamic.
-   Default value: -6

|
|TruePeak|String|No|Maximum peak value, number.-   Value range: \[-9, 0\]
-   You must specify Method as dynamic.
-   Default value: -1

|
|LoudnessRangeTarget|String|No|Volume range, number.-   Value range: \[1, 20\]
-   You must specify Method as dynamic.
-   Default value: 8

|

## Amix {#section_wwh_nps_sfb .section}

|Parameters|Type|Required|Description|
|:---------|:---|:-------|:----------|
|AmixURL|String|Yes|Background audio track media that needs audio mixing. Value: OSS URL or character string "input".

input scenario: to mix two audio tracks of a video stream.

|
|Map|String|Yes|Select target audio tracks from AmixURL. The value is : 0:a:\{audio\_index\}. Example: 0:a:0.|
|MixDurMode|String|No|Value: first, long.-   first: indicates the time duration of the output media is subject to the time duration of the input media.
-   long: indicates that the time duration of the output media is subject to the media which has longer time duration.
-   Default value: long

|

