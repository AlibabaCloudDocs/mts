# Screenshot {#concept_a4h_xg2_z2b .concept}

1.  Create AcsClient instance.

    ```
    $clientProfile = DefaultProfile::getProfile(
        $mps_region_id,                   # Region ID
        $access_key_id,                   # AccessKey ID
        $access_key_secret                # AccessKey Secret
    );
    $client = new DefaultAcsClient($clientProfile);
    ```

2.  Create request, and set parameters.

    ```
    $request = new Mts\SubmitSnapshotJobRequest();
    $request->setAcceptFormat('JSON');
    ```

3.  Set screenshot parameters.
    -   Input

        ```
        $input = array('Location' => $oss_location,
                  'Bucket' => $oss_bucket,
                  'Object' => urlencode($oss_input_object));
        $request->setInput(json_encode($input));
        ```

    -   SnapshotConfig
        -   OutputFile

            ```
            $output = array('Location' => $oss_location,
                    'Bucket' => $oss_bucket,
                    'Object' => urlencode($oss_output_object));
            $snapshot_config = array('OutputFile' => $output);
            ```

        -   Time

            ```
            $snapshot_config['Time'] = 2;
            ```

        -   Interval/Num

            ```
            $snapshot_config['Interval'] = 2;
            $snapshot_config['Num'] = 3;
            ```

        -   Width/Height

            ```
            $snapshot_config['Height'] = 360;
            ```

4.  Initiate API request and display returned value.

    ```
    $response = $client->getAcsResponse($request);
    print 'RequestId is:' . $response->{'RequestId'} . "\n";
    print 'JobId is:' . $response->{'SnapshotJob'}->{'Id'} . "\n";
    print 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/output_00001.jpg' . "\n";
    print 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/output_00002.jpg' . "\n";
    print 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/output_00003.jpg' . "\n";
    ```


Full code

```
<? php
include_once 'aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
$access_key_id = 'xxx';
$access_key_secret = 'xxx';
$mps_region_id = 'cn-hangzhou';
$pipeline_id = 'xxx';
$oss_location = 'oss-cn-hangzhou';
$oss_bucket = 'xxx';
$oss_input_object = 'input.mp4';
$oss_output_object = 'output_{Count}.jpg';
# DefaultAcsClient
$clientProfile = DefaultProfile::getProfile(
    $mps_region_id,                   # Region ID
    $access_key_id,                   # AccessKey ID
    $access_key_secret                # AccessKey Secret
);
$client = new DefaultAcsClient($clientProfile);
# request
$request = new Mts\SubmitSnapshotJobRequest();
$request->setAcceptFormat('JSON');
# Input
$input = array('Location' => $oss_location,
               'Bucket' => $oss_bucket,
               'Object' => urlencode($oss_input_object));
$request->setInput(json_encode($input));
# SnapshotConfig->OutputFile
$output = array('Location' => $oss_location,
                'Bucket' => $oss_bucket,
                'Object' => urlencode($oss_output_object));
$snapshot_config = array('OutputFile' => $output);
# SnapshotConfig->Time
$snapshot_config['Time'] = 2;
# SnapshotConfig->Interval/Num
$snapshot_config['Interval'] = 2;
$snapshot_config['Num'] = 3;
# SnapshotConfig->Width/Height
$snapshot_config['Height'] = 360;
# SnapshotConfig
$request->setSnapshotConfig(json_encode($snapshot_config));
# PipelineId
$request->setPipelineId($pipeline_id);
# call api
try {
    $response = $client->getAcsResponse($request);
    print 'RequestId is:' . $response->{'RequestId'} . "\n";
    print 'JobId is:' . $response->{'SnapshotJob'}->{'Id'} . "\n";
    print 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/output_00001.jpg' . "\n";
    print 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/output_00002.jpg' . "\n";
    print 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/output_00003.jpg' . "\n";
} catch(ServerException $e) {
    print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
} catch(ClientException $e) {
    print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
}
```

