# Create HLS standard encryption workflow

## Overview

The article is an example of calling API to create HLS standard encryption workflow. For more information about creating workflow, see [AddMediaWorkflow](/intl.en-US/API Reference/Media workflow APIs/AddMediaWorkflow.md). For more information about MPS SDK, see [Installation](/intl.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Installation.md).

## Code example

```
<? php
include_once 'aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
date_default_timezone_set('PRC');
class HLSEncryptionWorkflowDemo {
    private $client;
    private $region = '<region>';
    private $accessKeyId = '<accessKeyId>';
    private $accessKeySecret = '<accessKeySecret>';
    private $pipelineId = "<PipelineId>";
    private $templateId = "S00000001-100020"; #transcoding template ID,m3u8 template, set as needed
    private $ossLocation = "<OssLocation>";
    private $inputBucket = "<InputBucket>";
    private $inputPath = "<InputPath>"; #Example: "HLS-Encryption"
    private $outputBucket = "<OutputBucket>";
    private $encryptionType = "hls-aes-128";
    private $hlsKeyUri = "<decryption key URI>"; #Example: http://decrypt.testdomain.com
    private $actStart = "Act-Start";
    private $actEncryption = "Act-HLS-Encryption";
    private $actReport = "Act-Report";
    function __construct() {
        $profile = DefaultProfile::getProfile($this->region, $this->accessKeyId, $this->accessKeySecret);
        $this->client = new DefaultAcsClient($profile);
    }
    function addMediaWorkflow() {
        $request = new Mts\AddMediaWorkflowRequest();
        $request->setName("HLS encryption workflow php");
        $request->setTopology($this->buildWorkflowTopology());
        $response = $this->client->getAcsResponse($request);
        echo json_encode($response);
    }
    function buildWorkflowTopology() {
        $activities = $this->buildActivities();
        $dependencies = $this->buildDependencies();
        $workflow = array(
                          "Activities" => $activities,
                          "Dependencies" => $dependencies
                         );
        echo json_encode($workflow)."\n";
        return json_encode($workflow);
    }
    function buildActivities() {
        $activities = [
            $this->actStart => $this->buildStartActivity(),
            $this->actEncryption => $this->buildTranscodeActivity(),
            $this->actReport => $this->buildReportActivity()
        ];
        return $activities;
    }
    function buildStartActivity() {
        $startActivity = array(
            "Name" => $this->actStart,
            "Type" => "Start",
            "Parameters" => $this->buildStartParameters()
        );
        return $startActivity;
    }
    function buildStartParameters() {
        $startParameters = array(
            "PipelineId" => $this->pipelineId,
            "InputFile" => $this->buildInputFile()
        );
        return $startParameters;
    }
    function buildInputFile() {
        $inputFile = array(
            "Bucket" => $this->inputBucket,
            "Location" => $this->ossLocation,
            "ObjectPrefix" => $this->inputPath
        );
        return $inputFile;
    }
    function buildTranscodeActivity() {
        $transcodeParameters = array(
            "Name" => $this->actEncryption,
            "Type" => "Transcode",
            "Parameters" => $this->buildTranscodeParameters()
        );
        return $transcodeParameters;
    }
    function buildTranscodeParameters() {
        $transcodeParameters = array(
            "OutputBucket" => $this->outputBucket,
            "OutputLocation" => $this->ossLocation,
            "Outputs" => $this->buildOutputsConfig()
        );
        return $transcodeParameters;
    }
    function buildOutputsConfig() {
        $output = array(
            "ObjectRegex" => $this->actEncryption." /{RunId}/{FileName}",
            "TemplateId" => $this->templateId,
            "Encryption" => $this->buildEncryption()
        );
        $outputs = array($output);
        return $outputs;
    }
    function buildEncryption() {
        $encryption = array(
            "Type" => $this->encryptionType,
            "KeyUri" => $this->hlsKeyUri
        );
        return $encryption;
    }
    function buildReportActivity() {
        $reportActivity = array(
            "Name" => $this->actReport,
            "Parameters" => (object)[],
            "Type" => "Report"
        );
        return $reportActivity;
    }
    function buildDependencies() {
        $subActivityOfStart = array(
            $this->actEncryption
        );
        $subActivityOfTranscode = array(
            $this->actReport
        );
        $dependencies = array(
            $this->actStart => $subActivityOfStart,
            $this->actEncryption => $subActivityOfTranscode,
            $this->actReport => []
        );
        return $dependencies;
    }
}
$demo = new HLSEncryptionWorkflowDemo();
$demo->addMediaWorkflow();
? >
```

