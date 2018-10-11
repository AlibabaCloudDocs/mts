# API overview {#reference_vxd_1sm_x2b .reference}

## MediaInfo APIs {#section_qxt_bsm_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitMediaInfoJob](reseller.en-US/API Reference/MediaInfo APIs/SubmitMediaInfoJob.md#)|Submits a media information task.|
|[QueryMediaInfoJobList](reseller.en-US/API Reference/MediaInfo APIs/QueryMediaInfoJobList.md#)|Queries information about MediaInfo tasks.|

## Preset smart template recommended APIs {#section_e2m_jsm_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitAnalysisJob](reseller.en-US/API Reference/Preset smart template recommended APIs/SubmitAnalysisJob.md#)|Intelligently analyzes the input file to recommend a preset template suitable for the input file。|
|[QueryAnalysisJobList](reseller.en-US/API Reference/Preset smart template recommended APIs/QueryAnalysisJobList.md#)|Lists available preset templates.|

## Transcoding APIs {#section_c5c_b5m_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitJobs](reseller.en-US/API Reference/Transcoding APIs/SubmitJobs.md#)|Submits transcoding tasks.|
|[CancelJob](reseller.en-US/API Reference/Transcoding APIs/CancelJob.md#)|Cancels transcoding tasks.|
|[QueryJobList](reseller.en-US/API Reference/Transcoding APIs/QueryJobList.md#)|Queries transcoding tasks in batches by transcoding task ID.|
|[ListJob](reseller.en-US/API Reference/Transcoding APIs/ListJob.md#)|Lists transcoding tasks by task status, creation time range, and transcoding MPS queue.|

## Custom transcoding template APIs {#section_ncd_f5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddTemplate](reseller.en-US/API Reference/Custom transcoding template APIs/AddTemplate.md#)|Creates a custom template.|
|[UpdateTemplate](reseller.en-US/API Reference/Custom transcoding template APIs/UpdateTemplate.md#)|Updates custom template settings.|
|[QueryTemplateList](reseller.en-US/API Reference/Custom transcoding template APIs/QueryTemplateList.md#)|Queries custom templates.|
|[SearchTemplate](reseller.en-US/API Reference/Custom transcoding template APIs/SearchTemplate.md#)|Searches for custom templates in the specified state.|
|[DeleteTemplate](reseller.en-US/API Reference/Custom transcoding template APIs/DeleteTemplate.md#)|Deletes a custom template.|

## MPS queue APIs {#section_wvl_g5m_x2b .section}

|API|Description|
|:--|:----------|
|[UpdatePipeline](reseller.en-US/API Reference/MPS queue APIs/UpdatePipeline.md#)|Updates an MPS queue.|
|[QueryPipelineList](reseller.en-US/API Reference/MPS queue APIs/QueryPipelineList.md#)|Queries MPS queues.|
|[SearchPipeline](reseller.en-US/API Reference/MPS queue APIs/SearchPipeline.md#)|Searches for MPS queues by MPS queue status.|

## Watermark template APIs {#section_h31_h5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddWaterMarkTemplate](reseller.en-US/API Reference/Watermark template APIs/AddWaterMarkTemplate.md#)|Creates a watermark template.|
|[UpdateWaterMarkTemplate](reseller.en-US/API Reference/Watermark template APIs/UpdateWaterMarkTemplate.md#)|Updates the name and configurations of a specified watermark template.|
|[QueryWaterMarkTemplateList](reseller.en-US/API Reference/Watermark template APIs/QueryWaterMarkTemplateList.md#)|Queries details about watermark templates by watermark template ID.|
|[SearchWaterMarkTemplate](reseller.en-US/API Reference/Watermark template APIs/SearchWaterMarkTemplate.md#)|Searches for watermark templates in the specified state.|
|[DeleteWaterMarkTemplate](reseller.en-US/API Reference/Watermark template APIs/DeleteWaterMarkTemplate.md#)|Deletes a watermark template.|

## Screenshot APIs {#section_zt1_35m_x2b .section}

|API|Description|
|:--|:----------|
|[SubmitSnapshotJob](reseller.en-US/API Reference/Screenshot APIs/SubmitSnapshotJob.md#)|Submits screenshot tasks, currently supports jpg format.|
|[QuerySnapshotJobList](reseller.en-US/API Reference/Screenshot APIs/QuerySnapshotJobList.md#)|Queries the screenshot task results.|

## Media workflow APIs {#section_vct_35m_x2b .section}

|API|Description|
|:--|:----------|
|[AddMediaWorkflow](reseller.en-US/API Reference/Media workflow APIs/AddMediaWorkflow.md#)|Adds a media workflow and defines the topology of the media workflow.|
|[ActivateMediaWorkflow](reseller.en-US/API Reference/Media workflow APIs/ActivateMediaWorkflow.md#)|Activates a media workflow.|
|[DeactivateMediaWorkflow](reseller.en-US/API Reference/Media workflow APIs/DeactivateMediaWorkflow.md#)|Disables a media workflow.|
|[DeleteMediaWorkflow](reseller.en-US/API Reference/Media workflow APIs/DeleteMediaWorkflow.md#)|Deletes a media workflow.|
|[UpdateMediaWorkflow](reseller.en-US/API Reference/Media workflow APIs/UpdateMediaWorkflow.md#)|Updates the topology of a media workflow.|
|[QueryMediaWorkflowList](reseller.en-US/API Reference/Media workflow APIs/QueryMediaWorkflowList.md#)|Queries registered media workflows.|
|[SearchMediaWorkflow](reseller.en-US/API Reference/Media workflow APIs/SearchMediaWorkflow.md#)|Searches for media workflows.|
|[UpdateMediaWorkflowTriggerMode](reseller.en-US/API Reference/Media workflow APIs/UpdateMediaWorkflowTriggerMode.md#)|Update the trigger mode of media workflow.|

## Media workflow execution instance APIs {#section_xbr_j5m_x2b .section}

|API|Description|
|:--|:----------|
|[ListMediaWorkflowExecutions](reseller.en-US/API Reference/Media workflow execution instance APIs/ListMediaWorkflowExecutions.md#)|Lists all media workflow execution instances.|
|[QueryMediaWorkflowExecutionList](reseller.en-US/API Reference/Media workflow execution instance APIs/QueryMediaWorkflowExecutionList.md#)|Queries media workflow execution instances.|

## Media APIs {#section_dsx_k5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddMedia](reseller.en-US/API Reference/Media APIs/AddMedia.md#)|Adds media.|
|[DeleteMedia](reseller.en-US/API Reference/Media APIs/DeleteMedia.md#)|Deletes media.|
|[UpdateMedia](reseller.en-US/API Reference/Media APIs/UpdateMedia.md#)|Updates media set basic information, such as the title, description, and category.|
|[UpdateMediaCategory](reseller.en-US/API Reference/Media APIs/UpdateMediaCategory.md#)|Updates media categories.|
|[UpdateMediaCover](reseller.en-US/API Reference/Media APIs/UpdateMediaCover.md#)|Updates the media cover.|
|[AddMediaTag](reseller.en-US/API Reference/Media APIs/AddMediaTag.md#)|Adds a media tag.|
|[DeleteMediaTag](reseller.en-US/API Reference/Media APIs/DeleteMediaTag.md#)|Deletes a media tag.|
|[UpdateMediaPublishState](reseller.en-US/API Reference/Media APIs/UpdateMediaPublishState.md#)|Updates the status of media publishing.|
|[QueryMediaList](reseller.en-US/API Reference/Media APIs/QueryMediaList.md#)|Queries media sets by media IDs.|
|[QueryMediaListByURL](reseller.en-US/API Reference/Media APIs/QueryMediaListByURL.md#)|Queries media sets by OSS file URLs.|
|[ListMedia](reseller.en-US/API Reference/Media APIs/ListMedia.md#)|Lists all media resources.|

## Media category APIs {#section_djm_l5m_x2b .section}

|API|Description|
|:--|:----------|
|[AddCategory](reseller.en-US/API Reference/Media category APIs/The AddCategory API adds a category..md#)|Adds a category.|
|[DeleteCategory](reseller.en-US/API Reference/Media category APIs/DeleteCategory.md#)|Deletes a category.|
|[UpdateCategoryName](reseller.en-US/API Reference/Media category APIs/UpdateCategoryName.md#)|Update a category name.|
|[CategoryTree](reseller.en-US/API Reference/Media category APIs/CategoryTree.md#)|Retrieves a category tree.|
|[ListAllCategory](reseller.en-US/API Reference/Media category APIs/ListAllCategory.md#)|Retrieves a category list.|

## Media bucket APIs {#section_p3h_m5m_x2b .section}

|API|Description|
|:--|:----------|
|[BindInputBucket](reseller.en-US/API Reference/Media bucket APIs/BindInputBucket.md#)|Binds the library to the input media bucket.|
|[BindOutputBucket](reseller.en-US/API Reference/Media bucket APIs/BindOutputBucket.md#)|Binds the library to the output media bucket.|
|[ListAllMediaBucket](reseller.en-US/API Reference/Media bucket APIs/ListAllMediaBucket.md#)|Lists all the media buckets in the library.|

