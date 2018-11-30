# How do I create an HLS package workflow? {#concept_oh1_klm_x2b .concept}

## Scenario {#section_h5b_llm_x2b .section}

Pack three video streams respectively in 480P, 720P and 1080P, and output one file, so that you can swich to the most appropriate video stream based on network bandwidth.

## Procedure {#section_fgz_llm_x2b .section}

1.  Log on to the [MPS console](https://partners-intl.aliyun.com/login-required#/mps).
2.  Select the region.
3.  Click **Library** \> **Library Settings**.
4.  Click **Workflows** \> **Create Workflow**.
5.  Click the ![](images/10193_en-US.png) icon at the right side of **Input** to add **Output Container** node.

    ![](images/10197_en-US.png)

6.  Click the ![](images/10194_en-US.png) icon at the right side of **Config.** to add three **Extract Video** nodes.

    ![](images/10198_en-US.png)

    ![](images/10199_en-US.png)

7.  Configure the **Input** node.
    1.  Click the ![](images/10194_en-US.png) icon at the right side of the **Input** node.
    2.  In **Input**, click **Select** at the right side of **Input Path**.

        ![](images/10200_en-US.png)

        **Note:** **Input path**is a storage location in OSS. The Input path must exist in OSS.

    3.  In **OSS File Manager**, select the bucket name and click**OK**.

        ![](images/10202_en-US.png)

    4.  **Message Type** is optional. You can select **MNS Queue** or **Notification** and set an instance.![](images/10203_en-US.png)
8.  Configure the **Config.** node.

    1.  Modify **Name**, or you can keep the default name.
    2.  Click the ![](images/10194_en-US.png) icon at the right side of **Config.**node to configure.
    3.  In **Config.** , click **Select** at the right side of **Output Location**.

        ![](images/10205_en-US.png)

        **Note:** **Output Location** is a storage location in OSS and is a file name. To avoid workflows overwite output files when executing tasks, you can combine the following built-in UC variable parameters in the system:

        -   \{RunId\}: The workflow execution ID,

        -   \{ObjectPrefix\}: The path of the original file not including Bucket information,

        -   \{FileName\}: The name of the original file not including the extension name,

        -   \{ExtName\}: The extension name of the original file.

    4.  In **OSS File Manager**, select the bucket name and click **OK**.

        ![](images/10207_en-US.png)

        **Note:** The output bucket and the input bucket cannot be the same.

    The **Config.** node is configured successfully.

    ![](images/10208_en-US.png)

9.  Configure the **Extract Video** node.
    1.  Click the ![](images/10194_en-US.png) icon at the right side of the **Extract Video**node.
    2.  Modify **Name**, or you can keep the default name.
    3.  In **Extract Video** \> **Basic Settings**, click **Select** at the right side of **Template**.

        ![](images/10209_en-US.png)

    4.  Select the **template** and click **OK**.

        ![](images/10210_en-US.png)

    5.  Configure the **Resource Path**.

        We recommend that you use the default resource path. You can also modify the path based on your needs. Note that if the **Output Location** of the **Config.** node is `a/b/c.m3u8`, the **Resource Path** of the Extract Video node is `d/e/f.m3u8`, then the actual storage position of the extracted file is `a/b/d/e/f.m3u8`.

    6.  In **Audio**, select **Keep**.

        ![](images/10216_en-US.png)

        **Note:** Configure the three **Extract Video** nodes respectively according to the previous procedure, and the transcoding templates correspond to the videos in 480P, 720P and 1080P respectively.

10. Configure the **Generate** node.
    1.  Click the ![](images/10194_en-US.png) icon at the right side of **Generate** to configure.
    2.  You can modify the value of **Bandwidth** based on your needs.

        ![](images/10217_en-US.png)

11. Click **OK**, and the nodes configuration is completed.
12. 单击 **下一步**。

    ![](images/10218_en-US.png)

    The workflow is created successfully.

13. Submit task.

    HLS package workflow is not triggered by default. You can use the `AddMedia` interface to specify video and HLS package workflow ID to process videos.


