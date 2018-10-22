# Splicing-opening and ending scenes {#concept_qyz_2j2_z2b .concept}

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
    $request = new Mts\SubmitJobsRequest();
    $request->setAcceptFormat('JSON');
    ```

3.  Set transcoding parameters.
    -   Input

        ```
        $input = array('Location' => $oss_location,
                  'Bucket' => $oss_bucket,
                  'Object' => urlencode($head_object));
        $request->setInput(json_encode($input));
        ```

    -   Output

        ```
        $output = array('OutputObject' => urlencode($oss_output_object));
        ```

        -   Video

            ```
            $output['Video'] = array('Width' => 1280,
                             'Height' => 720);
            ```

        -   OpeningList

            ```
            $opening_video = array('OpenUrl' => 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/'.urlencode($head_object),
                           'Width' => 640,
                           'Start' => 2);
            $output['OpeningList'] = array($opening_video);
            ```

        -   TailSlateList

            ```
            $tailslate_video = array('TailUrl' => 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/'.urlencode($tail_object),
                             'Width' => 640,
                             'BlendDuration' => 3,
                             'BgColor' => 'Black');
            $output['TailSlateList'] = array($tailslate_video);
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


Full codes

```
<? php
include_once 'aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
$access_key_id = 'xxx';
$access_key_secret = 'xxx';
$mps_region_id = 'cn-hangzhou';
$pipeline_id = 'xxx';
$template_id = 'S00000001-200030';
$oss_location = 'oss-cn-hangzhou';
$oss_bucket = 'xxx';
$oss_input_object = 'input.mp4';
$oss_output_object = 'output.mp4';
$head_object = 'head.mp4';
$tail_object = 'tail.mp4';
# Create DefaultAcsClient instance and complete initialization
$clientProfile = DefaultProfile::getProfile(
    $mps_region_id,                   # Region ID
    $access_key_id,                   # AccessKey ID
    $access_key_secret                # AccessKey Secret
);
$client = new DefaultAcsClient($clientProfile);
#Create API request and set parameters
$request = new Mts\SubmitJobsRequest();
$request->setAcceptFormat('JSON');
# Input
$input = array('Location' => $oss_location,
               'Bucket' => $oss_bucket,
               'Object' => urlencode($oss_input_object));
$request->setInput(json_encode($input));
# Output
$output = array('OutputObject' => urlencode($oss_output_object));
# Ouput->TemplateId
$output['TemplateId'] = $template_id;
# Output->OpeningList
$opening_video = array('OpenUrl' => 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/'.urlencode($head_object),
                       'Width' => 640,
                       'Start' => 2);
$output['OpeningList'] = array($opening_video);
# Output->TailSlateList
$tailslate_video = array('TailUrl' => 'http://'.$oss_bucket.'.'.$oss_location.'.aliyuncs.com/'.urlencode($tail_object),
                         'Width' => 640,
                         'BlendDuration' => 3,
                         'BgColor' => 'Black');
$output['TailSlateList'] = array($tailslate_video);
# Outputs
$outputs = array($output);
$request->setOUtputs(json_encode($outputs));
$request->setOutputBucket($oss_bucket);
$request->setOutputLocation($oss_location);
# PipelineId
$request->setPipelineId($pipeline_id);
# call api
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

