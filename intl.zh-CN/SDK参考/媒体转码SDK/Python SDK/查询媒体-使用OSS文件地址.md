# 查询媒体-使用OSS文件地址 {#concept_lxf_lld_z2b .concept}

如果您不知道媒体ID（直播走工作流转点播），可以通过媒体的输入地址进行媒体信息的查询，接口为 QueryMediaListByURL。

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
    #对ossObject进行encode
    ossObject = encodeByRFC3986("test/笑傲江湖.mp4")
    request.set_FileURLs(ossDomain + ossObject)
    response = client.do_action_with_exception(request);
    json_response = json.loads(response)
    print json_response
def encodeByRFC3986(ossObject):
    return urllib.quote(ossObject)
if __name__ == "__main__":
    queryMediaListByURL()
```

