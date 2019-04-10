# How do I add a watermark? {#concept_qjv_ypl_x2b .concept}

Watermarks refer to the process of adding related information \(such as a corporate logo, TV station logo, and user nickname\) to a video. Watermarks can highlight brands, protect copyrights, and increase product recognition. MPS supports three watermark types: **image watermarks**, **animated watermarks** and **text watermarks.**. You can select a type based on your needs.

## Type {#section_kyz_bql_x2b .section}

-   **Image watermarks**: You can use a PNG image as the watermark. The image is displayed at a fixed position on the video. You can specify the display time \(from the beginning to the end or in a certain duration\).

-   **Animated watermark**: You can use an animated graphic in APNG format or a video in MOV format as the watermark. The animation is displayed repeatedly at a fixed position on the video.

-   **Text watermark**: You can use texts as the watermark. You can specify the font, size, and color of the texts and add different texts to different videos.


## Parameter description {#section_rzd_2ql_x2b .section}

When submitting transcoding tasks \(see [Simple transcoding](intl.en-US/Best Practices/Transcoding/How do I perform simple transcoding?.md#)\), you can specify a watermark template and material to add watermark information for the output video.

You can specify several [WaterMark](../../../../../intl.en-US/API Reference/Appendix/Parameter details.md#) objects for each transcoding task. A WaterMark object contains the following parameters:

-   WaterMarkTemplateId \(watermark template ID\)

    A watermark template contains common parameters such as Type, ReferPos, Width, Height, Dx, and Dy.

    You can create a template on the Media Processing console. For more information, see [Watermark transcoding template](../../../../../intl.en-US/User Guide/Settings.md#).

    **Note:** The parameters in WaterMark objects have a higher priority than the corresponding parameters in the template. The parameters in WaterMark objects overwrite those parameters in the template.

-   Type \(watermark type\)

    When adding image or animated watermarks, you can set Type to Image and specify InputFile, which is the OSS file path of the watermark materials.

    When adding text watermarks, you can set Type to Text and specify the [TextWaterMark](../../../../../intl.en-US/API Reference/Appendix/Parameter details.md#) parameter, including text font, size, color, and transparency.

-   ReferPos \(watermark position\)

    The reference position where a watermark is displayed. Dx and Dy are calculated based on ReferPos. See [Watermark template configuration](../../../../../intl.en-US/API Reference/Appendix/Parameter details.md#).

    Watermark coordinate description:

    ![](images/10135_en-US.png)

-   Width, Height, Dx, and Dy

    Specify the width, height, horizontal offset, and vertical offset of a watermark. The values can be calculated in the following two ways:

    -   Absolute value:

        Units: pixels. Value range: \[8,4096\].

    -   Relative scale:

        The width and height relative to the output video resolution. Value range: \(0, 1\). Up to four digits are allowed after the decimal point, for example, 0.9999.

    -   Default value:

        -   The default value is 0 when Dx and Dy are not set.

        -   When neither Width nor Height is set, the watermark width is 0.12 times the resolution width of the output video. The watermark height scales proportionally according to the aspect ratio of the original watermark image.

        -   When either Width or Height is set, the unspecified parameter scales proportionally based on the aspect ratio of the original watermark image.

        -   When both Width and Height are set, the watermark image is set based on the specified values.

-   InputFile \(input file\)

    Specifies the OSS file location of an image or animated watermark. Images in PNG format and animations in MOV and APNG formats can be used as watermarks.

    **Note:** The file extension of an animated watermark must be mov or apng in lowercase. File extensions of images are not limited.

-   [TextWaterMark](../../../../../intl.en-US/API Reference/Appendix/Parameter details.md#) \(text watermark\)

    Specifies the detailed parameters of text watermarks.

    **Note:** The reference position and relative scale cannot be set for text watermarks. You can specify the upper-left corner as the reference position and specify Dx and Dy offsets according to the absolute values.


## Scenarios {#section_p4n_zql_x2b .section}

Short videos

In this scenario, you can add an image watermark \(product logo\) and a text watermark \(user ID\) to downloaded or shared short videos to protect copyright.

Example:

![](images/10136_en-US.png)

Audio and video websites

For audio and video websites, you can add brand logos to videos to demonstrate copyright ownership. Additionally, you can also add stickers to videos of entertainment programs to make the programs more interesting or increase advertisement exposure.

Example:

![](images/10137_en-US.png)

## Code example {#section_xbk_grl_x2b .section}

When transcoding to a `720P(1280x720)` in MP4 format, you can add three watermarks at the same time and specify parameters for all three.

-   Image watermark

    You can specify the upper-right corner as the reference position and set the relative scale of the image watermark width to 0.05 times the resolution width of the output video. The watermark height scales proportionally based on the aspect ratio of the original watermark image.

-   Text watermark

    You can specify the upper-left corner as the reference position and set the text to `Test text watermark`. You can specify the text font information such as typeface to SimSun, font size to 16, color to red, and transparency to 50. The text will be displayed in the video based on the specified information.

-   Animated watermark

    You can specify the lower-left corner as the reference position and add an MOV video as the watermark. You can set the height of the video to 240 pixels. The width of the video scales proportionally according to the aspect ratio of the original watermark video.


Code examples:

-   [Watermarks-Java SDK](../../../../../intl.en-US/SDK Reference/Transcoding SDKs/Java SDK/Watermarks.md#)

-   [Watermarks-Python SDK](../../../../../intl.en-US/SDK Reference/Transcoding SDKs/Python SDK/Watermarks.md#)

-   [Watermarks-PHP SDK](../../../../../intl.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Watermarks.md#)


