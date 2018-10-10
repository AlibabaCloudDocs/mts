# Video management {#concept_yrx_qn2_x2b .concept}

The video management feature is mainly achieved by using the **Media Files**. The features of the **Media Files** are shown as follows.

-   Manages your audio/video files.

    A **media file** is a set of source video files, and videos, screenshots, and other resources processed and output by workflows of the source video files. A unique**Media ID** is allocated to each media file.

-   Supports setting the title, tag, category, description, thumbnail, and other information for a media file; and supports search for a media file using the information. In addition, the Media Files contains the format, duration, bit rate, frame rate, resolution, file size, and other metadata of each media file. It also displays the OSS storage URL and CDN domain URL of each resource, and supports online preview and playback for each resource.

-   Supports managing video publishing and also serves as the portal to upload videos on the Web.


1.  Log on to the [Media Processing console](https://partners-intl.aliyun.com/login-required#/mts).
2.  Select the region.
3.  Click **Library** \> **Media Files** to go to the **Media Files** page.
4.  Publishing management.
    -   Click **Publish** at the right side of the expected Media ID, you can set the **publishing status** of a video output from the workflow as**Published**.
    -   Click **Cancel** at the right side of the expected Media ID, you can modify the video**publishing status** as **Not Published**. In the **Not Published** status, the video cannot be accessed using the OSS or CDN URL.
5.  Delete a media file.

    You can delete a media file if it is no longer needed. Click**Delete** at the right side of the Media ID and you can complete deletion.

6.  Query and edit attributes of a media file.

    Click **Manage** at the right side of the expected Media ID to go to the **Video Details** page.

    -   In the **Media Files** tab, you can edit the **Media File Name**and **and Details** of a media file in **Information**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11362/153916677810047_en-US.png)

    -   In the **Retrieve Media URL** tab, you can check the Information, OSS Endpoint, and CDN Endpoint of the source file and the output media file after transcoding. Output media files after transcoding can also be played back and previewed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11362/153916677810048_en-US.png)

    In the preceding figure, the names at the right side of the Source File are names of Transcode nodes of workflows.

    **Note:** OSS and CDN traffic fees are charged on video playback and preview.


