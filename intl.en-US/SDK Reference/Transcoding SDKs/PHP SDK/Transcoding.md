# Transcoding {#concept_jpr_rf2_z2b .concept}

1.  Create AcsClient instance.

    ```
    $clientProfile = DefaultProfile::getProfile(
    $mps_region_id,                   # Your Region ID
    $access_key_id,                   # Your AccessKey ID
    $access_key_secret                # Your AccessKey Secret
    );
    $client = new DefaultAcsClient($clientProfile);
    ```

2.  Create request, and set parameters.

    ```
    $request = new Mts\SubmitJobsRequest();
    $request->setAcceptFormat('JSON');
    ```

3.  Transcoding parameters.
    -   Input

        ```
        $input = array('Location' => $oss_location,
                        'Bucket' => $oss_bucket,
                        'Object' => urlencode($oss_input_object));
        $request->setInput(json_encode($input));
        ```

    -   Output

        ```
        $output = array('OutputObject' => urlencode($oss_output_object));
        ```

        -   Container

            ```
            $output['Container'] = array('Format' => 'mp4');
            ```

        -   Video

            ```
            $output['Video'] = array('Codec' =>'H. 264',
                                        'Bitrate' => 1500,
                                        'Width' => 1280,
                                        'Fps' => 25);
            ```

        -   Audio

            ```
            $output['Audio'] = array('Codec' => 'AAC',
                                        'Bitrate' => 128,
                                        'Channels' => 2,
                                        'Samplerate' => 44100);
            ```

        -   TemplateId

            ```
            $output['TemplateId'] = $template_id;
            ```

    -   PipelineId

        ```
        $request->setPipelineId($pipeline_id);
        ```

4.  Initiate API request and display returned value.

    ```
    $response = $client->getAcsResponse($request);
    print 'RequestId is:' . $response->{'RequestId'} . "\n";;
    if ($response->{'JobResultList'}->{'JobResult'}[0]->{'Success'}) {
    print 'JobId is:' .
          $response->{'JobResultList'}->{'JobResult'}[0]->{'Job'}->{'JobId'} . "\n";
    } else {
    print 'SubmitJobs Failed code:' .
          $response->{'JobResultList'}->{'JobResult'}[0]->{'Code'} .
          ' message:' .
          $response->{'JobResultList'}->{'JobResult'}[0]->{'Message'} . "\n";
    }
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
$template_id = 'S00000001-200010';
$oss_location = 'oss-cn-hangzhou';
$oss_bucket = 'xxx';
$oss_input_object = 'input.mp4';
$oss_output_object = 'output.mp4';
# Create DefaultAcsClient instance and complete initialization
$clientProfile = DefaultProfile::getProfile(
    $mps_region_id,                   # Your Region ID
    $access_key_id,                   # Your AccessKey ID
    $access_key_secret                # Your AccessKey Secret
);
$client = new DefaultAcsClient($clientProfile);
# Create API request and set parameters
$request = new Mts\SubmitJobsRequest();
$request->setAcceptFormat('JSON');
# Input
$input = array('Location' => $oss_location,
               'Bucket' => $oss_bucket,
               'Object' => urlencode($oss_input_object));
$request->setInput(json_encode($input));
# Output
$output = array('OutputObject' => urlencode($oss_output_object));
# Ouput->Container
$output['Container'] = array('Format' => 'mp4');
# Ouput->Video
$output['Video'] = array('Codec' =>'H. 264',
                         'Bitrate' => 1500,
                         'Width' => 1280,
                         'Fps' => 25);
# Ouput->Audio
$output['Audio'] = array('Codec' => 'AAC',
                         'Bitrate' => 128,
                         'Channels' => 2,
                         'Samplerate' => 44100);
# Ouput->TemplateId
$output['TemplateId'] = $template_id;
$outputs = array($output);
$request->setOUtputs(json_encode($outputs));
$request->setOutputBucket($oss_bucket);
$request->setOutputLocation($oss_location);
# PipelineId
$request->setPipelineId($pipeline_id);
# Initiate request and handle returned value
try {
    $response = $client->getAcsResponse($request);
    print 'RequestId is:' . $response->{'RequestId'} . "\n";;
    if ($response->{'JobResultList'}->{'JobResult'}[0]->{'Success'}) {
        print 'JobId is:' .
               $response->{'JobResultList'}->{'JobResult'}[0]->{'Job'}->{'JobId'} . "\n";
    } else {
        print 'SubmitJobs Failed code:' .
               $response->{'JobResultList'}->{'JobResult'}[0]->{'Code'} .
               ' message:' .
               $response->{'JobResultList'}->{'JobResult'}[0]->{'Message'} . "\n";
    }
} catch(ServerException $e) {
    print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
} catch(ClientException $e) {
    print 'Error: ' . $e->getErrorCode() . ' Message: ' . $e->getMessage() . "\n";
}
```

