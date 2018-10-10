# Video file upload and workflow execution {#concept_orb_wvy_w2b .concept}

## Upload a file {#section_y1f_xvy_w2b .section}

You can use the MPS console or OSS related upload tools to upload a video file. In addition, an upload SDK that covers all platforms is provided. For details, see Upload SDK usage instructions, Upload SDK downloading. For more information, see Upload SDK usage instructions, Upload SDK downloading.

-   Upload a video file on the MPS console.

    After creating a workflow, upload a video file to the specified workflow in **Media Files**. The video is saved to the Input Path bound to the workflow. After the video is uploaded, the workflow is automatically executed to process the video.

    1.  Log on to the [Media Processing console](https://partners-intl.aliyun.com/login-required#/mts).
    2.  Select the region.
    3.  Click **Library** \> **Media Files**.
    4.  Click **Upload Media**.
    5.  On the **Upload**page, select a Workflow, and click **Select File**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11361/153916675210022_en-US.png)

        After uploading is completed, you can also click **Upload More**to upload multiple video files.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11361/153916675210023_en-US.png)

        **Note:** 

        -   Web upload supports multi-part upload, resumable upload, and batch upload.
        -   In the upload process, you can switch to other pages on the MPS console, but do not close the browser or access the consoles of other cloud products. Otherwise, the upload process is interrupted.
-   Upload a media file using OSS tools.

    We recommend that you use the OSS console client \(officially recommended\).

    -   Tool market for [Windows](http://market.aliyun.com/products/53690006/cmgj000281.html).

    -   Tool market for [Mac](http://market.aliyun.com/products/53690006/cmgj000282.html).

**Note:** Tool usage instructions are available on the preceding links.

    When using the OSS console client, upload the video file to the Input Path bound to the corresponding workflow to enable automatic workflow execution.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11361/153916675210024_en-US.png)


## Execute a workflow {#section_s2p_wwy_w2b .section}

After a video is uploaded to the Input Path bound to the workflow, the workflow is automatically executed. Each workflow execution is called an execution instance. You can query the status of the execution instance of the specified workflow on the Executed Tasks page.

1.  Click **Library** \> **Library Settings** \> **Executed Tasks**.

2.  Select the Workflow ID.
3.  Select the **Task**, and click **Details** at the right side.You can view the details of the instance through **Details**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11361/153916675210026_en-US.png)


