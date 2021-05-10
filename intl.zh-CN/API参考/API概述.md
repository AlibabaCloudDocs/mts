# API概述

## 媒体信息接口

|API|描述|
|:--|:-|
|[SubmitMediaInfoJob](/intl.zh-CN/API参考/媒体信息接口/提交媒体信息作业.md)|提交媒体信息作业接口。|
|[QueryMediaInfoJobList](/intl.zh-CN/API参考/媒体信息接口/查询媒体信息作业.md)|查询媒体信息作业接口。|

## 预置智能模板推荐接口

|API|描述|
|:--|:-|
|[SubmitAnalysisJob](/intl.zh-CN/API参考/预置智能模版推荐接口/提交模板分析作业.md)|提交预置模板分析作业接口。|
|[QueryAnalysisJobList](/intl.zh-CN/API参考/预置智能模版推荐接口/查询模板分析作业.md)|查询模板分析作业接口。|

## 转码接口

|API|描述|
|:--|:-|
|[SubmitJobs](/intl.zh-CN/API参考/转码接口/提交转码作业.md)|提交转码作业接口。|
|[CancelJob](/intl.zh-CN/API参考/转码接口/取消转码作业.md)|取消转码作业接口。|
|[QueryJobList](/intl.zh-CN/API参考/转码接口/查询转码作业.md)|通过转码作业ID，批量查询转码作业。|
|[ListJob](/intl.zh-CN/API参考/转码接口/列出转码作业.md)|通过作业状态，创建时间区间，转码管道列出转码作业。|

## 自定义转码模板接口

|API|描述|
|:--|:-|
|[AddTemplate]()|创建自定义模板，包含容器信息，视频跟音频流等设置。|
|[UpdateTemplate](/intl.zh-CN/API参考/自定义转码模板接口/更新自定义转码模版.md)|更新自定义模板设置。|
|[QueryTemplateList](/intl.zh-CN/API参考/自定义转码模板接口/查询自定义转码模板.md)|查询自定义模板接口。|
|[SearchTemplate](/intl.zh-CN/API参考/自定义转码模板接口/搜索自定义转码模板.md)|搜索指定状态的自定义模板。|
|[DeleteTemplate](/intl.zh-CN/API参考/自定义转码模板接口/删除自定义转码模板.md)|删除自定义模板接口。|

## 管道接口

|API|描述|
|:--|:-|
|[UpdatePipeline](/intl.zh-CN/API参考/管道接口/更新管道.md)|更新管道接口。|
|[QueryPipelineList](/intl.zh-CN/API参考/管道接口/查询管道.md)|查询管道接口。|
|[SearchPipeline](/intl.zh-CN/API参考/管道接口/搜索管道.md)|通过管道状态搜索管道。|

## 水印模板接口

|API|描述|
|:--|:-|
|[AddWaterMarkTemplate](/intl.zh-CN/API参考/水印模板接口/新增水印模版.md)|创建水印模板。|
|[UpdateWaterMarkTemplate](/intl.zh-CN/API参考/水印模板接口/更新水印模版.md)|更新指定水印模板的名称、配置。|
|[QueryWaterMarkTemplateList](/intl.zh-CN/API参考/水印模板接口/查询水印模板.md)|查询水印模板接口。|
|[SearchWaterMarkTemplate](/intl.zh-CN/API参考/水印模板接口/搜索水印模板.md)|搜索指定状态的水印模板。|
|[DeleteWaterMarkTemplate](/intl.zh-CN/API参考/水印模板接口/删除水印模板.md)|删除水印模板接口。|

## 截图接口

|API|描述|
|:--|:-|
|[SubmitSnapshotJob](/intl.zh-CN/API参考/截图接口/提交截图作业.md)|提交截图作业接口，目前支持生成jpg格式图片。|
|[QuerySnapshotJobList](/intl.zh-CN/API参考/截图接口/查询截图作业.md)|查询截图作业结果。|

## 媒体工作流接口

|API|描述|
|:--|:-|
|[AddMediaWorkflow](/intl.zh-CN/API参考/媒体工作流接口/新增媒体工作流.md)|用于新增媒体工作流。|
|[ActivateMediaWorkflow](/intl.zh-CN/API参考/媒体工作流接口/激活媒体工作流.md)|激活媒体工作流。|
|[DeactivateMediaWorkflow](/intl.zh-CN/API参考/媒体工作流接口/停用媒体工作流.md)|停用媒体工作流。|
|[DeleteMediaWorkflow](/intl.zh-CN/API参考/媒体工作流接口/删除媒体工作流.md)|删除媒体工作流。|
|[UpdateMediaWorkflow](/intl.zh-CN/API参考/媒体工作流接口/更新媒体工作流.md)|用于更新媒体工作流的拓扑结构。|
|[QueryMediaWorkflowList](/intl.zh-CN/API参考/媒体工作流接口/查询媒体工作流.md)|查询已注册媒体工作流。|
|[SearchMediaWorkflow](/intl.zh-CN/API参考/媒体工作流接口/搜索媒体工作流.md)|搜索媒体工作流。|
|[UpdateMediaWorkflowTriggerMode](/intl.zh-CN/API参考/媒体工作流接口/更新媒体工作流触发模式.md)|更新媒体工作流触发模式。|

## 媒体工作流执行实例接口

|API|描述|
|:--|:-|
|[ListMediaWorkflowExecutions](/intl.zh-CN/API参考/媒体工作流执行实例接口/遍历媒体工作流执行实例.md)|遍历媒体工作流执行实例。|
|[QueryMediaWorkflowExecutionList](/intl.zh-CN/API参考/媒体工作流执行实例接口/查询媒体工作流执行实例.md)|查询媒体工作流执行实例。|

## 媒体接口

|API|描述|
|:--|:-|
|[AddMedia](/intl.zh-CN/API参考/媒体接口/新增媒体.md)|新增媒体。|
|[DeleteMedia](/intl.zh-CN/API参考/媒体接口/删除媒体.md)|删除媒体。|
|[UpdateMedia](/intl.zh-CN/API参考/媒体接口/更新媒体-基本信息.md)|更新媒体基本信息，如标题，描述，类目等。|
|[UpdateMediaCategory](/intl.zh-CN/API参考/媒体接口/更新媒体-类目.md)|更新媒体类目。|
|[UpdateMediaCover](/intl.zh-CN/API参考/媒体接口/更新媒体-封面.md)|更新媒体封面。|
|[AddMediaTag](/intl.zh-CN/API参考/媒体接口/更新媒体-添加标签.md)|新增媒体标签。|
|[DeleteMediaTag](/intl.zh-CN/API参考/媒体接口/更新媒体-删除标签.md)|删除媒体标签。|
|[UpdateMediaPublishState](/intl.zh-CN/API参考/媒体接口/更新媒体-发布状态.md)|更新媒体发布状态。|
|[QueryMediaList](/intl.zh-CN/API参考/媒体接口/查询媒体-使用媒体ID.md)|查询媒体列表。|
|[QueryMediaListByURL](/intl.zh-CN/API参考/媒体接口/查询媒体-使用OSS文件地址.md)|使用OSS文件地址查询媒体。|

## 媒体Bucket接口

|API|描述|
|:--|:-|
|[BindInputBucket](/intl.zh-CN/API参考/媒体Bucket接口/绑定输入媒体Bucket.md)|媒体库绑定输入Bucket。|
|[BindOutputBucket](/intl.zh-CN/API参考/媒体Bucket接口/绑定输出媒体Bucket.md)|媒体库绑定输出Bucket。|
|[ListAllMediaBucket](/intl.zh-CN/API参考/媒体Bucket接口/查询媒体Bucket.md)|列出媒体库所有媒体Bucket。|

## 智能生产接口

|API|描述|
|---|--|
|[t1896506.md\#]()|提交智能生产作业接口。|
|[查询智能生产作业]()|查询智能生产作业接口。|

