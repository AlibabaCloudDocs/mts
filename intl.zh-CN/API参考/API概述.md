# API概述 {#reference_vxd_1sm_x2b .reference}

## 媒体信息接口 {#section_qxt_bsm_x2b .section}

|API|描述|
|:--|:-|
|[SubmitMediaInfoJob](https://help.aliyun.com/document_detail/29220.html)|提交媒体信息作业接口。|
|[QueryMediaInfoJobList](https://help.aliyun.com/document_detail/29221.html)|查询媒体信息作业接口。|

## 预置智能模板推荐接口 {#section_e2m_jsm_x2b .section}

|API|描述|
|:--|:-|
|[SubmitAnalysisJob](https://help.aliyun.com/document_detail/29223.html)|提交预置模板分析作业接口。|
|[QueryAnalysisJobList](https://help.aliyun.com/document_detail/29224.html)|查询模板分析作业接口。|

## 转码接口 {#section_c5c_b5m_x2b .section}

|API|描述|
|:--|:-|
|[SubmitJobs](https://help.aliyun.com/document_detail/29226.html)|提交转码作业接口。|
|[CancelJob](https://help.aliyun.com/document_detail/29227.html)|取消转码作业接口。|
|[QueryJobList](https://help.aliyun.com/document_detail/29228.html)|通过转码作业ID，批量查询转码作业。|
|[ListJob](https://help.aliyun.com/document_detail/29229.html)|通过作业状态，创建时间区间，转码管道列出转码作业。|

## 自定义转码模板接口 {#section_ncd_f5m_x2b .section}

|API|描述|
|:--|:-|
|[AddTemplate](https://help.aliyun.com/document_detail/29239.html)|创建自定义模板，包含容器信息，视频跟音频流等设置。|
|[UpdateTemplate](https://help.aliyun.com/document_detail/29240.html)|更新自定义模板设置。|
|[QueryTemplateList](https://help.aliyun.com/document_detail/29241.html)|查询自定义模板接口。|
|[SearchTemplate](https://help.aliyun.com/document_detail/29242.html)|搜索指定状态的自定义模板。|
|[DeleteTemplate](https://help.aliyun.com/document_detail/29243.html)|删除自定义模板接口。|

## 管道接口 {#section_wvl_g5m_x2b .section}

|API|描述|
|:--|:-|
|[UpdatePipeline](https://help.aliyun.com/document_detail/29235.html)|更新管道接口。|
|[QueryPipelineList](https://help.aliyun.com/document_detail/29236.html)|查询管道接口。|
|[SearchPipeline](https://help.aliyun.com/document_detail/29237.html)|通过管道状态搜索管道。|

## 水印模板接口 {#section_h31_h5m_x2b .section}

|API|描述|
|:--|:-|
|[AddWaterMarkTemplate](https://help.aliyun.com/document_detail/29245.html)|创建水印模板。|
|[UpdateWaterMarkTemplate](https://help.aliyun.com/document_detail/29246.html)|更新指定水印模板的名称、配置。|
|[QueryWaterMarkTemplateList](https://help.aliyun.com/document_detail/29247.html)|查询水印模板接口。|
|[SearchWaterMarkTemplate](https://help.aliyun.com/document_detail/29248.html)|搜索指定状态的水印模板。|
|[DeleteWaterMarkTemplate](https://help.aliyun.com/document_detail/29249.html)|删除水印模板接口。|

## 截图接口 {#section_zt1_35m_x2b .section}

|API|描述|
|:--|:-|
|[SubmitSnapshotJob](https://help.aliyun.com/document_detail/29232.html)|提交截图作业接口，目前支持生成jpg格式图片。|
|[QuerySnapshotJobList](https://help.aliyun.com/document_detail/29233.html)|查询截图作业结果。|

## 媒体工作流接口 {#section_vct_35m_x2b .section}

|API|描述|
|:--|:-|
|[AddMediaWorkflow](https://help.aliyun.com/document_detail/44437.html)|用于新增媒体工作流。|
|[ActivateMediaWorkflow](https://help.aliyun.com/document_detail/44445.html)|激活媒体工作流。|
|[DeactivateMediaWorkflow](https://help.aliyun.com/document_detail/44446.html)|停用媒体工作流。|
|[DeleteMediaWorkflow](https://help.aliyun.com/document_detail/44444.html)|删除媒体工作流。|
|[UpdateMediaWorkflow](https://help.aliyun.com/document_detail/44438.html)|用于更新媒体工作流的拓扑结构。|
|[QueryMediaWorkflowList](https://help.aliyun.com/document_detail/44442.html)|查询已注册媒体工作流。|
|[SearchMediaWorkflow](https://help.aliyun.com/document_detail/44443.html)|搜索媒体工作流。|
|[UpdateMediaWorkflowTriggerMode](https://help.aliyun.com/document_detail/29226.html)|更新媒体工作流触发模式。|

## 媒体工作流执行实例接口 {#section_xbr_j5m_x2b .section}

|API|描述|
|:--|:-|
|[ListMediaWorkflowExecutions](https://help.aliyun.com/document_detail/44450.html)|遍历媒体工作流执行实例。|
|[QueryMediaWorkflowExecutionList](https://help.aliyun.com/document_detail/44449.html)|查询媒体工作流执行实例。|

## 媒体接口 {#section_dsx_k5m_x2b .section}

|API|描述|
|:--|:-|
|[AddMedia](https://help.aliyun.com/document_detail/44458.html)|新增媒体。|
|[DeleteMedia](https://help.aliyun.com/document_detail/44467.html)|删除媒体。|
|[UpdateMedia](https://help.aliyun.com/document_detail/44464.html)|更新媒体基本信息，如标题，描述，类目等。|
|[UpdateMediaCategory](https://help.aliyun.com/document_detail/44465.html)|更新媒体类目。|
|[UpdateMediaCover](https://help.aliyun.com/document_detail/44466.html)|更新媒体封面。|
|[AddMediaTag](https://help.aliyun.com/document_detail/44468.html)|新增媒体标签。|
|[DeleteMediaTag](https://help.aliyun.com/document_detail/44469.html)|删除媒体标签。|
|[UpdateMediaPublishState](https://help.aliyun.com/document_detail/44463.html)|更新媒体发布状态。|
|[QueryMediaList](https://help.aliyun.com/document_detail/44459.html)|查询媒体列表。|
|[QueryMediaListByURL](https://help.aliyun.com/document_detail/44460.html)|使用OSS文件地址查询媒体。|
|[ListMedia](https://help.aliyun.com/document_detail/52810.html)|遍历所有的媒体。|

## 媒体类目接口 {#section_djm_l5m_x2b .section}

|API|描述|
|:--|:-|
|[AddCategory](https://help.aliyun.com/document_detail/44471.html)|新增类目。|
|[DeleteCategory](https://help.aliyun.com/document_detail/44475.html)|删除类目。|
|[UpdateCategoryName](https://help.aliyun.com/document_detail/44472.html)|更新类目。|
|[CategoryTree](https://help.aliyun.com/document_detail/44474.html)|获取类目树。|
|[ListAllCategory](https://help.aliyun.com/document_detail/44473.html)|获取类目列表。|

## 媒体Bucket接口 {#section_p3h_m5m_x2b .section}

|API|描述|
|:--|:-|
|[BindInputBucket](https://help.aliyun.com/document_detail/44478.html)|媒体库绑定输入Bucket。|
|[BindOutputBucket](https://help.aliyun.com/document_detail/44479.html)|媒体库绑定输出Bucket。|
|[ListAllMediaBucket](https://help.aliyun.com/document_detail/44480.html)|列出媒体库所有媒体Bucket。|

