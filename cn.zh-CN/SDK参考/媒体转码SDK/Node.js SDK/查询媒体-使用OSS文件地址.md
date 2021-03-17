# 查询媒体-使用OSS文件地址

本文提供了Node.js SDK通过OSS文件地址查询媒体的完整代码示例。

## 示例代码

如果您在不知道媒体ID（直播工作流转点播），可以通过媒体的输入地址进行媒体信息的查询，接口为[查询媒体-使用OSS文件地址](/cn.zh-CN/API参考/媒体接口/查询媒体-使用OSS文件地址.md)。

```
var RPCClient = require('@alicloud/pop-core').RPCClient;

function initMtsClient(accessKeyId, accessKeySecret, regionId) {
    var client = new RPCClient({
        accessKeyId: accessKeyId,
        accessKeySecret: accessKeySecret,
        endpoint: 'http://mts.' + regionId + '.aliyuncs.com',
        apiVersion: '2014-06-18'
    });
    return client;
}


var REGION = "xxx";
var ID = "xxx"; // your accessKey
var KEY = "xxx";//your secretKey
var client = initMtsClient(ID, KEY, REGION);

//根据视频源OSS地址查询媒体信息， 如: 媒体ID, 媒体状态及其他属性
function queryMediaListByURL() {
    var ossHost = 'xxx';//比如 http://ice-auto-test-bj.oss-cn-beijing.aliyuncs.com/
    var ossObject = "xxx";
    var rfc3986Object = encodeByRFC3986(ossObject);
    console.log(rfc3986Object);
    client.request("QueryMediaListByURL", {
        FileURLs: ossHost.concat(rfc3986Object)
    }, {}).then(function (response) {
        console.log(JSON.stringify(response));
    }).catch(function (response) {
        console.log(response);
    });

}

function encodeByRFC3986(object) {
    var builder = [];
    var segments = object.split("/");
    for (var i = 0; i < segments.length; i++) {
        builder.push(percentEncode(segments[i]));
        if (i != segments.length - 1) {
            builder.push("/");
        }
    }
    return builder.join("");
}

function percentEncode(value) {
    if (typeof value == "undefined" || value == null || value == "")
        return null;
    return encodeURIComponent(value).replace("+", "%20").replace("*", "%2A").replace("%7E", "~");
}

queryMediaListByURL();
```

