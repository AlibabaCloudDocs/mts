# Functions and features

Media Processing \(MPS\) is a service that converts an audio/video file into another or multiple audio/video files. It helps you to produce videos that are suitable for different bandwidths, terminal devices, and user demands. On the basis of deep learning of large amounts of data, it performs multi-model analysis based on the content, text, audio, scenario of audio/video files; it is able to intelligently detect, understand, and edit content.

You can use MPS for:

-   Terminal device adaptation: You can convert audio/video formats to achieve media playback on different devices, such as PCs, TVs, and mobile devices.

-   Network environment adaptation: You can perform video transcoding to convert videos to different definitions, such as standard, high, and ultra high. Users can choose a suitable definition based on their bandwidth and have smooth playback.

-   Watermarks: You can add watermarks to videos to highlight brands, protect copyrights, and increase product recognition. Watermarks can be a corporate logo, TV station logo, or uploader nickname.

-   Screenshots: You can take screenshots at a specified time. You can use the screenshots as video covers or to generate image sprites.

-   Video editing: You can produce new videos by cutting and splicing videos.

-   Digital restoration: You can refine the image blur or mosaic in poor-quality videos to produce high-definition videos.

-   Reduction of storage and distribution costs: You can adjust video bit rates, improve video compression efficiency, and reduce file sizes while ensuring the same image quality. This reduces playback and saves storage space and traffic.

-   Video deduplication and original content recognition: You can extract the fingerprints in images and audio of a video to generate video fingerprints. This function enables you to detect duplicate videos and trace the sources of duplicate video clips. The function is applicable to scenarios such as video deduplication, copyright infringement filtering, original content recognition, and video source tracing.

-   Video detection: This function supports intelligent detection of sexual, violent, terrorism-related, and politically sensitive videos. It saves costs of manual review and reduces risks of potential violations.

-   Digital improvement and conversion: This function helps you to pick out optimal key frames based on the understanding of video contents, aesthetic of pictures, and large amounts of user behavior data. You can use the key frames to generate images, animated images, or short videos, which can be used as video covers to help increase the number of views.


## Transcoding

Encapsulation format

|Parameter|Description|
|:--------|:----------|
|Input format|-   Container formats: 3GP, AVI, FLV, MP4, M3U8, MPG, ASF, WMV, MKV, MOV, TS, WebM, and MXF.
-   Video encoding formats: H. 264/AVC, H. 263, H. 263+, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, Quicktime, RealVideo, and Windows Media Video.
-   Audio encoding formats: AAC, AC-3, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, and Windows Media Audio. |
|Output format|-   Container formats:
    -   Video: FLV, MP4, HLS\(m3u8+ts\), MPEG-DASH\(MPD+fMP4\)
    -   Audio: MP3, MP4, OGG, FLAC, and m4a.
    -   Image: GIF and WEBP.

-   Video encoding formats: H. 264/AVC and H. 265/HEVC.

-   Audio encoding formats: MP3, AAC, VORBIS, and FLAC. |
|Audio extraction|Isolates the audio from a video file, which means the video is disabled.|
|Video extraction|Isolates the video from a video file, which means the audio is disabled.|
|Encapsulation|Changes the encapsulation format of a video but not the encoding method. Audio files can be encapsulated into MP4, M3U8, and FLV formats.|
|Conversion from videos to animated images|Outputs highlight contents in a video into animated images in GIF or WEBP format for display.|

Video encoding parameters

|Parameter|Description|
|:--------|:----------|
|Codec|Encoding/Decoding formats.-   Supported formats: H. 264, H. 265, GIF, and WEBP.

-   default value: H. 264. |
|Bitrate|Bit rate.-   Supported output bit rate range: \[10,50000\].

-   Unit: kbps. |
|Fps|Frame Rate.-   The default value is the frame rate of the input file. If the frame rate of the input file is greater than 60, the value is still 60.

-   Value range: \(0, 60\].

-   Unit: fps. |
|Width\* Height|Resolution.-   Width:
    -   The default value is the original video width.
    -   Value range: \[128,4096\].
    -   Unit: pixel.

-   Height:
    -   Default: Video height.
    -   Value range: \[128,4096\].
    -   Unit: px. |
|Scale|Automatic scaling. Allows proportional scaling of a file according to Width.Allows proportional scaling of a file according to Height.|
|GOP|Maximum time interval between two key frames or maximum number of frames.-   Maximum time interval between two key frames: the unit of the value must be included for transmission. Unit: seconds. Default value: 10 seconds.
-   Maximum number of frames: no unit. Value range: \[1, 100000\]. |
|Profile|Encoding level. H. H.264: Supported encoding levels include Baseline, Main, and High.|
|PixFmt|Video color format.-   Values: yuv420p, yuvj420p, and other standard color formats.
-   Default value: yuv420p or original color format. |
|Rotate|Video rotation angle. The video rotation is clockwise.-   Value range: \[0,360\).

-   Default value: 0. |

Video processing parameters

|Parameter|Description|
|:--------|:----------|
|ScanMode|Scan mode. Optional values: interlaced and progressive.|
|RateControlModes|Bit rate control method. The bit rate control methods that are supported: VBR, CBR, and CRF.|
|Crop|Video cropping. Allows automatically detecting and cropping black borders; allows user-defined cropping.|
|Pad|Pad a video with black borders is supported .|

Audio encoding parameters

|Parameter|Description|
|:--------|:----------|
|Codec|Encoding/Decoding formats.-   Audio codec format: AAC, MP3, VORBIS, and FLAC.
-   Default value: AAC. |
|Samplerate|Sampling rate.-   Default value: 44100.
-   Optional values: 22050, 32000, 44100, 48000, and 96000.
-   Unit: Hz.
-   When the video container format is FLV and the audio codec format is MP3, Samplerate cannot be set to 32000, 48000, or 96000.
-   When the audio codec format is MP3, Samplerate cannot be set to 96000. |
|Bitrate|Audio bit rate.-   Default value: 128.
-   Rate range: \[8,1000\].
-   Unit: Kbps. |
|Channels|Number of sound channels.-   Default value: 2.
-   It can be set to either 1 or 2 when Codec is set to MP3.
-   It can be set to 1, 2, 4, 5, 6, or 8 when Codec is set to AAC. |

Transcoding control

|Category|Description|
|:-------|:----------|
|HLS MasterPlayList|Generates a Master Playlist file by combining multiple subtitles, sound tracks, and video streams of multiple bit rates.|
|Conditional transcoding|Two methods are supported:-   When the bit rate \(or resolution\) of the transcoding template is greater than that of the input video, the video will not be transcoded.
-   When the bit rate \(or resolution\) in the transcoding template is greater than that of the input video, the output bit rate \(or resolution\) will be the same as that of the input video. |
|Workflow|Cloud-based automated processing workflows. The workflows are used to automatically process audio and video files after the files are uploaded.|

## Transcoding templates

Preset templates

MPS allows you to preset a series of transcoding templates for output videos to adapt to certain bandwidth conditions.

-   Preset smart templates

    This function automatically adjusts the transcoding parameters based on the input video to suit the output video requirements. Because input videos vary widely from each other \(in terms such as resolution and bit rate\), not all preset smart templates are suitable for all input files. You must use a template analysis task to locate the preset templates suitable for a specific input file. When you perform multimedia transcoding, reduce the file size \(lower the bit rate\) as much as possible while minimizing quality loss. Preset smart templates give priority to quality.

-   Preset static templates

    You can call these templates without performing template analysis. Three types of static templates are video transcoding templates, audio MP3 transcoding templates, and encapsulation templates. These templates are suitable for normal media player devices and bandwidth conditions. The templates give priority to bit rate reduction.

-   Preset narrowband HDTM templates

    You can call these templates without performing template analysis. These templates provide three output formats: FLV, MP4, and M3U8. The preset narrowband HDTM templates are a type of transcoding template unique to Alibaba Cloud MPS. They provide transcoding to even lower bit rates while maintaining the same video definition as normal transcoding templates, which helps lower costs even more.


Custom templates

These presets are created from user-defined transcoding parameters. These collections of transcoding parameters \(such as for audio, video, and containers\) can satisfy your individualized transcoding needs.

## Editing

|Category|Description|
|:-------|:----------|
|Video cutting|Allows you to extract a media clip of a specified duration from a specified start point|
|Video splicing|Allows you to splice up to 20 videos|
|Video blurring|Allows you to blur a specific area of a video|
|Opening and ending scenes|-   Allows you to add dynamic logos at the beginning of a video and specify the contents of the end credits.
-   Scenes help increase product recognition and protect your copyright. |

## Watermarks

|Category|Description|
|:-------|:----------|
|Static watermark|-   Allows you to add a maximum of 20 static watermarks to an output video.
-   The watermarks can be in the PNG, TEXT, MOV, and APNG formats. |
|Dynamic watermark|Allows you to set the time when the watermarks are displayed.|

## Screenshots

|Category|Description|
|:-------|:----------|
|Video screenshot|-   Allows you to take screenshots in JPG format at a specified time of a video file stored in OSS.
-   You can take a single screenshot, multiple screenshots, and average screenshots. |
|Image sprite/WebVTT thumbnail|Allows you to generate image sprites by capturing a series of images. Information about multiple images can be requested at one time, which reduces the number of image requests and improves client performance.|
|Smart cover pictures|Helps you to pick out optimal key frames as video cover pictures based on the understanding of video contents and aesthetic of pictures|

## Narrowband HDTM

|Category|Description|
|:-------|:----------|
|Narrowband HDTM1.0|Based on the proprietary transcoding technology of Alibaba Cloud, it intelligently analyzes each scene, action, content, and texture of a video to lower the bit rate while keeping the same video quality, effectively lowering bandwidth costs.|
|Narrowband HDTM2.0|-   Modeled based on human visual system models, this function helps encoders emphasize user experience over fidelity when the encoders perform video optimization.
-   Because of the unique algorithm applied in this function, it performs better than current video encoders and enhances video clarity at lower bit rates. |

## Digital restoration

|Category|Description|
|:-------|:----------|
|Frame rate conversion \(FRC\) service|For HD videos at or below 30 frames/second, this function allows you to generate high frame rate versions of 60 frames/second or even 120 frames/second. Streaming quality is not affected even on a large 4K screen.|
|Video source repair \(PicRescue\)|For over-compressed online videos, this function allows you to remove the blurs and mosaics from the screen, and generate a restored version of higher definition|
|SD to HD conversion service \(SD to HD\)|For classic films of standard definition, this function allows you to remove film granules and compression noise and use ultra-resolution technology to generate HD versions of 720p or even 1080p|
|2k to 4k conversion service \(2k to 4k\)|For 1080p films, this function allows you to generate an exclusive 4k content source of high-quality. The function is based on the super definition technology that uses a large quantity of videos|

## High speed transcoding

For long videos over 30 minutes, this function improves the speed of transcoding significantly by splitting the videos for parallel transcoding. Transcoding can be up to five times faster.

## More

|Category|Description|
|:-------|:----------|
|Media information|This function enables you to get the encoding and content information about audio and video files stored in OSS.|
|Custom duration of M3U8 output slices|-   This function enables you to customize the M3U8 slice duration, from 1 second to 60 seconds.
-   This helps you to determine the slice duration based on the bandwidth conditions to reduce loading time for the first screen. |
|External subtitle import|This function allows you to import external subtitle files and specify the subtitle encoding format.|
|Notification integration|-   This function integrates the MNS service.
-   After the notification attributes for an MTS queue are set, the messages returned by asynchronous interfaces for transcoding tasks in the MTS queue are actively pushed to your message receiving service by the MNS service. |
|Playback|-   This function provides a Web player that supports Flash, HTML5, and adaptive mode.
-   It also provides mobile player SDKs for iOS and Android. |

