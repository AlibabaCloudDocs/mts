# HLS数据加密

本文介绍了Node.js SDK，HLS数据加密的使用场景和使用限制，并提供了完整的代码示例。

## 使用场景

-   HLS标准数据加密适用于对视频进行简单的保护，可以简单的防止非法下载和非法传播。
-   如果对安全有强烈需求，请开启工作流中的数据加密。详情请参见[加密](/cn.zh-CN/开发指南/视频加密/加密.md)。

## 使用限制

-   HLS标准数据加密需要使用[提交转码作业](/cn.zh-CN/API参考/转码接口/提交转码作业.md)接口。
-   工作流中不可使用HLS标准数据加密。

## 示例代码

```
const base64url = require('base64-url');
var RPCClient = require('@alicloud/pop-core').RPCClient;

var REGION = "xxx"; //按需配置
var ID = "xxx"; //按需配置
var KEY = "xxx"; //按需配置
var LOCATION = "xxx"; //按需配置
var INPUT_BUCKET = "xxx"; //按需配置
var OUTPUT_BUCKET = "xxx"; //按需配置
var PIPELINE_ID = "xxx"; //按需配置

function initMtsClient(accessKeyId, accessKeySecret, regionId) {
    var client = new RPCClient({
        accessKeyId: accessKeyId,
        accessKeySecret: accessKeySecret,
        endpoint: 'http://mts.' + regionId + '.aliyuncs.com',
        apiVersion: '2014-06-18'
    });

    return client;
}

function DataEncryptionDemo() {
    return initMtsClient(ID, KEY, REGION);
}

function getInputFile() {
    var inputFile = {};
    inputFile.Location = LOCATION;
    inputFile.Bucket = INPUT_BUCKET;
    inputFile.Object = 'result.mp4';
    return inputFile;
}

function getOutputs() {
    var left = '[';
    var right = ']';
    var output = getOutput();
    var outputs = left.concat(JSON.stringify(output), right);
    return outputs;
}

function getOutput() {
    var output = {};
    output.OutputObject = "BaseTest/hls-encryption.m3u8";
    output.TemplateId = "S00000001-100020";
    output.Encryption = JSON.stringify(getEncryptionConfigs());
    return output;
}

function getEncryptionConfigs() {
    var encryption = {};
    encryption.Type = "hls-aes-128";
    encryption.Key = base64url.encode("encryptionkey123");
    encryption.KeyUri = base64url.encode("http://demo.aliyuncs.com/document/hls128.key");
    encryption.KeyType = "Base64";
    return encryption;
}

function submitJobs() {
    inputFile = getInputFile();
    outputs = getOutputs();
    client = DataEncryptionDemo();
    client.request('SubmitJobs', {
        Input: JSON.stringify(inputFile),
        OutputLocation: LOCATION,
        OutputBucket: OUTPUT_BUCKET,
        Outputs: outputs,
        PipelineId: PIPELINE_ID,
        OutputLocation: LOCATION
    }).then(function (response) {
        console.log(JSON.stringify(response.JobResultList));
        console.log(response.JobResultList.JobResult[0].Job.JobId);
    }).catch(function (response) {
        console.log(JSON.stringify(response));
    })
}

submitJobs();
```

