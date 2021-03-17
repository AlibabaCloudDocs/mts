# 创建HLS标准加密工作流

本文介绍了Node.js SDK，HLS数据加密的使用场景和使用限制，并提供了完整的代码示例。

## 简介

示例调用API进行创建HLS标准加密工作流。创建工作流，请参见[t11442.md\#](/cn.zh-CN/API参考/媒体工作流接口/新增媒体工作流.md)。

## 示例代码

```
const base64url = require('base64-url');
var RPCClient = require('@alicloud/pop-core').RPCClient;

var REGION_ID = "xxx";
var ACCESS_KEY_ID = "xxx";
var ACCESS_KEY_SECRET = "xxx";
var PIPELINE_ID = "xxx";
var TEMPLATE_ID = "S00000001-100020"; //转码模版ID，m3u8模版，按需配置
var OSS_LOCATION = "xxx";
var INPUT_BUCKET = "xxx"; //输入bucket
var INPUT_PATH = "xxx"; //如 "HLS-Encryption"
var OUTPUT_BUCKET = "xxx"; //输出bucket
var ENCRYPTION_TYPE = "hls-aes-128";
var HLS_KEY_URI = "xxx"; //如http://decrypt.testdomain.com
var ACT_START = "Act-Start";
var ACT_ENCRYPTION = "Act-HLS-Encryption";
var ACT_REPORT = "Act-Report";

function initMtsClient(accessKeyId, accessKeySecret, regionId) {
    var client = new RPCClient({
        accessKeyId: accessKeyId,
        accessKeySecret: accessKeySecret,
        endpoint: 'http://mts.' + regionId + '.aliyuncs.com',
        apiVersion: '2014-06-18'
    });

    return client;
}

function addMediaWorkflow() {
    var client = initMtsClient(ACCESS_KEY_ID, ACCESS_KEY_SECRET, REGION_ID);
    var workflow = createWorkflow();
    var response = client.request("AddMediaWorkflow", {
        Name: "HLSWorkFlow1",
        Topology: JSON.stringify(workflow)
    }).then(function (response) {
        console.log("success");
        console.log(JSON.stringify(response));
    }).catch(function (response) {
        console.log(JSON.stringify(response));
    });
}

function createWorkflow() {
    var workflow = {};
    var activities = {};
    activities[ACT_START] = createStartActivity();
    activities[ACT_ENCRYPTION] = createTrancodeActivity();
    activities[ACT_REPORT] = createReportActivity();
    workflow.Activities = activities;
    workflow.Dependencies = createDependencies();
    return workflow;
}

function createStartActivity() {
    var startActivity = {};
    startActivity.Name = ACT_START;
    startActivity.Type = "Start";
    startActivity.Parameters = buildStartParameters();
    return startActivity;
}

function buildStartParameters() {
    var parameters = {};
    parameters.PipelineId = PIPELINE_ID;
    parameters.InputFile = buildInputFile();
    return parameters;
}

function buildInputFile() {
    var inputFile = {};
    inputFile.Bucket = INPUT_BUCKET;
    inputFile.Location = OSS_LOCATION;
    inputFile.ObjectPrefix = INPUT_PATH;
    return inputFile;
};

function createTrancodeActivity() {
    var transcodeActivity = {};
    transcodeActivity.Name = ACT_ENCRYPTION;
    transcodeActivity.Type = "Transcode";
    transcodeActivity.Parameters = buildTranscodeParameters();
    return transcodeActivity;
}

function buildTranscodeParameters() {
    var transcodeParamters = {};
    transcodeParamters.OutputBucket = OUTPUT_BUCKET;
    transcodeParamters.OutputLocation = OSS_LOCATION;
    transcodeParamters.Outputs = buildOutputsConfig();
    return transcodeParamters;
}

function buildOutputsConfig() {
    var output = {};
    output.ObjectRegex = ACT_ENCRYPTION.concat('/{RunId}/{FileName}');
    output.TemplateId = TEMPLATE_ID;
    output.Encryption = buildEncryption();
    var outputs = new Array();
    outputs.push(output);
    outputs = JSON.parse(JSON.stringify(outputs));
    return outputs;
}

function buildEncryption() {
    var encryption = {};
    encryption.Type = ENCRYPTION_TYPE;
    encryption.KeyUri = HLS_KEY_URI;
    // console.log("here is "+ JSON.stringify(encryption));
    return encryption;
}

function createReportActivity() {
    var reportActivity = {};
    reportActivity.Name = ACT_REPORT;
    reportActivity.Parameters = {};
    reportActivity.Type = "Report";
    return reportActivity;
}

function createDependencies() {
    var dependencies = {};
    var subActivityOfStart = new Array();
    subActivityOfStart.push(ACT_ENCRYPTION);
    subActivityOfStart = JSON.parse(JSON.stringify(subActivityOfStart));
    dependencies[ACT_START] = subActivityOfStart;
    var subActivityOfTranscode = new Array();
    subActivityOfTranscode.push(ACT_REPORT);
    subActivityOfTranscode = JSON.parse(JSON.stringify(subActivityOfTranscode));
    dependencies[ACT_ENCRYPTION] = subActivityOfTranscode;
    dependencies[ACT_REPORT] = JSON.parse(JSON.stringify(new Array()));
    return dependencies;
}

addMediaWorkflow();
```

