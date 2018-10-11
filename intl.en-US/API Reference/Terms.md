# Terms {#reference_p1f_z5m_x2b .reference}

|Terms|Full name|Meaning|Description|
|:----|:--------|:------|:----------|
|OSS|Object Storage Service|Alibaba Cloud Object Storage Service|MPS transcodes the media files stored in OSS and stores the output files in the media bucket or output bucket.|
|Bucket|OSS Bucket|OSS Bucket|The bucket name can only contain lower-case letters, numbers, and hyphens \(-\). It must be a string of 3 to 255 bytes which starts with a lower-case letter or number.|
|Location|OSS Location|The OSS data center|Follow the OSS location definition.|
|Object|OSS Object|OSS object|See OSS documentation for the definition. The object name can contain a UTF-8 encoded string of 1 to 1,023 bytes. A leading forward slash \(/\) or backward slash \(\\\) is not supported.|
|LocalFile|Local file|Local media files|Media file that is stored locally and has not yet been uploaded to OSS.|
|Input|Task input|Task input|Task input includes an input file and the input parameters for transcoding.|
|InputFile|Input file|Input file|After a local file is uploaded to OSS, the file is considered an input file.|
|Output|Task output|Task output|Task output contains a set of attributes such as the template ID, watermark list, and output file.|
|OutputFile|Output file|Output file|An output file is stored in OSS and uniquely identified by the output location, output bucket, and output object.|
|OutputBucket|Output bucket|Transcoding output Bucket|Bucket that stores the output file after transcoding. You must set this parameter when submitting a task during the OSS file transcoding process, and grant the output bucket write permission to Media Processing in the bucket authorization channel on the resource management page of the Media Processing console.|
|OutputLocation|Output location|Output location|A location of an output bucket in an OSS instance. You can set this parameter when you submit a task in the OSS file transcoding process.|
|Template|Transcoding template|Transcoding template|Custom template that contains a set of transcoding parameters, including audio, video, and container. Each template is identified by a unique ID.|
|PresetTemplate|Preset transcoding template|Preset transcoding template|An intelligent transcoding template inherent in Media Processing, which can be used to dynamically adjust the transcoding settings based on the features of an input file to obtain the optimal output file under specific bandwidth conditions. Not all preset templates are suitable for all input files. If you want to use a preset transcoding template, call the SubmitAnalysisJob API to trigger template analysis and call the QueryAnalysisJobList API to obtain a list of preset transcoding templates available for the input file. For a list of preset transcode templates supported by Media Processing, see “Preset transcode templates” in “Appendix.”|
|WaterMarkTemplate|Watermark template|Watermark template|A watermark consists of a variable parameter \(watermark content\) and a set of virtually unchanged parameters \(watermark position, offset, and size\). The latter parameters constitute a watermark template with a unique ID.|
|Job|Transcoding task|Transcoding task|A transcoding task consists of an input and an output. It is added to an MPS queue, where the tasks are scheduled by a scheduling engine to the transcoding system.|
|AnalysisJob|Analysis job|Analysis task|An analysis task consists of an input file and analysis settings. It is used to obtain an applicable preset template.|
|SnapshotJob|Screenshot task|Screenshot task|A screenshot task consists of an input file and screenshot settings. It is used to obtain a screenshot of the input file based on screenshot settings.|
|MediaInfoJob|MediaInfo task|MediaInfo task|A MediaInfo task is used to obtain the media information of the specified input file.|
|Pipeline|MPS queue|MPS queue|An MPS queue is a queue of tasks that can be scheduled by Media Processing to implement transcoding. If a large number of tasks exist in the MPS queue, they are queued up in waiting state. An MPS queue can be in active or suspended state. If it is in the suspended state, the queued tasks are not scheduled by Media Processing until the MPS queue enters the active state, but tasks with transcoding in progress are not affected.|
|MediaRepository|Media repository|Media repository|A media repository contains a full set of media.|
|Media|Media resource|Media resource|A media resource is the minimum management unit of the media repository. A media resource contains an input \(a video or audio multimedia file\) and all relevant outputs \(such as the transcoded file and screenshot\). A media resource has a unique ID \(MediaId\) and has a one-to-one mapping with an input file.|
|MediaWorkflow|Media workflow|Media workflow|A factory that produces media. A media workflow is a custom processing procedure starting when a multimedia file is received from the input bucket till the transcoded file is saved to the output bucket. Each media workflow is uniquely identified by a MediaWorkflowId.|
|Activity|Media workflow activity|Media workflow activity|The unit of composition of the media workflow. Activities are components of a media workflow. A media workflow can be represented by a directed acyclic graph where each node is considered an activity, which may be transcoding, screenshot taking, or metadata acquisition. Each activity has a unique name.|
|MediaWorkflowExecution|Media workflow execution instance|Media workflow execution instance|The execution of a media workflow is considered an instance. Each instance has a unique RunId.|
|MediaBucket|Media bucket|Media bucket|The media repository is associated with multiple media buckets that store media files. Media buckets are classified into input media bucket and output media bucket, which must be non-overlapping OSS buckets and independent of each other.|
|InputMediaBucket|Input media bucket|Input media bucket|After a multimedia file is added to an input media bucket, the file is automatically added to the media repository; if the file matches the input conditions of a media workflow, the media workflow is automatically executed.|
|OutputMediaBucket|Output media bucket|Output media bucket|The output media bucket stores the output file that is generated after a media workflow is executed.|
| | | | |
| | | | |
| | | | |

