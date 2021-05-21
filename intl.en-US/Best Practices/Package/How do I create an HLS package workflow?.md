# How do I create an HLS package workflow?

## Scenario

Pack three video streams respectively in 480P, 720P and 1080P, and output one file, so that you can swich to the most appropriate video stream based on network bandwidth.

## Procedure

1.  Log on to the [MPS console](https://mts.console.aliyun.com/?spm=5176.2020520001.0.0.6RsosT#/mts/oss).
2.  Select the region.
3.  Click **Library** \> **Library Settings**.
4.  Click **Workflows** \> **Create Workflow**.
5.  Click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310193_en-US.png) icon at the right side of **Input** to add **Output Container** node.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310197_en-US.png)

6.  Click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410194_en-US.png) icon at the right side of **Config.** to add three **Extract Video** nodes.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310198_en-US.png)

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310199_en-US.png)

7.  Configure the **Input** node.
    1.  Click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410194_en-US.png) icon at the right side of the **Input** node.
    2.  In **Input**, click **Select** at the right side of **Input Path**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310200_en-US.png)

        **Note:** **Input path** is a storage location in OSS. The Input path must exist in OSS.

    3.  In **OSS File Manager**, select the bucket name and click **OK**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310202_en-US.png)

    4.  **Message Type** is optional. You can select **MNS Queue** or **Notification** and set an instance.![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503310203_en-US.png)
8.  Configure the **Config.** node.

    1.  Modify **Name**, or you can keep the default name.
    2.  Click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410194_en-US.png) icon at the right side of **Config.** node to configure.
    3.  In **Config.** , click **Select** at the right side of **Output Location**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410205_en-US.png)

        **Note:** **Output Location** is a storage location in OSS and is a file name. To avoid workflows overwite output files when executing tasks, you can combine the following built-in UC variable parameters in the system:

        -   \{RunId\}: The workflow execution ID,

        -   \{ObjectPrefix\}: The path of the original file not including Bucket information,

        -   \{FileName\}: The name of the original file not including the extension name,

        -   \{ExtName\}: The extension name of the original file.

    4.  In **OSS File Manager**, select the bucket name and click **OK**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410207_en-US.png)

        **Note:** The output bucket and the input bucket cannot be the same.

    The **Config.** node is configured successfully.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410208_en-US.png)

9.  Configure the **Extract Video** node.
    1.  Click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410194_en-US.png) icon at the right side of the **Extract Video** node.
    2.  Modify **Name**, or you can keep the default name.
    3.  In **Extract Video** \> **Basic Settings**, click **Select** at the right side of **Template**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410209_en-US.png)

    4.  Select the **template** and click **OK**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410210_en-US.png)

    5.  Configure the **Resource Path**.

        We recommend that you use the default resource path. You can also modify the path based on your needs. Note that if the **Output Location** of the **Config.** node is `a/b/c.m3u8`, the **Resource Path** of the Extract Video node is `d/e/f.m3u8`, then the actual storage position of the extracted file is `a/b/d/e/f.m3u8`.

    6.  In **Audio**, select **Keep**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410216_en-US.png)

        **Note:** Configure the three **Extract Video** nodes respectively according to the previous procedure, and the transcoding templates correspond to the videos in 480P, 720P and 1080P respectively.

10. Configure the **Generate** node.
    1.  Click the ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410194_en-US.png) icon at the right side of **Generate** to configure.
    2.  You can modify the value of **Bandwidth** based on your needs.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410217_en-US.png)

11. Click **OK**, and the nodes configuration is completed.
12. Click **Next**.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/18620/154357503410218_en-US.png)

    The workflow is created successfully.

13. Submit task.

    HLS package workflow is not triggered by default. You can use the `AddMedia` interface to specify video and HLS package workflow ID to process videos.


