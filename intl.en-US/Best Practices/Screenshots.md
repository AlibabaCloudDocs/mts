# Screenshots {#concept_qqs_mrl_x2b .concept}

Screenshots refer to the process where an image captured at a specified time in a video is saved as an image file.

## Type {#section_fql_nyl_x2b .section}

-   Key frame

    A key frame has good image quality and can be captured quickly because key frames of videos are independently encoded. Key frames appear in a video at intervals but cannot be captured at a specified time. The system can search for corresponding key frames close to the specified time.

-   Normal frame

    Compared with a key frame, a normal frame has poorer image quality and takes longer time to capture. However, it can be precisely captured at a specified time.


## ​Parameter description​ {#section_gf1_pyl_x2b .section}

You need to take note of the following parameters when you input a file:

[Input](https://help.aliyun.com/document_detail/29253.html#h2-19-15)

Specifies the OSS input file of the video that you want to take a screenshot of.

**Note:** The location of OSS must correspond to the region of MPS. For example, oss-cn-hangzhou location of OSS corresponds to cn-hangzhou region of MPS.

You need to take note of the following parameters in [SnapshotConfig](https://help.aliyun.com/document_detail/29253.html#h2-11-snapshotconfig-10):

-   [OutputFile](https://help.aliyun.com/document_detail/29253.html#h2-38-outputfile-34)

    Specifies the OSS output file of screenshots. You can either specify a fixed file name of an OSS Object or customize one. For naming rules, see [Screenshot OutputFile](https://help.aliyun.com/document_detail/29253.html#h2-38-outputfile-34).

-   Time

    Specifies the time for a single screenshot or the start time for multiple screenshots. Integer type in milliseconds.

-   Interval and Num

    Specify the time interval between any two frames \(unit: second\) and the number of frames to be captured. It involves the following situations:

    -   When Num is not set, screenshots are taken till the end of the video based on the specified interval.

    -   When the value of Num is greater than 1, screenshots are taken based on the specified interval till the number of captured screenshots reaches the specified number.

    -   When the value of Num is 1, a single screenshot is taken asynchronously.

-   Width and Height

    Specify the width and height \(pixels\) of one or more output screenshot images.

    The width and height are based on the input video.

    -   When neither Width nor Height is set, the size of the output image is the same as that of the video.

    -   When either Width or Height is set, the unspecified side is scaled based on the aspect ratio of the video. This avoids image deformation.

    **Note:** We recommend that you do not randomly set both Width and Height to avoid image distortion.

    -   When an MP4 video in the portrait mode has a rotation identifier, the screenshot orientation is landscape.

    -   When an MP4 video in the portrait mode does not have a rotation identifier, the screenshot orientation remains portrait.

-   FrameType

    Specifies the screenshot type: Key Frame or Normal Frame. The default value is Key Frame.

-   TileOutputFile and TileOut

    Specify the OSS output file of image sprites and[TileOut](https://help.aliyun.com/document_detail/29253.html#h2-39-tileout-35).

-   SubOut and Format
    -   If you want to use WebVTT thumbnails, set Format to vtt.
    -   If you want to output the WebVTT thumbnails as image sprites, set Format and SubOut at the same time.

## Scenarios {#section_rnd_czl_x2b .section}

-   Single screenshot

    Specify a time to take the screenshot of a video at that time.

-   Multiple screenshots

    Specify a time interval to take multiple screenshots of a video at even intervals. Each screenshot is an image file. This operation is also called batch screenshots or ordinal screenshots.

-   Image sprites

    You can merge the images of multiple screenshots into one big image sprite. Multiple screenshots can be requested at one time, which reduces the number of image requests and improves client performance.

-   WebVTT thumbnails

    Standard subtitle format in HTML5 as well as the thumbnail preview format for several H5 players. See [JWPlayer Documents](https://support.jwplayer.com/articles/how-to-add-preview-thumbnails).

    WebVTT is a file format. A thumbnail can be either multiple images or one big image sprite.


## Execution method {#section_sqh_dzl_x2b .section}

See `Task execution and completion` in [Task and MPS Queue](https://help.aliyun.com/document_detail/64682.html).

-   Synchronization

    When the API is called, IDs and results of screenshot jobs are synchronously returned.

    Only a single screenshot can be synchronized.

-   Asynchronization

    When the API is called, only IDs of screenshot jobs are returned. To check the screenshot results, you can use screenshot job IDs or use the Notification service.

    Single screenshot, multiple screenshots, image sprites, and WebVTT thumbnails can all be taken asynchronously.


## Code examples {#section_zcm_1vl_x2b .section}

You have a `720P(1280x720)` video lasting 10 seconds. You can specify the height of screenshots to 360 pixels, the start time to 2 seconds, the interval to 1 second, and the number to 3. Three images are captured at the second, third, and fourth seconds, respectively. The image files are named in succession, such as 00001, 00002, and 00003.

[Screenshots-Java SDK](https://help.aliyun.com/document_detail/56333.html)

[Screenshots-Python SDK](https://help.aliyun.com/document_detail/56338.html)

[Screenshots-PHP SDK](https://help.aliyun.com/document_detail/56337.html)

