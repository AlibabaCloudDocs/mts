# API overview {#reference_vxd_1sm_x2b .reference}

## MediaInfo APIs {#section_qxt_bsm_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitMediaInfoJob](https://help.aliyun.com/document_detail/29220.html)|Submits a media information task.|
|[QueryMediaInfoJobList](https://help.aliyun.com/document_detail/29221.html)|Queries information about MediaInfo tasks.|

## Preset smart template recommended APIs {#section_e2m_jsm_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitAnalysisJob](https://help.aliyun.com/document_detail/29223.html)|Intelligently analyzes the input file to recommend a preset template suitable for the input file。|
|[QueryAnalysisJobList](https://help.aliyun.com/document_detail/29224.html)|Lists available preset templates.|

## Transcoding APIs {#section_c5c_b5m_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitJobs](https://help.aliyun.com/document_detail/29226.html)|Submits transcoding tasks.|
|[CancelJob](https://help.aliyun.com/document_detail/29227.html)|Cancels transcoding tasks.|
|[QueryJobList](https://help.aliyun.com/document_detail/29228.html)|Queries transcoding tasks in batches by transcoding task ID.|
|[ListJob](https://help.aliyun.com/document_detail/29229.html)|Lists transcoding tasks by task status, creation time range, and transcoding MPS queue.|

## Custom transcoding template APIs {#section_ncd_f5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddTemplate](https://help.aliyun.com/document_detail/29239.html)|Creates a custom template.|
|[UpdateTemplate](https://help.aliyun.com/document_detail/29240.html)|Updates custom template settings.|
|[QueryTemplateList](https://help.aliyun.com/document_detail/29241.html)|Queries custom templates.|
|[SearchTemplate](https://help.aliyun.com/document_detail/29242.html)|Searches for custom templates in the specified state.|
|[DeleteTemplate](https://help.aliyun.com/document_detail/29243.html)|Deletes a custom template.|

## MPS queue APIs {#section_wvl_g5m_x2b .section}

|API|Description|
|:--|:----------|
|[UpdatePipeline](https://help.aliyun.com/document_detail/29235.html)|Updates an MPS queue.|
|[QueryPipelineList](https://help.aliyun.com/document_detail/29236.html)|Queries MPS queues.|
|[SearchPipeline](https://help.aliyun.com/document_detail/29237.html)|Searches for MPS queues by MPS queue status.|

## Watermark template APIs {#section_h31_h5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddWaterMarkTemplate](https://help.aliyun.com/document_detail/29245.html)|Creates a watermark template.|
|[UpdateWaterMarkTemplate](https://help.aliyun.com/document_detail/29246.html)|Updates the name and configurations of a specified watermark template.|
|[QueryWaterMarkTemplateList](https://help.aliyun.com/document_detail/29247.html)|Queries details about watermark templates by watermark template ID.|
|[SearchWaterMarkTemplate](https://help.aliyun.com/document_detail/29248.html)|Searches for watermark templates in the specified state.|
|[DeleteWaterMarkTemplate](https://help.aliyun.com/document_detail/29249.html)|Deletes a watermark template.|

## Screenshot APIs {#section_zt1_35m_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitSnapshotJob](https://help.aliyun.com/document_detail/29232.html)|Submits screenshot tasks, currently supports jpg format.|
|[QuerySnapshotJobList](https://help.aliyun.com/document_detail/29233.html)|Queries the screenshot task results.|

## Media workflow APIs {#section_vct_35m_x2b .section}

|API|Description|
|:--|:----------|
|[AddMediaWorkflow](https://help.aliyun.com/document_detail/44437.html)|Adds a media workflow and defines the topology of the media workflow.|
|[ActivateMediaWorkflow](https://help.aliyun.com/document_detail/44445.html)|Activates a media workflow.|
|[DeactivateMediaWorkflow](https://help.aliyun.com/document_detail/44446.html)|Disables a media workflow.|
|[DeleteMediaWorkflow](https://help.aliyun.com/document_detail/44444.html)|Deletes a media workflow.|
|[UpdateMediaWorkflow](https://help.aliyun.com/document_detail/44438.html)|Updates the topology of a media workflow.|
|[QueryMediaWorkflowList](https://help.aliyun.com/document_detail/44442.html)|Queries registered media workflows.|
|[SearchMediaWorkflow](https://help.aliyun.com/document_detail/44443.html)|Searches for media workflows.|
|[UpdateMediaWorkflowTriggerMode](https://help.aliyun.com/document_detail/29226.html)|Update the trigger mode of media workflow.|

## Media workflow execution instance APIs {#section_xbr_j5m_x2b .section}

|API|Description|
|:--|:----------|
|[ListMediaWorkflowExecutions](https://help.aliyun.com/document_detail/44450.html)|Lists all media workflow execution instances.|
|[QueryMediaWorkflowExecutionList](https://help.aliyun.com/document_detail/44449.html)|Queries media workflow execution instances.|

## Media APIs {#section_dsx_k5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddMedia](https://help.aliyun.com/document_detail/44458.html)|Adds media.|
|[DeleteMedia](https://help.aliyun.com/document_detail/44467.html)|Deletes media.|
|[UpdateMedia](https://help.aliyun.com/document_detail/44464.html)|Updates media set basic information, such as the title, description, and category.|
|[UpdateMediaCategory](https://help.aliyun.com/document_detail/44465.html)|Updates media categories.|
|[UpdateMediaCover](https://help.aliyun.com/document_detail/44466.html)|Updates the media cover.|
|[AddMediaTag](https://help.aliyun.com/document_detail/44468.html)|Adds a media tag.|
|[DeleteMediaTag](https://help.aliyun.com/document_detail/44469.html)|Deletes a media tag.|
|[UpdateMediaPublishState](https://help.aliyun.com/document_detail/44463.html)|Updates the status of media publishing.|
|[QueryMediaList](https://help.aliyun.com/document_detail/44459.html)|Queries media sets by media IDs.|
|[QueryMediaListByURL](https://help.aliyun.com/document_detail/44460.html)|Queries media sets by OSS file URLs.|
|[ListMedia](https://help.aliyun.com/document_detail/52810.html)|Lists all media resources.|

## Media category APIs {#section_djm_l5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddCategory](https://help.aliyun.com/document_detail/44471.html)|Adds a category.|
|[DeleteCategory](https://help.aliyun.com/document_detail/44475.html)|Deletes a category.|
|[UpdateCategoryName](https://help.aliyun.com/document_detail/44472.html)|Update a category name.|
|[CategoryTree](https://help.aliyun.com/document_detail/44474.html)|Retrieves a category tree.|
|[ListAllCategory](https://help.aliyun.com/document_detail/44473.html)|Retrieves a category list.|

## Media bucket APIs {#section_p3h_m5m_x2b .section}

|API|Description|
|:--|:----------|
|[BindInputBucket](https://help.aliyun.com/document_detail/44478.html)|Binds the library to the input media bucket.|
|[BindOutputBucket](https://help.aliyun.com/document_detail/44479.html)|Binds the library to the output media bucket.|
|[ListAllMediaBucket](https://help.aliyun.com/document_detail/44480.html)|Lists all the media buckets in the library.|

