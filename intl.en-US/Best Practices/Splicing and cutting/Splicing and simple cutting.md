# Splicing and simple cutting {#concept_p2j_hvl_x2b .concept}

Splicing refers to the process of splicing multiple videos of different formats, encoding, and resolutions and outputting a new video with the same format, encoding methods, and resolution. This function is often used to add fixed titles and credits and splice live broadcast videos.

Cutting refers to the process where you extract a certain clip of a video and output into a new video. This function is often used to extract the highlights or essential contents of videos.

## Parameter description {#section_mqd_svl_x2b .section}

When splicing a video, you need to take note of the following parameters:

[Input](https://help.aliyun.com/document_detail/29253.html#h2-19-15)

Specifies an OSS input file for the title.

**Note:** The location of OSS must correspond to the region of MPS. For example, oss-cn-hangzhou location of OSS corresponds to cn-hangzhou region of MPS.

Set the following parameters in [Output:](https://help.aliyun.com/document_detail/29253.html#h2-2-output-2):

-   [Video](https://help.aliyun.com/document_detail/29253.html#h2-8-video-8)

    Specifies the width, height, and bit rate of the final output video. If the width and height of multiple clips \(including titles and credits\) are inconsistent with those of the final video, the margins will be automatically filled with black. We recommend that you prepare titles and credits of different widths and heights based on the actual resolutions of different jobs to create a better video.

-   [MergeList](https://help.aliyun.com/document_detail/29253.html#h2-27-23)

    The list order is the splicing order. The last item of the list is the credits. You can splice up to five videos \(including the title and credits\) into one. You can use the `MergeConfigUrl` parameter to splice more videos together.

    **Note:** `MergeLsit` and `MergeConfigUrl` are mutually exclusive. You can specify only one of them.

    Each spliced video has three parameters:

    -   MergeURL

        Specifies the OSS URL of a splicing video.

        **Note:** The OSS region of the video that you splice must be consistent with that of the title. Videos from different regions cannot be spliced.

    -   Start

        When you splice videos, you can specify a start point to extract a desired clip for the final video. The default value is 0.

    -   Duration

        When you splice videos, you can specify a duration \(with the start point as the value of Start\) to extract a desired clip for the final video. The default duration is from Start to the end of the video.

-   MergeConfigUrl

    Specifies the OSS URL of the configuration file of the videos that you are splicing. The content of the configuration file is a JSON object, with the same value of [MergeList](https://help.aliyun.com/document_detail/29253.html#h2-27-23).

    The list order is the splicing order. The last item of the list is the credits. You can splice up to 100 clips \(including the title and credits\) into one.


## Code examples {#section_r5p_szl_x2b .section}

You can splice a `720P(1280x720)` video with the `480P(640x480)` title and credit in MP4 format. The resolution of the output video is `1280x720`. When you play the output video, black borders are displayed on the left and right sides of the title and credit. However, the video is normally displayed.

Code example details:

-   [Splicing and simple cutting-Java SDKPanels and simple clips-Java SDK](https://help.aliyun.com/document_detail/85509.html)

-   [Splicing and simple cutting-Python SDK](https://help.aliyun.com/document_detail/85512.html)

-   [Splicing and simple cutting-PHP SDK](https://help.aliyun.com/document_detail/85514.html)


