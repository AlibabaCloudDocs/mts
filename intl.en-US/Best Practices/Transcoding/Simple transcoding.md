# Simple transcoding {#concept_nmj_vfg_x2b .concept}

## Introduction {#section_vrj_xfg_x2b .section}

Transcoding refers to the process to process an OSS input file according to specified parameters, and output the result to specified OSS file. When submitting a [transcoding task](../../../../reseller.en-US/Developer Guide/Concepts/Task and MPS queue.md#), note the following objects:

-   [Input](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

    Specify an OSS input file.

    **Note:** The Location of OSS must correspond to the region of MPS. For example, the oss-cn-hangzhou of OSScorresponds to the cn-hangzhou of MPS.

-   [Output](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

    Several output objects can be specified for each transcoding task, which includes multiple parameters and subobjects. Three important parameters and subobjects are introduced as follows:

    -   [Container](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

        The output container type \(file format\). The video supports mp4, flv, ts, and m3u8, and the audio supports mp3 and mp4.

    -   [Video](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

        The output video parameter, for example, the codec format, bitrate, width, height, and frame rate.

    -   [Audio](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

        The output audio parameter, for example, the audio codec forma, bitrate, channels, and samplerate.

    -   TemplateId

        Parameters specified through API have higher priority than parameters set by templates, and overwrite the corrosponding parameters set in the templates.

        MPS provides [Preset static templates](../../../../reseller.en-US/API Reference/Appendix/Preset template details.md#).

        Also, you can [Custom transcoding template](../../../../reseller.en-US/User Guide/Settings.md#).


-   PipelineId

    Each region provides an MPS queue. You can log on to the [MPS console](https://partners-intl.aliyun.com/login-required#/mts), click **Library** \> **Settings** \> **MPS queue** to query.


## Scenarios {#section_c31_ggg_x2b .section}

The video in any format is transcoded to MP4 video file with the definition `720P (1280x720)`, and the audio and video parameters are set as follows:

-   Video

    H. 264 coder is used, the bitrate is 1500Kbps, the width is 1280, the height is adaptive \(to avoid the picture is scaled out of proportion due to a fixed height value\), and the frame rate value is 25.

-   Audio

    AAC encoder is used, the bit rate is 128Kbps, the channels are 2 and the samplerate is 44100.

-   Transcoding template

    The preset static template “MP4-fluent” is used: S00000001-200010, the video bitrate set in the template is 400Kbps, the audio bit rate is 64Kbps, and the width is 640 \(The height is adaptive\).

-   Output result

    The API parameters overwrite the template parameters, therefore, in the output video, the bitrate is 1500Kbps, the width is 1280, the fram rate is 25, and in the output audio, the bitrate is 128Kps, the channels are 2, adn the samplerate is 44100.


## Example code {#section_x4f_3gg_x2b .section}

[Simple transcoding-Java](../../../../reseller.en-US//Java SDK/Transcoding.md#)

[Simple transcoding-Python](../../../../reseller.en-US//Python SDK/Transcoding.md#)

[Simple transcoding-PHP](../../../../reseller.en-US//PHP SDK/Transcoding.md#)

