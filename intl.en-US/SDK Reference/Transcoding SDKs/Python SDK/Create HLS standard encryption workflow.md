# Create HLS standard encryption workflow {#concept_opz_wld_z2b .concept}

## Introduction {#section_dr1_hmd_z2b .section}

This document is an example of calling API to create HLS standard encryption workflow. For more information about creating HLS standard encryption workflow and playing encryption videos, see [HLS encryption and play](https://help.aliyun.com/document_detail/68565.html). For more information about MPS SDK, see [Installation](https://help.aliyun.com/document_detail/55746.html).

## Example {#section_if1_jmd_z2b .section}

```
import json
from aliyunsdkmts.request.v20140618 import AddMediaWorkflowRequest
from aliyunsdkcore import client
REGION_ID = '<region>'
ACCESS_KEY_ID = '<accessKeyId>'
ACCESS_KEY_SECRET = '<accessKeySecret>'
PIPELINE_ID = "<PipelineId>"
TEMPLATE_ID = "S00000001-100020" #Transcoding template ID, m3u8 template, set as needed
OSS_LOCATION = "<OssLocation>"
INPUT_BUCKET = "<InputBucket>"
INPUT_PATH = "<InputPath>" ##Example: "HLS-Encryption"
OUTPUT_BUCKET = "<OutputBucket>"
ENCRYPTION_TYPE = "hls-aes-128"
HLS_KEY_URI = "<URI of decryption key>" #Example: http://decrypt.testdomain.com
ACT_START = "Act-Start"
ACT_ENCRYPTION = "Act-HLS-Encryption"
ACT_REPORT = "Act-Report"
def addMediaWorkflow():
    global client
    client = client.AcsClient(ACCESS_KEY_ID, ACCESS_KEY_SECRET, REGION_ID)
    request = AddMediaWorkflowRequest.AddMediaWorkflowRequest()
    request.set_Topology(buildWorkflowTopology())
    request.set_Name("HLS encryption workflow py")
    response = client.do_action_with_exception(request)
    print json.loads(response)
def buildWorkflowTopology():
    workflow = {}
    workflow["Activities"] = buildActivities()
    workflow["Dependencies"] = buildDependencies()
    print json.dumps(workflow)
    return json.dumps(workflow)
def buildActivities():
    activities = {}
    activities[ACT_START] = buildStartActivity()
    activities[ACT_ENCRYPTION] = buildTranscodeActivity()
    activities[ACT_REPORT] = buildReportActivity()
    return activities
def buildStartActivity():
    startActivity = {}
    startActivity["Name"] = ACT_START
    startActivity["Type"] = "Start"
    startActivity["Parameters"] = buildStartParameters()
    return startActivity
def buildStartParameters():
    startParameters = {}
    startParameters["PipelineId"] = PIPELINE_ID
    startParameters["InputFile"] = buildInputFile();
    return startParameters
def buildInputFile():
    inputFile = {}
    inputFile["Bucket"] = INPUT_BUCKET
    inputFile["Location"] = OSS_LOCATION
    inputFile["ObjectPrefix"] = INPUT_PATH
    return inputFile
def buildTranscodeActivity():
    transcodeActivity = {}
    transcodeActivity["Name"] = ACT_ENCRYPTION
    transcodeActivity["Type"] = "Transcode"
    transcodeActivity["Parameters"] = buildTranscodeParameters()
    return transcodeActivity
def buildTranscodeParameters():
    transcodeParameters = {}
    transcodeParameters["OutputBucket"] = OUTPUT_BUCKET
    transcodeParameters["OutputLocation"] = OSS_LOCATION
    transcodeParameters["Outputs"] = buildOutputsConfig()
    return transcodeParameters
def buildOutputsConfig():
    outputs = []
    output = {}
    output["ObjectRegex"] = ACT_ENCRYPTION + "/{RunId}/{FileName}"
    output["TemplateId"] = TEMPLATE_ID
    output["Encryption"] = buildEncryption()
    outputs.append(output)
    return outputs
def buildEncryption():
    encryption = {}
    encryption["Type"] = ENCRYPTION_TYPE
    encryption["KeyUri"] = HLS_KEY_URI
    return encryption
def buildReportActivity():
    reportActivity = {}
    reportActivity["Name"] = ACT_REPORT
    reportActivity["Parameters"] = buildReportParameters()
    reportActivity["Type"] = "Report"
    return reportActivity
def buildReportParameters():
    parameters = {}
    parameters["PublishType"] = "Auto"
    return parameters
def buildDependencies():
    dependencies ={}
    subActivityOfStart = [ACT_ENCRYPTION]
    dependencies[ACT_START] = subActivityOfStart
    subActivityOfTranscode = [ACT_REPORT]
    dependencies[ACT_ENCRYPTION] = subActivityOfTranscode
    dependencies[ACT_REPORT] = []
    return dependencies
if __name__ == "__main__":
    addMediaWorkflow()
```

