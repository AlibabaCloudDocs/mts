# Query media - Use OSS file address {#concept_lxf_lld_z2b .concept}

If you do not know the media ID \(a live video converted to an on-demand video using the media workflow\), you can use the media input URL to query the media information over QueryMediaListByURL.

```
import json
from aliyunsdkmts.request.v20140618 import QueryMediaListByURLRequest
from aliyunsdkcore import client
import urllib
region = '<region>'
access_key_id = '<accessKeyId>'
access_key_secret = '<accessKeySecret>'
def queryMediaListByURL():
    global client
    client = client.AcsClient(access_key_id, access_key_secret, region)
    request = QueryMediaListByURLRequest.QueryMediaListByURLRequest()
    ossDomain = 'http://<input-bucket>.<region>.aliyuncs.com/';
    #Encode ossObject
    ossObject = encodeByRFC3986("test/The Legend of the Swordsman.mp4")
    request.set_FileURLs(ossDomain + ossObject)
    response = client.do_action_with_exception(request);
    json_response = json.loads(response)
    print json_response
def encodeByRFC3986(ossObject):
    return urllib.quote(ossObject)
if __name__ == "__main__":
    queryMediaListByURL()
```

