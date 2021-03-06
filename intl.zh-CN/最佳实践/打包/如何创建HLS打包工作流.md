# 如何创建HLS打包工作流 {#concept_oh1_klm_x2b .concept}

## 场景 {#section_h5b_llm_x2b .section}

把480P、720P、1080P的视频流打包为1个输出文件，以便您根据网络带宽情况切换最适宜的视频流。

## 操作步骤 {#section_fgz_llm_x2b .section}

1.  登录 [媒体处理控制台](https://mts.console.aliyun.com/?spm=5176.2020520001.0.0.6RsosT#/mts/oss)。
2.  选择所需的地域。
3.  单击 **媒体管理** \> **媒体库设置**。
4.  单击 **工作流** \> **创建工作流**。
5.  单击 **输入** 节点右侧的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710193_zh-CN.png)图标，添加**打包**节点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710197_zh-CN.png)

6.  单击 **打包配置** 节点右侧的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710194_zh-CN.png)图标，添加3个 **视频提取** 节点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710198_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710199_zh-CN.png)

7.  配置 **输入** 节点。
    1.  单击 **输入** 节点右侧的![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710194_zh-CN.png)图标进行配置。
    2.  在 **输入** 页面，单击 **输入路径** 右侧的 **选择**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710200_zh-CN.png)

        **说明：** **输入路径** 是OSS上的一个存储位置，应为OSS上真实存在的路径。

    3.  在 **OSS文件管理** 中，选择bucket名称，并单击 **确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710202_zh-CN.png)

    4.  **消息类别**：可选，您可以选择 **队列** 或 **通知**，并设定队列或消息的实例。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710203_zh-CN.png)
8.  配置 **打包配置** 节点。

    1.  修改 **名称**，或者保持系统默认名称。
    2.  单击 **打包配置**节点右侧的 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710194_zh-CN.png) 图标进行配置。
    3.  在 **打包配置** 页面，单击 **输出路径** 右侧的 **选择**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710205_zh-CN.png)

        **说明：** **输出路径** 是OSS上的一个存储位置及输出文件名。为避免媒体工作流多次执行时覆盖输出文件，您可以组合使用系统内置的UC变量参数：

        -   \{RunId\}：媒体工作流执行ID，

        -   \{ObjectPrefix\}：不含Bucket信息的原文件路径，

        -   \{FileName\}：不含扩展名的原文件名，

        -   \{ExtName\}：原文件扩展名。

    4.  在 **OSS文件管理** 中，选择bucket名称，并单击 **确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710207_zh-CN.png)

        **说明：** 输出Bucket不可与输入Bucket为同一个Bucket。

    **打包配置** 节点配置完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710208_zh-CN.png)

9.  配置 **视频提取** 节点。
    1.  单击 **视频提取**节点右侧的 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710194_zh-CN.png) 图标进行配置。
    2.  修改 **名称**，或者保持系统默认的名称。
    3.  在 **视频提取** \> **基础配置** 页面，单击 **转码模板** 右侧的 **选择**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710209_zh-CN.png)

    4.  选择 **转码模板** 并单击 **确定**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710210_zh-CN.png)

    5.  配置 **资源路径**。

        建议您使用默认值。您也可以根据具体需求进行修改。需要注意的是：若 **打包配置** 节点的 **输出路径**为`a/b/c.m3u8`，提取节点 **资源路径** 为`d/e/f.m3u8`，则提取文件实际存放位置为`a/b/d/e/f.m3u8`。

    6.  在 **音轨** 中，选择 **保留**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199810216_zh-CN.png)

        **说明：** 请您按照上述操作分别配置3个 **视频提取** 节点，转码模板分别对应480P、720P、1080P。

10. 配置 **打包生成** 节点。
    1.  单击 **打包生成**节点右侧的 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199710194_zh-CN.png) 图标进行配置。
    2.  您可以根据实际需求修改 **网络宽带** 的值。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199810217_zh-CN.png)

11. 单击 **确定**，完成节点设置。
12. 单击 **下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/18620/154357199810218_zh-CN.png)

    工作流创建完成。

13. 提交任务。

    HLS打包工作流默认不会自动触发。请您调用 `AddMedia` 接口指定视频及HLS打包工作流ID进行视频的处理。


