# Add media {#concept_kfg_rld_z2b .concept}

Add a video file to MEdia Files, and the user can specify workflow to be triggered to process this file:

```
import json
from aliyunsdkcore.acs_exception.exceptions import ServerException, ClientException
from aliyunsdkmts.request.v20140618 import AddMediaRequest
from aliyunsdkcore import client
import urllib
import thread
# Step 1 set region
REGION = "cn-shenzhen";
mtsEndpoint = "mts." + REGION + ".aliyuncs.com";
# Step 2.set accesskey & keySecret
accessKeyId = "";
accessKeySecret = "";
cli = client.AcsClient(accessKeyId, accessKeySecret, REGION)
def addMeida():
    request = AddMediaRequest.AddMediaRequest()
    request.set_FileURL("http://mtb-sz-in.oss-cn-shenzhen.aliyuncs.com/media/r180-ABC.mp4")
    request.set_MediaWorkflowId("829bed0300994057a49e4f16de957e34")
    try:
        response = cli.do_action_with_exception(request)
        json_response = json.loads(response)
        print json.dumps(json_response)
    except ServerException, e:
        print e.get_error_code(), e.get_error_msg()
    except ClientException, e:
        print e.get_error_code(), e.get_error_msg()
def encodeByRFC3986(ossObject):
    return urllib.quote(ossObject)
if __name__ == "__main__":
    addMeida()
```

