# How do I set the opening and ending scenes? {#concept_glz_vzl_x2b .concept}

Video opening and ending scenes refer to a special effect of splicing: embedding the scenes in a video as picture-in-picture.

## Parameter description {#section_vdk_yzl_x2b .section}

When you embed the opening and ending scenes, you need to take note of the following parameters:

[Input](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

Specifies an OSS input file for the video.

**Note:** The location of OSS must correspond to the region of MPS. For example, oss-cn-hangzhou location of OSS corresponds to cn-hangzhou region of MPS.

Set the following parameters in [Output](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#):

-   [Video](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

    Specifies the width, height, and bit rate of the final output video. When the width and height of the video are inconsistent with those of the final output, the video will be stretched automatically. We recommend that you specify either the width or height. The unspecified side will be scaled based on the original aspect ratio of the video.

-   [Opening](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

    The order of the opening scene list is the splicing order. You can add up to two opening scenes.

    Each opening scene contains four parameters:

    -   OpenUrl

        Specifies the OSS URL of an opening scene.

        **Note:** The OSS region of an opening scene must be consistent with that of the video you plan to splice it with. Videos from different regions cannot be spliced.

    -   Start

        Specifies the time when the opening scene starts to play after the start of the video. The default value is 0 seconds.

    -   Width

        Specifies the width of an opening scene. Two special values of the parameter:

        -   `-1` indicates that the width is equal to that of the opening scene source;

        -   `full` indicates that the video screen is filled up.

        -   You can specify other values. Value range: \(0, 4096\].

            **Note:** The scene is aligned to the center of the video. We recommend that you do not set the width of an ending scene to be greater than that of the video to avoid any problems.

    -   Height

        Specifies the height of an opening scene. Two special values of the parameter:

        -   `-1` indicates that the height is equal to that of the opening scene source;

        -   `full` indicates that the video screen is filled up.

        -   You can specify other values. Value range: \(0, 4096\].

            **Note:** The scene is aligned to the center of the video. We recommend that you do not set the height of an opening scene to be greater than that of the video to avoid any problems.

-   [TailSlate](../../../../reseller.en-US/API Reference/Appendix/Parameter details.md#)

    The order of the ending scene order list is the splicing order. You can add up to two ending scenes.

    Each ending scene contains the following parameters:

    -   TailUrl

        Specifies the OSS URL of an ending scene.

        **Note:** The OSS region of an ending scene must be consistent with that of the video you plan to splice it with. Videos from different regions cannot be spliced.

    -   Width

        Specifies the width of an ending scene. Two special values of the parameter:

        -   `-1` ndicates that the width is equal to that of the ending scene source;

        -   `full` indicates that the video screen is filled up.

        -   You can specify other values. Value range: \(0, 4096\].

            **Note:** The scene is aligned to the center of the video. We recommend that you do not set the width of an ending scene to be greater than that of the video to avoid any problems.

    -   Height

        Specifies the height of an ending scene. Two special values of the parameter:

        -   `-1` indicates that the height equals to that of the ending scene source;

        -   `full` indicates that the video screen is filled up.

        -   You can specify other values. Value range: \(0, 4096\].

            **Note:** The scene is aligned to the center of the video. We recommend that you do not set the height of an ending scene to be greater than that of the video to avoid any problems.

    -   BlendDuration

        The duration of transition from the video to the ending scene. The effect of transition is fade-in and fade-out: The last frame of the video and the ending scene start playing at the same time. The last frame of the video gradually fades out while the ending scene fades in. The default value is 0 seconds.

    -   IsMergeAudio

        Specifies whether to splice the audio in the ending scene or not.

    -   BgColor

        Specifies the background color that fills up the margin when the width or height is smaller than that of the video.


## Code example {#section_occ_j1m_x2b .section}

You can splice a `720P (1280x720)` video with the `480P (640x480)` opening and ending scenes in MP4 format. You can set the start time of the opening scene to 2 seconds, the transition time of the ending scene to 3 seconds, and the background color to `Black`. The opening scene starts to play two seconds into the video. The opening scene is centered in the video and plays simultaneously with the video. The ending scene fades in and out at the end of the video.

Code example:

-   [Opening and ending scenes-Java SDK](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Java SDK/Splicing-opening and ending scenes.md#)

-   [Opening and ending scene-Python SDK](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Python SDK/Splicing-opening and ending scenes.md#)

-   [Opening and ending scene-PHP SDK](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Splicing-opening and ending scenes.md#)


