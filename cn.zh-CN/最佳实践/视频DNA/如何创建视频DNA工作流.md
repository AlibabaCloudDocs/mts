# 如何创建视频DNA工作流 {#concept_yyj_mgd_dhb .concept}

视频DNA通过对视频中的图像、音频等指纹特征的提取和比对，解决重复视频查找、视频片段查源、原创识别等问题。有关视频DNA详细知识请参见[视频DNA概述](../../../../../cn.zh-CN/用户指南/视频DNA/概述.md#)。

## 场景 {#section_ejr_kmd_dhb .section}

请参见[使用场景](cn.zh-CN/最佳实践/视频DNA/使用场景.md#)。

## 操作步骤 {#section_fmy_fnd_dhb .section}

1.  登录[媒体处理控制台](https://mps.console.aliyun.com)。
2.  选择所需的地域（目前支持北京、上海、杭州、新加坡、孟买）。
3.  单击**工作流管理** \> **工作流设置**。
4.  单击**创建工作流**，新建一个媒体工作流。
5.  根据实际需求添加任务节点。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/141153/155532106040969_zh-CN.jpg)

6.  设置视频DNA节点。
    -   管道：请选择视频DNA专用管道，否则任务会执行失败。
    -   入库规则：“仅入库不重复内容”表示DNA库中只保存不重复的视频的DNA，重复视频将不会对其DNA进行入库操作。“所有视频均不入库”表示对视频只做比对并不需要保留视频DNA。
    -   工作流终止条件：视频发现重复便终止工作流。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/141153/155532106140970_zh-CN.jpg)

7.  配置工作流中各节点，可参考工作流配置指南。
8.  上传视频并自动触发视频DNA工作流。
9.  视频DNA处理结果包含与输入文件重复的文件个数、以及每对重复文件的相似度及重复区间信息。

