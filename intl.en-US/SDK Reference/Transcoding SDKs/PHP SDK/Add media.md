# Add media {#concept_wnb_jp2_z2b .concept}

Add a video file to Media files:

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
#  Create DefaultAcsClient instance and perform initialization
$clientProfile = DefaultProfile::getProfile(
    $REGION,                        # Your Region ID
    $accessKeyId,                   # Your AccessKey ID
    $accessKeySecret                #Your AccessKey Secret
);
$client = new DefaultAcsClient($clientProfile);
$request = new Mts\AddMediaRequest();
$request->setAcceptFormat('JSON');
$request->setFileURL("http://mtb-sz-in.oss-cn-shenzhen.aliyuncs.com/media/r180-ABC.mp4");
$request->setMediaWorkflowId("829bed0300994057a49e4f16de957e34");
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

