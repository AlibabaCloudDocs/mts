# Quick start {#concept_pjj_jf2_z2b .concept}

1.  Create AcsClient instance.

    ```
    $clientProfile = DefaultProfile::getProfile(
    $mps_region_id,                   # Your  Region ID
    $access_key_id,                   # Your AccessKey ID
    $access_key_secret                # Your AccessKey Secret
    );
    $client = new DefaultAcsClient($clientProfile);
    ```

2.  Create request and set parameters.

    ```
    $request = new Mts\SubmitJobsRequest();
    $request->setAcceptFormat('JSON');
    ```

3.  Initiate API request and display returned value.

    ```
    $response = $client->getAcsResponse($request);
    print 'PipelineName is:' . $response->{'PipelineList'}->{'Pipeline'}[0]->{'Name'} . "\n";
    print 'PipelineId is:' . $response->{'PipelineList'}->{'Pipeline'}[0]->{'Id'} . "\n";
    ```


Full codes

```
<? php
include_once 'aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
$access_key_id = 'xxx';
$access_key_secret = 'xxx';
$mps_region_ids = array('cn-hangzhou', 'cn-beijing', 'cn-shenzhen',
                            'cn-shanghai', 'cn-hongkong', 'us-west-1',
                            'ap-southeast-1', 'ap-northeast-1', 'eu-central-1',
                            'ap-south-1');
foreach ($mps_region_ids as $mps_region_id) {
    print 'region is:' . $mps_region_id . "\n";
    # Create DefaultAcsClient instance and complete initialization
    $clientProfile = DefaultProfile::getProfile(
        $mps_region_id,                   # Your Region ID
        $access_key_id,                   #Your  AccessKey ID
        $access_key_secret                # Your  AccessKey Secret
    );
    $client = new DefaultAcsClient($clientProfile);
    # Create API request and set parameters
    $request = new Mts\SearchPipelineRequest();
    # Initiate request and handle the returned value
    try {
        $response = $client->getAcsResponse($request);
        print 'PipelineName is:' . $response->{'PipelineList'}->{'Pipeline'}[0]->{'Name'} . "\n";
        print 'PipelineId is:' . $response->{'PipelineList'}->{'Pipeline'}[0]->{'Id'} . "\n";
    } catch(ServerException $e) {
        print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
    } catch(ClientException $e) {
        print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
    }
}
```

