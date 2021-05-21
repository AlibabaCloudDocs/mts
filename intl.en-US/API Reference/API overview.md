# API overview

## MediaInfo APIs

|API|Description|
|:--|:----------|
|[SubmitMediaInfoJob](/intl.en-US/API Reference/MediaInfo APIs/SubmitMediaInfoJob.md)|Submits a media information task.|
|[QueryMediaInfoJobList](/intl.en-US/API Reference/MediaInfo APIs/QueryMediaInfoJobList.md)|Queries information about MediaInfo tasks.|

## Preset smart template recommended APIs

|API|Description|
|:--|:----------|
|[SubmitAnalysisJob](/intl.en-US/API Reference/Preset smart template recommended APIs/SubmitAnalysisJob.md)|Intelligently analyzes the input file to recommend a preset template suitable for the input file.|
|[QueryAnalysisJobList](/intl.en-US/API Reference/Preset smart template recommended APIs/QueryAnalysisJobList.md)|Lists available preset templates.|

## Transcoding APIs

|API|Description|
|:--|:----------|
|[SubmitJobs](/intl.en-US/API Reference/Transcoding APIs/SubmitJobs.md)|Submits transcoding tasks.|
|[CancelJob](/intl.en-US/API Reference/Transcoding APIs/CancelJob.md)|Cancels transcoding tasks.|
|[QueryJobList](/intl.en-US/API Reference/Transcoding APIs/QueryJobList.md)|Queries transcoding tasks in batches by transcoding task ID.|
|[ListJob](/intl.en-US/API Reference/Transcoding APIs/ListJob.md)|Lists transcoding tasks by task status, creation time range, and transcoding MPS queue.|

## Custom transcoding template APIs

|API|Description|
|:--|:----------|
|[AddTemplate](/intl.en-US/API Reference/Custom transcoding template APIs/AddTemplate.md)|Creates a custom template.|
|[UpdateTemplate](/intl.en-US/API Reference/Custom transcoding template APIs/UpdateTemplate.md)|Updates custom template settings.|
|[QueryTemplateList](/intl.en-US/API Reference/Custom transcoding template APIs/QueryTemplateList.md)|Queries custom templates.|
|[SearchTemplate](/intl.en-US/API Reference/Custom transcoding template APIs/SearchTemplate.md)|Searches for custom templates in the specified state.|
|[DeleteTemplate](/intl.en-US/API Reference/Custom transcoding template APIs/DeleteTemplate.md)|Deletes a custom template.|

## MPS queue APIs

|API|Description|
|:--|:----------|
|[UpdatePipeline](/intl.en-US/API Reference/MPS queue APIs/UpdatePipeline.md)|Updates an MPS queue.|
|[QueryPipelineList](/intl.en-US/API Reference/MPS queue APIs/QueryPipelineList.md)|Queries MPS queues.|
|[SearchPipeline](/intl.en-US/API Reference/MPS queue APIs/SearchPipeline.md)|Searches for MPS queues by MPS queue status.|

## Watermark template APIs

|API|Description|
|:--|:----------|
|[AddWaterMarkTemplate](/intl.en-US/API Reference/Watermark template APIs/AddWaterMarkTemplate.md)|Creates a watermark template.|
|[UpdateWaterMarkTemplate](/intl.en-US/API Reference/Watermark template APIs/UpdateWaterMarkTemplate.md)|Updates the name and configurations of a specified watermark template.|
|[QueryWaterMarkTemplateList](/intl.en-US/API Reference/Watermark template APIs/QueryWaterMarkTemplateList.md)|Queries details about watermark templates by watermark template ID.|
|[SearchWaterMarkTemplate](/intl.en-US/API Reference/Watermark template APIs/SearchWaterMarkTemplate.md)|Searches for watermark templates in the specified state.|
|[DeleteWaterMarkTemplate](/intl.en-US/API Reference/Watermark template APIs/DeleteWaterMarkTemplate.md)|Deletes a watermark template.|

## Screenshot APIs

|API|Description|
|:--|:----------|
|[SubmitSnapshotJob](/intl.en-US/API Reference/Screenshot APIs/SubmitSnapshotJob.md)|Submits screenshot tasks, currently supports jpg format.|
|[QuerySnapshotJobList](/intl.en-US/API Reference/Screenshot APIs/QuerySnapshotJobList.md)|Queries the screenshot task results.|

## Media workflow APIs

|API|Description|
|:--|:----------|
|[AddMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/AddMediaWorkflow.md)|Adds a media workflow and defines the topology of the media workflow.|
|[ActivateMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/ActivateMediaWorkflow.md)|Activates a media workflow.|
|[DeactivateMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/DeactivateMediaWorkflow.md)|Disables a media workflow.|
|[DeleteMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/DeleteMediaWorkflow.md)|Deletes a media workflow.|
|[UpdateMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/UpdateMediaWorkflow.md)|Updates the topology of a media workflow.|
|[QueryMediaWorkflowList](/intl.en-US/API Reference/Media workflow APIs/QueryMediaWorkflowList.md)|Queries registered media workflows.|
|[SearchMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/SearchMediaWorkflow.md)|Searches for media workflows.|
|[UpdateMediaWorkflowTriggerMode](/intl.en-US/API Reference/Media workflow APIs/UpdateMediaWorkflowTriggerMode.md)|Update the trigger mode of media workflow.|

## Media workflow execution instance APIs

|API|Description|
|:--|:----------|
|[ListMediaWorkflowExecutions](/intl.en-US/API Reference/Media workflow execution instance APIs/ListMediaWorkflowExecutions.md)|Lists all media workflow execution instances.|
|[QueryMediaWorkflowExecutionList](/intl.en-US/API Reference/Media workflow execution instance APIs/QueryMediaWorkflowExecutionList.md)|Queries media workflow execution instances.|

## Media APIs

|API|Description|
|:--|:----------|
|[AddMedia](/intl.en-US/API Reference/Media APIs/AddMedia.md)|Adds media.|
|[DeleteMedia](/intl.en-US/API Reference/Media APIs/DeleteMedia.md)|Deletes media.|
|[UpdateMedia](/intl.en-US/API Reference/Media APIs/UpdateMedia.md)|Updates media set basic information, such as the title, description, and category.|
|[UpdateMediaCategory](/intl.en-US/API Reference/Media APIs/UpdateMediaCategory.md)|Updates media categories.|
|[UpdateMediaCover](/intl.en-US/API Reference/Media APIs/UpdateMediaCover.md)|Updates the media cover.|
|[AddMediaTag](/intl.en-US/API Reference/Media APIs/AddMediaTag.md)|Adds a media tag.|
|[DeleteMediaTag](/intl.en-US/API Reference/Media APIs/DeleteMediaTag.md)|Deletes a media tag.|
|[UpdateMediaPublishState](/intl.en-US/API Reference/Media APIs/UpdateMediaPublishState.md)|Updates the status of media publishing.|
|[QueryMediaList](/intl.en-US/API Reference/Media APIs/QueryMediaList.md)|Queries media sets by media IDs.|
|[QueryMediaListByURL](/intl.en-US/API Reference/Media APIs/QueryMediaListByURL.md)|Queries media sets by OSS file URLs.|

## Media bucket APIs

|API|Description|
|:--|:----------|
|[BindInputBucket](/intl.en-US/API Reference/Media bucket APIs/BindInputBucket.md)|Binds the library to the input media bucket.|
|[BindOutputBucket](/intl.en-US/API Reference/Media bucket APIs/BindOutputBucket.md)|Binds the library to the output media bucket.|
|[ListAllMediaBucket](/intl.en-US/API Reference/Media bucket APIs/ListAllMediaBucket.md)|Lists all the media buckets in the library.|

