# Add media workflow {#concept_okw_4p2_z2b .concept}

The user can assemble activities provided by MPS, such as transcode activity and screenshot activity into a topology. The topology is as follows:

```
<? php
include_once 'aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
# Step 1 set region
$REGION = "cn-shenzhen";
$OSS_REGION = "oss-cn-shenzhen";
$mtsEndpoint = "mts." + REGION + ".aliyuncs.com";
# Step 2.set accesskey & keySecret
$accessKeyId = "";
$accessKeySecret = "";
# Step 3.set mps transcoding queue id
$PIPELINE_ID = "38bba54d524448be92d277caaa8da118";
#Create DefaultAcsClient instance and perform initialization
$clientProfile = DefaultProfile::getProfile(
    $REGION,                        # Your Region ID
    $accessKeyId,                   # Your AccessKey ID
    $accessKeySecret                # Your AccessKey Secret
);
$client = new DefaultAcsClient($clientProfile);
$request = new Mts\AddMediaWorkflowRequest();
$request->setAcceptFormat('JSON');
$request->setName("Sequential-workflow");
$startActivity = array(
        "Type"=>"Start",
        "Parameters"=>array(
            "InputFile"=>array(
                "Bucket"=> "mtb-sz-in",
                "Location"=> $OSS_REGION,
                "ObjectPrefix"=> "media/"
            ),
            "PipelineId"=>$PIPELINE_ID
        )
    );
$transcodeActivity = array(
        "Type"=>"Transcode",
        "Parameters"=> array (
            "Outputs"=>array(
                array(
                    "OutputObject"=> urlencode("transcode/{ObjectPrefix}/{FileName}.{ ExtName}"),
                    "TemplateId"=> "S00000001-000070"
                )
            ),
            "OutputLocation"=> $OSS_REGION,
            "OutputBucket"=>"mtb-sz-out"
        )
    );
$reportActivity = array(
        "Type"=> "Report",
        "Parameters"=> array(
             "PublishType"=>"Auto"
        )
    );
$topology = array(
        "Activities"=> array(
            "startNode"=>$startActivity,
            "transcodingNode"=>$transcodeActivity,
            "reportNode"=>$reportActivity
        ),
        "Dependencies"=>array (
            "startNode"=>array("transcodingNode"),
            "transcodingNode"=>array("reportNode"),
            "reportNode"=>array()
        )
    );
$request->setTopology(json_encode($topology));
# Initiate request and handle returned result
try {
    $response = $client->getAcsResponse($request);
    print 'RequestId is:' . $response->{'RequestId'} . "\n";;
    print "Response:".json_encode($response);
} catch(ServerException $e) {
    print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
} catch(ClientException $e) {
    print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
}
? >
```

