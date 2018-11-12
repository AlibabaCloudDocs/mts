# 创建Python版ChinaDRM工作流 {#concept_tmh_yyg_tfb .concept}

本文介绍如何创建Python版ChinaDRM工作流。

## 使用限制 {#section_pnp_czg_tfb .section}

-   使用ChinaDRM前，请联系您的商务经理，开通服务并获取产品报价。
-   播放视频需集成阿里云播放器SDK，目前仅支持Android与iOS移动端播放。

## 安装 {#section_m2z_dzg_tfb .section}

MPS SDK详情参见 [安装](../../../../cn.zh-CN/SDK参考/媒体转码SDK/Python SDK/安装.md#)。

## 示例代码 {#section_js1_jzg_tfb .section}

```
# -*- coding: UTF-8 -*-
import json
from aliyunsdkmts.request.v20140618 import AddMediaWorkflowRequest
from aliyunsdkcore import client

REGION_ID = 'cn-shanghai'
ACCESS_KEY_ID = 'idid'
ACCESS_KEY_SECRET = 'keykey'
PIPELINE_ID = "pipelineid";
OSS_LOCATION = "oss-" + REGION_ID;
INPUT_BUCKET = "input_bucket"; #输入bucket
INPUT_PATH = "input_path"; #输入媒体的路径
OUTPUT_BUCKET = "output_bucket"; #输出bucket
OUTPUT_PATH = "output_path"; #输出媒体路径
ENCRYPTION_TYPE = "ChinaDRM";

WORKFLOW_TEMPLATE = '''{
    "Activities": {
        "Act-Start": {
            "Name": "Act-Start",
            "Parameters": {
                "PipelineId": "PIPELINE_ID",
                "InputFile": "{\\"Bucket\\":\\"INPUT_BUCKET\\",\\"Location\\":\\"OSS_LOCATION\\",\\"Object\\":\\"INPUT_PATH\\"}"
            },
            "Type": "Start"
        },
        "Act-ChinaDRM-LD": {
            "Name": "Act-ChinaDRM-LD",
            "Parameters": {
                "Outputs": "[{\\"Object\\":\\"OUTPUT_PATH/{MediaId}/{RunId}/LD/{FileName}\\",\\"Encryption\\":{\\"Type\\":\\"ENCRYPTION_TYPE\\"},\\"TemplateId\\":\\"S00000001-100010\\"}]",
                "OutputBucket": "OUTPUT_BUCKET",
                "OutputLocation": "OSS_LOCATION"
            },
            "Type": "Transcode"
        },
        "Act-ChinaDRM-SD": {
            "Name": "Act-ChinaDRM-SD",
            "Parameters": {
                "Outputs": "[{\\"Object\\":\\"OUTPUT_PATH/{MediaId}/{RunId}/SD/{FileName}\\",\\"Encryption\\":{\\"Type\\":\\"ENCRYPTION_TYPE\\"},\\"TemplateId\\":\\"S00000001-100020\\"}]",
                "OutputBucket": "OUTPUT_BUCKET",
                "OutputLocation": "OSS_LOCATION"
            },
            "Type": "Transcode"
        },
        "Act-ChinaDRM-HD": {
            "Name": "Act-ChinaDRM-HD",
            "Parameters": {
                "Outputs": "[{\\"Object\\":\\"OUTPUT_PATH/{MediaId}/{RunId}/HD/{FileName}\\",\\"Encryption\\":{\\"Type\\":\\"ENCRYPTION_TYPE\\"},\\"TemplateId\\":\\"S00000001-100030\\"}]",
                "OutputBucket": "OUTPUT_BUCKET",
                "OutputLocation": "OSS_LOCATION"
            },
            "Type": "Transcode"
        },
        "Act-Report": {
            "Name": "Act-Report",
            "Parameters": {
                "PublishType": "Auto"
            },
            "Type": "Report"
        }
    },
    "Dependencies": {
        "Act-ChinaDRM-LD": ["Act-Report"],
        "Act-ChinaDRM-HD": ["Act-Report"],
        "Act-Start": ["Act-ChinaDRM-SD", "Act-ChinaDRM-HD", "Act-ChinaDRM-LD"],
        "Act-Report": [],
        "Act-ChinaDRM-SD": ["Act-Report"]
    }
}'''

def addMediaWorkflow():
    global client
    client = client.AcsClient(ACCESS_KEY_ID, ACCESS_KEY_SECRET, REGION_ID)
    request = AddMediaWorkflowRequest.AddMediaWorkflowRequest()
    request.set_Topology(buildWorkflowTopology())
    #print request.get_Topology();
    request.set_Name("ChinaDRM加密工作流py")
    response = client.do_action_with_exception(request)
    print json.loads(response)

def buildWorkflowTopology():
    return WORKFLOW_TEMPLATE.replace("PIPELINE_ID", PIPELINE_ID).replace("INPUT_BUCKET", INPUT_BUCKET).replace("OSS_LOCATION", OSS_LOCATION).replace("INPUT_PATH", INPUT_PATH).replace("OUTPUT_BUCKET", OUTPUT_BUCKET).replace("OUTPUT_PATH", OUTPUT_PATH).replace("ENCRYPTION_TYPE", ENCRYPTION_TYPE);

if __name__ == "__main__":
    addMediaWorkflow()
```

