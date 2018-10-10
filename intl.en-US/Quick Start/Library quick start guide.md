# Library quick start guide {#concept_afy_2kw_w2b .concept}

A library uses OSS to store your audio and video resources. It provides media indexing function, allowing you to quickly search for audio and video resources by titles, tags, categories, and descriptions.

After MPS is activated, initialize the library and set **Input Media Bucket**and**Output Media Bucket**.

-   **Input Media Bucket**: This bucket stores the original videos you have uploaded.

-   **Output Media Bucket**: This bucket stores videos output by the Media Files.


1.  Log on to the [Media Processing console](https://partners-intl.aliyun.com/login-required#/mts).

    The console checks the activation status of services the product depends on. Follow the operation instructions on this page.

2.  Select the region.
3.  Click **Library** \> **Library Settings** \> **Media Buckets**to set the**Input Media Bucket** and **Output Media Bucket**.

    1.  Set **Input Media Bucket**.
        1.  Click**Add** at the right side of **Input Media Bucket**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582139910_en-US.png)

            **Note:** If you have already created OSS buckets in the current OSS service region, these buckets are listed on the settings interface. In this case, select the appropriate bucket. You can also create a new bucket as the Input Media Bucket.

        2.  Click **Create**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582139911_en-US.png)

        3.  Enter the **Bucket Name**, and click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582139912_en-US.png)

        4.  The **Input Media Bucket**name is shown in the **Input Media Bucket** list. Select the created bucket name and click**OK**.
    2.  Set **Output Media Bucket**.
        1.  Click **Add** at the right side of **Output Media Bucket**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149913_en-US.png)

            **Note:** If you have already created OSS buckets in the current OSS service region, these buckets are listed on the settings interface. In this case, select the appropriate bucket. You can also create a new bucket as the Input Media Bucket.

        2.  Click **Create**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149914_en-US.png)

        3.  Enter the **Bucket Name**, and click**OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149915_en-US.png)

        4.  The **Output Media Bucket** name is shown in the **Output Media Bucket**list. Select the created bucket name and click**OK**.
    As shown in the following figure, the**Input Media Bucket** and **Output Media Bucket** are added.

4.  Click**Library** \> **Library Settings** \> **Workflows** \> **Create Workflow**to create a workflow.

    You can select a workflow from**Preset**and edit it as needed to quickly create a workflow. You can also customize a workflow.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149920_en-US.png)

    1.  At the right side of **Input**node, click the![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149922_en-US.png)icon to set the following information.
        1.  On the**Input** page, click **select** at the right side of **Input Path**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149924_en-US.png)

            **Note:** **Input path**is a storage location in OSS. The Input path must exist in OSS.

        2.  In**OSS File Manager**, select the bucket name, and click**OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149925_en-US.png)

        3.  **Message Type** is optional. You can select MNS Queue or Notification and set the relevant instance.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149926_en-US.png)

    2.  At the right side of **Input**node, click the![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149927_en-US.png)icon to add the **Transcode** node.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149928_en-US.png)

        1.  At the right side of the **Transcode** node, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149922_en-US.png)icon to configure.
        2.  In **Transcode** \> **Basic Settings** , click **Select** at the right side of **Template**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159929_en-US.png)

        3.  Select the **Transcode template** and click**OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159930_en-US.png)

        4.  In **Transcode** \> **Basic Settings**, click **Select** at the right side of **Output Location**.

            **Note:** 

            **Output Location** is a storage location in OSS and the output file name. To avoid output files from being overwritten when a workflow is run multiple times, you can combine the system’s built-in variable parameters:

            -   \{RunId\} the media workflow run ID,

            -   \{ObjectPrefix\} the original file path not including Bucket information,

            -   \{FileName\} the original file name not including the extension name,

            -   \{ExtName\} the original file extension name.

        5.  In **OSS File Manager**, select the bucket name and click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159931_en-US.png)

            **Note:** The Input Bucket and the Output Bucket cannot be the same.

        6.  The **Output Location**is a storage location in OSS and the output file name. For details, see Output Location description for the **Transcode** node.

            The **Transcode**node cofiguration is completed.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159932_en-US.png)

    3.  At the right side of the **Input**node or**Transcode**node, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149927_en-US.png)icon to add the**Screenshot** node.
        1.  At the right side of the **Screenshot** node, click the![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582149922_en-US.png)icon to configure.
        2.  Select **Sreenshot Type**.
        3.  Click **Select**at the right side of **Output Location**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159933_en-US.png)

        4.  In **OSS File Manager**, select the bucket name and click**OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159934_en-US.png)

        5.  Enabe the**Set As Thumbnail** function.

            When multiple screenshots exist, the first one is set as the Thumbnail by default.

    4.  After setting the nodes, click**Next**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159944_en-US.png)

    5.  You can bind a CDN domain name to the**Output Bucket**\(Optional\).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159945_en-US.png)

        **Note:** The added domain name must already be filed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159946_en-US.png)

5.  Upload a file.

    1.  Click **Library** \> **Media Files** \> **Upload Media**.
    2.  On the Uploadpage, select the workflow, and click **Select File**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159949_en-US.png)

        After the file is uploaded, you can click**Upload More**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159952_en-US.png)

    After the file is uploaded, this workflow is automatically triggered.

6.  View workflow progress and result.
    -   On the Media Files page, you can view the Task Status and output file information.
    -   Click**Details** in the **Task Status**column, you can view the Workflow Instance Status, source file, transcoding output, screenshot output, and other information.
    -   Click the **Task ID**, you can also obtain the address of the transcoding output file and preview video playback.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11351/15391582159955_en-US.png)


