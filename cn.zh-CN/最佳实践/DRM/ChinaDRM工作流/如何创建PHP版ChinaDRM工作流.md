# 如何创建PHP版ChinaDRM工作流 {#concept_x2m_nzg_tfb .concept}

本文创建如何创建PHP版ChinaDRM工作流。

## 使用限制 {#section_bd2_pzg_tfb .section}

-   使用ChinaDRM前，请联系您的商务经理，开通服务并获取产品报价。
-   播放视频需集成阿里云播放器SDK，目前仅支持Android与iOS移动端播放。

## 安装 {#section_cfl_rzg_tfb .section}

MPS SDK详情参见 [安装](../../../../cn.zh-CN/SDK参考/媒体转码SDK/PHP SDK/安装.md#)。

## 示例代码 {#section_ivt_tzg_tfb .section}

```
<?php
include_once 'aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
date_default_timezone_set('PRC');

class ChinaDRMWF {
    private $client;
    private $region = 'cn-shanghai';
    private $accessKeyId = 'idid';
    private $accessKeySecret = 'keykey';

    private $pipelineId = "pipelineId";
    private $ossLocation = "oss-cn-shanghai";
    private $inputBucket = "input_first";
    private $inputPath = "input_path";
    private $outputBucket = "output_bucket";
    private $outputPath = "output_path";
    private $encryptionType = "ChinaDRM";

    private $WORKFLOW_TEMPLATE = '{
	"Activities": {
		"Act-Start": {
			"Name": "Act-Start",
			"Parameters": {
				"PipelineId": "PIPELINE_ID",
				"InputFile": "{\"Bucket\":\"INPUT_BUCKET\",\"Location\":\"OSS_LOCATION\",\"Object\":\"INPUT_PATH\"}"
			},
			"Type": "Start"
		},
		"Act-ChinaDRM-LD": {
			"Name": "Act-ChinaDRM-LD",
			"Parameters": {
				"Outputs": "[{\"Object\":\"OUTPUT_PATH/{MediaId}/{RunId}/LD/{FileName}\",\"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"},\"TemplateId\":\"S00000001-100010\"}]",
				"OutputBucket": "OUTPUT_BUCKET",
				"OutputLocation": "OSS_LOCATION"
			},
			"Type": "Transcode"
		},
		"Act-ChinaDRM-SD": {
			"Name": "Act-ChinaDRM-SD",
			"Parameters": {
				"Outputs": "[{\"Object\":\"OUTPUT_PATH/{MediaId}/{RunId}/SD/{FileName}\",\"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"},\"TemplateId\":\"S00000001-100020\"}]",
				"OutputBucket": "OUTPUT_BUCKET",
				"OutputLocation": "OSS_LOCATION"
			},
			"Type": "Transcode"
		},
		"Act-ChinaDRM-HD": {
			"Name": "Act-ChinaDRM-HD",
			"Parameters": {
				"Outputs": "[{\"Object\":\"OUTPUT_PATH/{MediaId}/{RunId}/HD/{FileName}\",\"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"},\"TemplateId\":\"S00000001-100030\"}]",
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
}';


    function __construct() {
        $profile = DefaultProfile::getProfile($this->region, $this->accessKeyId, $this->accessKeySecret);
        $this->client = new DefaultAcsClient($profile);
    }

    function addMediaWorkflow() {
        $request = new Mts\AddMediaWorkflowRequest();
        $request->setName("ChinaDRM加密工作流php");
        $request->setTopology($this->buildWorkflowTopology());

        $response = $this->client->getAcsResponse($request);
        echo json_encode($response);
    }

    function buildWorkflowTopology() {
        $workflow = str_replace("\t", "" , $this->WORKFLOW_TEMPLATE);
        $workflow = str_replace("\n", "" , $workflow);
        $workflow = str_replace("PIPELINE_ID", $this->pipelineId, $workflow);
        $workflow = str_replace("OSS_LOCATION", $this->ossLocation , $workflow);
        $workflow = str_replace("INPUT_BUCKET", $this->inputBucket , $workflow);
        $workflow = str_replace("INPUT_PATH", $this->inputPath , $workflow);
        $workflow = str_replace("OUTPUT_BUCKET", $this->outputBucket , $workflow);
        $workflow = str_replace("OUTPUT_PATH", $this->outputPath , $workflow);
        $workflow = str_replace("ENCRYPTION_TYPE", $this->encryptionType , $workflow);
        return $workflow;
    }
}

$demo = new ChinaDRMWF();
$demo->addMediaWorkflow();
?>
```

