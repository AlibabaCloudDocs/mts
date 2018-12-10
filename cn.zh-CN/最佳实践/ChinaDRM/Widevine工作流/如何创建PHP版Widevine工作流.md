# 如何创建PHP版Widevine工作流 {#concept_ftn_fsc_bgb .concept}

本文介绍如何创建PHP版Widevine工作流。

## 使用限制 {#section_qmf_3sc_bgb .section}

-   使用Widevine前，请联系您的商务经理，开通服务并获取产品报价。
-   播放视频需集成Web播放器。

## 安装 {#section_gfx_jsc_bgb .section}

-   MPS SDK安装，参见 [安装](../../../../cn.zh-CN/SDK参考/媒体转码SDK/PHP SDK/安装.md#)。
-   创建三个容器格式为mpd的三路不同分辨率的转码模版，参见 [创建模版](../../../../cn.zh-CN/API参考/自定义转码模板接口/新增自定义转码模版.md#)。

## 示例代码 {#section_dlz_4sc_bgb .section}

```
<?php
include_once 'aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
date_default_timezone_set('PRC');

class ChinaDRMWF {
    private $client;
    private $region = 'cn-shanghai';
    private $accessKeyId = '<id>';
    private $accessKeySecret = '<secret>';

    private $pipelineId = "<pipelineid>";
    private $ossLocation = "<osslocation>";
    private $inputBucket = "<input>";
    private $inputPath = "<inputpath上传的视频存储路径>";
    private $outputBucket = "<outputbucket>";
    private $outputPath = "<转出视频输出路径>";
    private $encryptionType = "Widevine";
    private $mpd360Template = "<MPD模版>";
    private $mpd480Template = "<MPD模版>";
    private $mpd720Template = "<MPD模版>";

    private $WORKFLOW_TEMPLATE = '{
	"Activities": {
		"video-group": {
			"Name": "video-group",
			"Parameters": {
				"AdaptationSet": "{\"Group\":\"VideoGroup\"}"
			},
			"Type": "VideoGroup"
		},
		"act-start": {
			"Name": "act-start",
			"Parameters": {
				"PipelineId": "PIPELINE_ID",
				"InputFile": "{\"Bucket\":\"INPUT_BUCKET\",\"Location\":\"OSS_LOCATION\",\"ObjectPrefix\":\"INPUT_PATH/\"}"
			},
			"Type": "Start"
		},
		"audio-cn-group": {
			"Name": "audio-cn-group",
			"Parameters": {
				"AdaptationSet": "{\"Lang\":\"chinese\", \"Group\":\"AudioGroupChinese\"}"
			},
			"Type": "AudioGroup"
		},
		"audioCNTransNode": {
			"Name": "audioCNTransNode",
			"Parameters": {
				"Outputs": "[{\"TemplateId\":\"MPD_360P_TEMPLATE\",\"AudioStreamMap\":\"0:a:0\",\"Video\":{\"Remove\":\"true\"},\"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"}}]",
				"Representation": "{\"Id\":\"chinese128k\", \"URI\":\"audiocn/cn-abc.mpd\"}"
			},
			"Type": "Transcode"
		},
		"act-package": {
			"Name": "act-package",
			"Parameters": {
				"Output": "{\"Bucket\": \"OUTPUT_BUCKET\",\"Location\": \"OSS_LOCATION\",\"MasterPlayListName\": \"INPUT_PATH/{MediaId}/{RunId}/master.mpd\"}",
				"Protocol": "dash"
			},
			"Type": "PackageConfig"
		},
		"videoTransLD": {
			"Name": "videoTransLD",
			"Parameters": {
				"Outputs": "[{\"TemplateId\":\"MPD_360P_TEMPLATE\",\"Audio\":{\"Remove\":\"true\"},\"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"}}]",
				"Representation": "{\"Id\":\"360p\", \"URI\":\"videoLD/xx.mpd\"}"
			},
			"Type": "Transcode"
		},
		"act-report": {
			"Name": "act-report",
			"Parameters": {
				"PublishType": "Auto"
			},
			"Type": "Report"
		},
		"generateMasterPlayListAct": {
			"Name": "generateMasterPlayListAct",
			"Parameters": {},
			"Type": "GenerateMasterPlayList"
		},
		"videoTransSD": {
			"Name": "videoTransSD",
			"Parameters": {
				"Outputs": "[{\"TemplateId\":\"MPD_480P_TEMPLATE\",\"Audio\":{\"Remove\":\"true\"}, \"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"}}]",
				"Representation": "{\"Id\":\"480p\", \"URI\":\"videoSD/xx.mpd\"}"
			},
			"Type": "Transcode"
		},
		"videoTransHD": {
			"Name": "videoTransHD",
			"Parameters": {
				"Outputs": "[{\"TemplateId\":\"MPD_720P_TEMPLATE\",\"Audio\":{\"Remove\":\"true\"},\"Encryption\":{\"Type\":\"ENCRYPTION_TYPE\"}}]",
				"Representation": "{\"Id\":\"720p\", \"URI\":\"videoHD/xx.mpd\"}"
			},
			"Type": "Transcode"
		}
	},
	"Dependencies": {
		"video-group": ["videoTransLD", "videoTransSD", "videoTransHD"],
		"act-start": ["act-package"],
		"audio-cn-group": ["audioCNTransNode"],
		"audioCNTransNode": ["generateMasterPlayListAct"],
		"act-package": ["audio-cn-group", "video-group"],
		"videoTransLD": ["generateMasterPlayListAct"],
		"act-report": [],
		"generateMasterPlayListAct": ["act-report"],
		"videoTransSD": ["generateMasterPlayListAct"],
		"videoTransHD": ["generateMasterPlayListAct"]
	}
}';


    function __construct() {
        $profile = DefaultProfile::getProfile($this->region, $this->accessKeyId, $this->accessKeySecret);
        $this->client = new DefaultAcsClient($profile);
    }

    function addMediaWorkflow() {
        $request = new Mts\AddMediaWorkflowRequest();
        $request->setName("Widevine加密工作流php");
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
        $workflow = str_replace("MPD_360P_TEMPLATE", $this->mpd360Template, $workflow);
        $workflow = str_replace("MPD_480P_TEMPLATE", $this->mpd480Template, $workflow);
        $workflow = str_replace("MPD_720P_TEMPLATE", $this->mpd720Template, $workflow);

        return $workflow;
    }
}

$demo = new ChinaDRMWF();
$demo->addMediaWorkflow();
?>
```

