# Error code list

This article lists general errors, task errors, MPS queue errors, and message sending errors.

## General errors

|Error code|Description|Detailed information|
|:---------|:----------|:-------------------|
|Throttling|The API is throttled.|Request was denied due to request throttling.|
|InvalidIdentity.ServiceDisabled|The service is inactivated or frozen.|The request identity was not allowed operated.|
|InvalidParameter|The parameter is invalid.|The specified parameter \\”%s\\” is invalid.|
|InvalidParameter.NullValue|The parameter is blank.|The specified parameter \\”%s\\” cannot be null.|
|InvalidParameter.InvalidState|The status is invalid.|The specified parameter \\”%s\\” is invalid.|
|InvalidParameter.EmptyValue|The parameter must be set.|The specified parameter \\”%s\\” cannot be empty.|
|InvalidParameter.NotSupported|The parameter is not supported. For example, H. 265 in the custom template does not support the Profile parameter currently.|The specified parameter \\”%s\\” is not supported.|
|InternalError|There is an unknown internal error.|The operation has failed due to some unknown error, exception or failure.|
|InvalidParameter.OutOfRange|The parameter value is out of the value range.|The specified parameter \\”%s\\” is out of range.|
|InvalidParameter.ResourceNotFound|The operated resource does not exist.|The resource operated \\”%s\\” cannot be found.|
|InvalidParameter.ResourceContentBad|The operated resource content is faulty.|The resource operated \\”%s\\” is bad.|
|InvalidParameter.ResourceNotSupported|The operated resource is not supported. For example, the file extension is not supported.|The resource operated \\”%s\\” is not supported.|
|InvalidParameter.NoAudioStream|The operated resource does not have the audio stream.|The resource has no audio stream.|
|InvalidParameter.MergeFileNoVideoOrAudio|The joined file must contain both the video and audio streams.|The merge File must contain video and audio stream at the sametime.|
|PermissionDenied.ResourceAccess|Resource access permission is restricted.|MTS not authorized to operate on the specified resource \\”%s\\”.|
|PermissionDenied.ResourceQuotaExceed|The resource quota has been used up.|The resource \\”%s\\” quota has been used up.|
|InvalidParameter.ResourceDeleted|The operated resource is deleted.|The resource operated \\”%s\\” has been deleted.|
|InvalidParameter.JsonFormatInvalid|The parameter is not a valid JSON string.|The parameter \\”%s\\” does not conform to the JSON specification.|
|InvalidParameter.JsonObjectFormatInvalid|The parameter is not a valid JSON object.|The parameter \\”%s\\” does not conform to the JSON Object specification.|
|InvalidParameter.JsonArrayFormatInvalid|The parameter is not a valid JSON array string.|The parameter \\”%s\\” does not conform to the JSON Array specification.|
|InvalidParameter.UUIDFormatInvalid|The ID is invalid or is not in UUID format.|The parameter \\”%s\\” is invalid.A uuid must:1\)be comprised of chracters\[a-f\],numbers\[0-9\];2\)be 32 characters long.|
|InvalidParameter.Format|The parameter format is incorrect.|The format of parameter \\”%s\\” is invalid.|
|InvalidParameter.NumberFormatInvalid|The number format is incorrect.|The number format of parameter \\”%s\\” is invalid.|
|InvalidParameter.BucketNameInvalid|The specified bucket name does not meet the OSS bucket specifications.|The bucket name \\”%s\\” is invalid. A bucket name must: 1\) be comprised of lower-case characters, numbers, underscore\(\_\) or dash\(-\); 2\) start with lower case or numbers; 3\) be between 3-255 characters long.|
|InvalidParameter.LocationInvalid|The specified location does not meet the OSS location specifications.|The location \\”%s\\” is invalid. A location name shoud be one of five:oss-cn-hangzhou,oss-cn-qingdao,oss-cn-beijing,oss-cn-hongkong,oss-cn-shenzhen.And now MTS only support oss-cn-hangzhou.|
|InvalidParameter.ObjectKeyInvalid|The specified object name does not meet the OSS object specifications.|The object key \\”%s\\” is invalid. An object name should be between 1 - 1023 bytes long when encoded as UTF-8 and cannot contain LF or CR or unsupported chars in XML1.0.|

## Task errors

|Error code|Description|Detailed information|
|:---------|:----------|:-------------------|
|PermissionDenied.JobInComplete|You do not have the permission to cancel completed tasks.|The Job operated \\”%s\\” is complete, cannot cancel.|
|PermissionDenied.JobInFailure|You do not have the permission to cancel failed tasks.|The Job operated \\”%s\\” is failure, cannot cancel.|
|PermissionDenied.JobInRunning|You do not have the permission to cancel running tasks.|The Job operated \\”%s\\” is running, cannot cancel.|
|InvalidParameter.TemplateNotSupported|The operated template is not supported. For example, the preset template specified when you submit a task is not in the list of recommend preset templates when the intelligent analysis is successful.|The template operated \\”%s\\” is not supported.|
|InvalidParameter.TemplateNotFound|The template does not exist.|The Template operated \\”%s\\” cannot be found.|

## MPS queue errors

|Error code|Description|Detailed information|
|:---------|:----------|:-------------------|
|NotSupportedJob.SystemTemplateJobNotSupported|The Boost MPS queue does not support tasks created based on the system template.|The Template \\”%s\\” is a system template,cannot be supported by boost pipeline.|
|NotSupportedJob.AnalysisJobNotSupported|The Boost MPS queue does not support analysis tasks.|Analysis Job cannot be supported by boost pipeline.|
|NotSupportedJob.ContainerFormatNotSupported|The Boost MPS queue does not support custom templates not in M3U8 format.|In user defined template \\”%s”,container format \\”%s” is not m3u8, cannot be supported by boost pipeline.|
|NotSupportedJob.DurationIsLessThanHalfAnHour|The Boost MPS queue does not support tasks shorter than 30 minutes.|Duration is \\”%s\\” less than half an hour,cannot be supported by boost pipeline.|

## Message sending errors

|Error code|Description|Detailed information|
|:---------|:----------|:-------------------|
|EntityNotExist.Role|The role does not exist.|The role does not exist.|
|AccessDenied|You do not have the permission to send the message.|The OwnerId that your AccessKey Idassociated to is forbidden for this operation.|
|InvalidQueueName|The name of the Message Service queue is invalid.|The queue name you provided is invalid. QueueName should start with alpha and contain only alpha, digit or - .|
|TopicNameInvalid|The topic name is invalid.|The topic name you provided is invalid. TopicName should start with alpha or digit and contain only alpha, digit or -.|
|QueueNotExist|The MPS queue does not exist.|The queue name you provided does not exist.|
|TopicNotExist|The topic does not exist.|The Topic you provided does not exist.|
|InvalidArgument|The length of the message body exceeds the upper threshold.|The length of message must not be larger than MaximumMessageSize.|

