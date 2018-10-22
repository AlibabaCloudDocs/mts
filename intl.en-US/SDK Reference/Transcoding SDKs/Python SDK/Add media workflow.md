# Add media workflow {#concept_jr5_pnd_z2b .concept}

The user can assemble activities provided by MPS, such as transcode activity and screenshot activity into a topology. The topology is as follows:

```
import json
from aliyunsdkcore.acs_exception.exceptions import ServerException
from aliyunsdkmts.request.v20140618 import AddMediaWorkflowRequest
from aliyunsdkcore import client
import urllib
import thread
# Step 1 set region
REGION = "cn-shenzhen";
OSS_REGION = "oss-cn-shenzhen";
mtsEndpoint = "mts." + REGION + ".aliyuncs.com";
# Step 2.set accesskey & keySecret
accessKeyId = "";
accessKeySecret = "";
# Step 3.set mps transcoding queue id
PIPELINE_ID = "38bba54d524448be92d277caaa8da118";
cl = client.AcsClient(accessKeyId, accessKeySecret, REGION)
def addMeidaWorkflow():
    request = AddMediaWorkflowRequest.AddMediaWorkflowRequest()
    request.set_Name("Sequential-workflow");
    startActivity = {
        "Type": "Start",
        "Parameters": {
            "InputFile": {
                "Bucket": "mtb-sz-in",
                "Location": OSS_REGION,
                "ObjectPrefix": "media/"
            },
            "PipelineId": PIPELINE_ID
        }
    }
    transcodeActivity = {
        "Type": "Transcode",
        "Parameters": {
            "Outputs": [
                {
                    "OutputObject": encodeByRFC3986("transcode/{ObjectPrefix}/{FileName}.{ ExtName}"),
                    "TemplateId": "S00000001-000070"
                }
            ],
            "OutputLocation": OSS_REGION,
            "OutputBucket": "mtb-sz-out"
        }
    }
    reportActivity = {
        "Type": "Report",
        "Parameters": {
        }
    }
    topology = {
        "Activities": {
            "startNode": startActivity,
            "transcodingNode": transcodeActivity,
            "reportNode": reportActivity
        },
        "Dependencies": {
            "startNode": ["transcodingNode"],
            "transcodingNode": ["reportNode"],
            "reportNode": []
        }
    }
    request.set_Topology(topology)
    try:
        response = json.loads(cl.do_action_with_exception(request))
        print json.dumps(response)
    except ServerException, e:
        print e.get_error_code(), e.get_error_msg()
def encodeByRFC3986(ossObject):
    return urllib.quote(ossObject)
if __name__ == "__main__":
    addMeidaWorkflow()
```

