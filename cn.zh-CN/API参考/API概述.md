# API概述

## 媒体信息接口

|API|描述|
|:--|:-|
|[SubmitMediaInfoJob](/cn.zh-CN/API参考/媒体信息接口/提交媒体信息作业.md)|提交媒体信息作业。|
|[QueryMediaInfoJobList](/cn.zh-CN/API参考/媒体信息接口/查询媒体信息作业.md)|查询媒体信息作业。|

## 预置智能模板推荐接口

|API|描述|
|:--|:-|
|[SubmitAnalysisJob](/cn.zh-CN/API参考/预置智能模版推荐接口/提交模板分析作业.md)|提交预置模板分析作业。|
|[QueryAnalysisJobList](/cn.zh-CN/API参考/预置智能模版推荐接口/查询模板分析作业.md)|查询模板分析作业。|

## 转码接口

|API|描述|
|:--|:-|
|[SubmitJobs](/cn.zh-CN/API参考/转码接口/提交转码作业.md)|提交转码作业。|
|[CancelJob](/cn.zh-CN/API参考/转码接口/取消转码作业.md)|取消转码作业。|
|[QueryJobList](/cn.zh-CN/API参考/转码接口/查询转码作业.md)|通过转码作业ID，批量查询转码作业。|
|[ListJob](/cn.zh-CN/API参考/转码接口/列出转码作业.md)|通过作业状态，创建时间区间，转码管道列出转码作业。|

## 自定义转码模板接口

|API|描述|
|:--|:-|
|[AddTemplate](/cn.zh-CN/API参考/自定义转码模板接口/新增自定义转码模板.md)|创建自定义模板，包含容器信息，视频跟音频流等设置。|
|[UpdateTemplate](/cn.zh-CN/API参考/自定义转码模板接口/更新自定义转码模版.md)|更新自定义模板设置。|
|[QueryTemplateList](/cn.zh-CN/API参考/自定义转码模板接口/查询自定义转码模板.md)|查询自定义模板。|
|[SearchTemplate](/cn.zh-CN/API参考/自定义转码模板接口/搜索自定义转码模板.md)|搜索指定状态的自定义模板。|
|[DeleteTemplate](/cn.zh-CN/API参考/自定义转码模板接口/删除自定义转码模板.md)|删除自定义模板。|

## 管道接口

|API|描述|
|:--|:-|
|[UpdatePipeline](/cn.zh-CN/API参考/管道接口/更新管道.md)|更新管道。|
|[QueryPipelineList](/cn.zh-CN/API参考/管道接口/查询管道.md)|查询管道。|
|[SearchPipeline](/cn.zh-CN/API参考/管道接口/搜索管道.md)|通过管道状态搜索管道。|

## 水印模板接口

|API|描述|
|:--|:-|
|[AddWaterMarkTemplate](/cn.zh-CN/API参考/水印模板接口/创建水印模版.md)|创建水印模板。|
|[UpdateWaterMarkTemplate](/cn.zh-CN/API参考/水印模板接口/更新水印模版.md)|更新指定水印模板的名称、配置。|
|[QueryWaterMarkTemplateList](/cn.zh-CN/API参考/水印模板接口/查询水印模板.md)|查询水印模板。|
|[SearchWaterMarkTemplate](/cn.zh-CN/API参考/水印模板接口/搜索水印模板.md)|搜索指定状态的水印模板。|
|[DeleteWaterMarkTemplate](/cn.zh-CN/API参考/水印模板接口/删除水印模板.md)|删除水印模板。|

## 截图接口

|API|描述|
|:--|:-|
|[SubmitSnapshotJob](/cn.zh-CN/API参考/截图接口/提交截图作业.md)|提交截图作业接口，目前支持生成jpg格式图片。|
|[QuerySnapshotJobList](/cn.zh-CN/API参考/截图接口/查询截图作业.md)|查询截图作业结果。|

## 媒体工作流接口

|API|描述|
|:--|:-|
|[AddMediaWorkflow](/cn.zh-CN/API参考/媒体工作流接口/新增媒体工作流.md)|新增媒体工作流。|
|[ActivateMediaWorkflow](/cn.zh-CN/API参考/媒体工作流接口/激活媒体工作流.md)|激活媒体工作流。|
|[DeactivateMediaWorkflow](/cn.zh-CN/API参考/媒体工作流接口/停用媒体工作流.md)|停用媒体工作流。|
|[DeleteMediaWorkflow](/cn.zh-CN/API参考/媒体工作流接口/删除媒体工作流.md)|删除媒体工作流。|
|[UpdateMediaWorkflow](/cn.zh-CN/API参考/媒体工作流接口/更新媒体工作流.md)|用于更新媒体工作流的拓扑结构。|
|[QueryMediaWorkflowList](/cn.zh-CN/API参考/媒体工作流接口/查询媒体工作流.md)|查询已注册媒体工作流。|
|[SearchMediaWorkflow](/cn.zh-CN/API参考/媒体工作流接口/搜索媒体工作流.md)|搜索媒体工作流。|
|[UpdateMediaWorkflowTriggerMode](/cn.zh-CN/API参考/媒体工作流接口/更新媒体工作流触发模式.md)|更新媒体工作流触发模式。|

## 媒体工作流执行实例接口

|API|描述|
|:--|:-|
|[QueryMediaWorkflowExecutionList](/cn.zh-CN/API参考/媒体工作流执行实例接口/查询媒体工作流执行实例.md)|查询媒体工作流执行实例。|
|[ListMediaWorkflowExecutions](/cn.zh-CN/API参考/媒体工作流执行实例接口/查询媒体工作流执行实例.md)|遍历媒体工作流执行实例。|

## 媒体接口

|API|描述|
|:--|:-|
|[AddMedia](/cn.zh-CN/API参考/媒体接口/新增媒体.md)|新增媒体。|
|[DeleteMedia](/cn.zh-CN/API参考/媒体接口/删除媒体.md)|删除媒体。|
|[UpdateMedia](/cn.zh-CN/API参考/媒体接口/更新媒体-基本信息.md)|更新媒体基本信息，如标题，描述，类目等。|
|[UpdateMediaCategory](/cn.zh-CN/API参考/媒体接口/更新媒体-类目.md)|更新媒体类目。|
|[UpdateMediaCover](/cn.zh-CN/API参考/媒体接口/更新媒体-封面.md)|更新媒体封面。|
|[AddMediaTag](/cn.zh-CN/API参考/媒体接口/更新媒体-添加标签.md)|新增媒体标签。|
|[DeleteMediaTag](/cn.zh-CN/API参考/媒体接口/更新媒体-删除标签.md)|删除媒体标签。|
|[UpdateMediaPublishState](/cn.zh-CN/API参考/媒体接口/更新媒体-发布状态.md)|更新媒体发布状态。|
|[QueryMediaList](/cn.zh-CN/API参考/媒体接口/查询媒体-使用媒体ID.md)|查询媒体列表。|
|[QueryMediaListByURL](/cn.zh-CN/API参考/媒体接口/查询媒体-使用OSS文件地址.md)|使用OSS文件地址查询。|

## 媒体Bucket接口

|API|描述|
|:--|:-|
|[BindInputBucket](/cn.zh-CN/API参考/媒体Bucket接口/绑定输入媒体Bucket.md)|媒体库绑定输入Bucket。|
|[BindOutputBucket](/cn.zh-CN/API参考/媒体Bucket接口/绑定输出媒体Bucket.md)|媒体库绑定输出Bucket。|
|[ListAllMediaBucket](/cn.zh-CN/API参考/媒体Bucket接口/查询媒体Bucket.md)|列出媒体库所有媒体Bucket。|

## 媒体审核接口

|API|描述|
|:--|:-|
|[SubmitMediaCensorJob](/cn.zh-CN/API参考/媒体审核接口/提交媒体审核作业.md)|提交媒体审核作业。|
|[QueryMediaCensorJobDetail](/cn.zh-CN/API参考/媒体审核接口/查询媒体审核作业详情.md)|查询媒体审核作业详情。|
|[SubmitVideoQualityJob](/cn.zh-CN/API参考/媒体审核接口/提交视频质量审核作业.md)|提交视频质量审核作业。|
|[QueryVideoQualityJob](/cn.zh-CN/API参考/媒体审核接口/查询视频质量审核作业.md)|查询视频质量审核作业的状态与结果。|

## 视频DNA接口

|API|描述|
|:--|:-|
|[SubmitFpShotJob](/cn.zh-CN/API参考/视频DNA接口/提交视频DNA作业.md)|查询视频库中是否存在相同或者相近的DNA结果。|
|[QueryFpShotJobList](/cn.zh-CN/API参考/视频DNA接口/查询视频DNA作业.md)|查询视频DNA作业结果。|
|[CreateFpShotDB](/cn.zh-CN/API参考/视频DNA接口/提交新建视频DNA库.md)|提交新建视频DNA库任务，返回新建DNA库信息。|
|[ListFpShotDB](/cn.zh-CN/API参考/视频DNA接口/查询视频DNA库.md)|查询DNA库状态信息。|
|[ReportFpShotJobResult](/cn.zh-CN/API参考/视频DNA接口/视频DNA作业结果反馈.md)|反馈视频作业有误结果。|
|[QueryFpImportResult](/cn.zh-CN/API参考/视频DNA接口/查询视频DNA导库结果.md)|查询导库视频比对结果。|
|[ListFpShotFiles](/cn.zh-CN/API参考/视频DNA接口/查询DNA库文件列表.md)|查询DNA库文件列表。|
|[SubmitFpFileDeleteJob](/cn.zh-CN/API参考/视频DNA接口/提交删除DNA文件.md)|提交删除DNA文件。|
|[QueryFpFileDeleteJobList](/cn.zh-CN/API参考/视频DNA接口/查询删除DNA文件.md)|查询删除DNA文件。|
|[SubmitFpDBDeleteJob](/cn.zh-CN/API参考/视频DNA接口/提交清空或删除DNA库.md)|提交清空或删除DNA库。|
|[QueryFpDBDeleteJobList](/cn.zh-CN/API参考/视频DNA接口/查询清空或删除DNA库.md)|查询清空或删除DNA库。|

## 智能标签接口

|API|描述|
|:--|:-|
|[SubmitSmarttagJob](/cn.zh-CN/API参考/智能标签接口/提交智能标签作业.md)|提交智能标签作业。|
|[QuerySmarttagJob](/cn.zh-CN/API参考/智能标签接口/查询智能标签作业.md)|查询智能标签作业。|
|[AddSmarttagTemplate](/cn.zh-CN/API参考/智能标签接口/添加模板.md)|添加模板。|
|[QuerySmarttagTemplateList](/cn.zh-CN/API参考/智能标签接口/查询模板.md)|查询模板。|
|[UpdateSmarttagTemplate](/cn.zh-CN/API参考/智能标签接口/更新模板.md)|更新模板。|
|[DeleteSmarttagTemplate](/cn.zh-CN/API参考/智能标签接口/删除模板.md)|删除模板。|
|[RegisterCustomFace](/cn.zh-CN/API参考/智能标签接口/注册⾃定义⼈脸.md)|注册一张自定义人脸。|
|[UnregisterCustomFace](/cn.zh-CN/API参考/智能标签接口/注销⾃定义⼈脸.md)|注销一张自定义人脸，或注销某个自定义人物下的所有人脸。|
|[TagCustomPerson](/cn.zh-CN/API参考/智能标签接口/添加⾃定义⼈物库或⼈物标签.md)|给自定义人物库或人物贴标签。|
|[ListCustomPersons](/cn.zh-CN/API参考/智能标签接口/列出⼈物库所有⼈物和⼈脸信息.md)|列出指定人物库下所有人物和人脸信息。|

## 智能生产接口

|API|描述|
|---|--|
|[SubmitIProductionJob](/cn.zh-CN/API参考/智能生产接口/提交智能生产作业.md)|提交智能生产作业。|
|[QueryIProductionJob](/cn.zh-CN/API参考/智能生产接口/查询智能生产作业.md)|查询智能生产作业。|

