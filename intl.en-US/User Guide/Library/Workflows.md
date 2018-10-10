# Workflows {#concept_a11_qny_w2b .concept}

Workflows support screenshot taking, transcoding, encapsulation, watermarking, encryption, and editing, allowing you to fast and flexibly construct a cloud-based audio/video handling process on demand. When a workflow starts or completes execution, a workflow execution message can be sent to the specified message queue or message notification.

Each media workflow is bound to a path of the **Input Media Bucket**. When an audio or video file is uploaded to the path or its sub-directory, the workflow is automatically triggered to perform preset processing operations and save the processing result to the specified path of the **Output Media Bucket**.

## Create a workflow {#section_zzj_54y_w2b .section}

1.  Log on to the [Media Processing console](https://partners-intl.aliyun.com/login-required#/mts).
2.  Select the region.
3.  Click **Library** \> **Library Settings** \> **Workfows**.
4.  Click **Create Workflow**.
5.  Set the workflow information.

    You can select a workflow from**Preset** and edit it as needed to quickly create a workflow. You can also customize a workflow.

    1.  Set the workflow name in **Workflow Name**.
    2.  Select **Customize**in **Preset**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/15391667279999_en-US.png)

6.  Set nodes.

    1.  Set the **Input** node.
        1.  At the right side of the **Input** node, click the![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710000_en-US.png)icon to set the following information.
        2.  On the **Input** node, click **Select** at the right side of **Input Path**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710001_en-US.png)

        3.  In **OSS File Manager**, select the bucket name, and click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710002_en-US.png)

            **Note:** To facilitate searching for fies, we recommend that the storage location of the original video in the Input Media Bucket and the storage location of the Output Media Bucket are consistent. Examples here are all stored in the root directory.

        4.  **Message Type** is optional. You can select MNS Queue or Notification and set the relevant instance.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710003_en-US.png)

    2.  Set the **Transcodde** node.
        1.  Click the icon at the right side of the **Input** node

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710005_en-US.png)

            to add the **Transcoding** node.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710006_en-US.png)

        2.  At the right side of the **Transcode** node, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710000_en-US.png) icon.
        3.  In **Transcode** \> **Basic Settings**, click **Select** at the right side of **Template**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710007_en-US.png)

        4.  Select the **template** and click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710008_en-US.png)

        5.  In **Transcode** \> **Basic Settings**, click **Select** at the right side of **Output Location**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810009_en-US.png)

            **Note:** 

            **Output Location** is a storage location in OSS and the output file name. To avoid output files from being overwritten when a workflow is run multiple times, you can combine the system’s built-in variable parameters:

            -   \{RunId\} the media workflow run ID,

            -   \{ObjectPrefix\} the original file path not including Bucket information,

            -   \{FileName\} the original file name not including the extension name;

            -   \{ExtName\} the original file extension name.

        6.  In **OSS File Manager**, select the bucket name and click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710002_en-US.png)

            **Note:** The Input Bucket and the Output Bucket cannot be the same.

        7.  The **Output Location** is a storage location in OSS and the output file name. For more information, see Output Location description for the **Transcode** node. Click**OK**, and the **Transcode** node cofiguration is completed.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810011_en-US.png)

    3.  Set the**Screenshot** node.
        1.  At the right side of the**Input** node or **Transcode** node, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710005_en-US.png) icon to add the **Screenshot** node.
        2.  At the right side of the **Screenshot** node, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710000_en-US.png)icon.
        3.  Select **Sreenshot Type**.
        4.  Click **Select** at the right side of**Output Location**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810012_en-US.png)

        5.  In **OSS File Manager**, select the bucket name and click**OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810010_en-US.png)

        6.  Set the Output Location.

            Output Location is a storage location in OSS and the output file name. To avoid the output files fron being overwritten when a workflow is run for multiple times, you can combine the system’s built-in variable parameters, in which \{SnapshotTime\} indicates the screenshot time, in milliseconds.

        7.  Enable the **Set As Thumbnail** function.

            If this function is enabled, the screenshot taken on this node is automatically set as the thumbnail of the media files set in the library. If multiple screenshots are taken, the first screenshot is set as the thumbnail by default.

    4.  Set the **Publish** node.
        1.  At the right side of **Publish** node, click the![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672710000_en-US.png) icon to set the **Publish** node.
        2.  On the **Publish** page, set the Media Publication Type **Automatic**.
            -   Media Publication Type is set to **Manual** by default. In this case, each file output by transcoding cannot be directed accessed using an OSS URL in public-read mode or CDN URL.
            -   If Media Publication Type is set to **Automatic**, a file output by transcoding can be directed accessed using an OSS URL in public-read mode or CDN URL.
    After setting the nodes, click**Next**to go to the **Content Delivery Network \(CDN\)**configuration page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810013_en-US.png)

7.  Configure the Content Delivery Network \(CDN\).

    The on-demand CDN domains that use the output media bucket as the source of this workflow are listed.

    In case of need, click **+ Add** to quickly add an on-demand CDN domain for**Output Bucket**\(Optional\). For more information, see [Acceleration of On-Demand Video/Audio](../../../../reseller.en-US/User Guide/Business type/Type 3: On-Demand Video/Audio Acceleration.md#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810014_en-US.png)

    **Note:** The added domain name must already be filed.


Complete the workflow creation.

After the media workflow is created, it is automatically activated and enters the Enabled status. The audio and video files uploaded to the**Input Location** bound to the **Input** node automatically trigger the workflow execution.

Click **Manage Workflow** to return to the Workflows page, the workflow ID list is displayed.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11360/153916672810015_en-US.png)

## Edit and delete workflows {#section_rcj_s5y_w2b .section}

To edit, modify, or delete a workflow, set the workflow status as **Disabled**.

After the workflow is stopped, it is not automatically executed.

After editing the workflow, click **Enable** to restore automatic execution of the workflow.

