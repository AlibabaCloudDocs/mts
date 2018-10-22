# Watermarks {#concept_bsb_kg2_z2b .concept}

1.  Create AcsClient instance.

    ```
    $clientProfile = DefaultProfile::getProfile(
        $mps_region_id,                   # Region ID
        $access_key_id,                   # AccessKey ID
        $access_key_secret                # AccessKey Secret
    );
    $client = new DefaultAcsClient($clientProfile);
    ```

2.  Create request and set parameters.

    ```
    $request = new Mts\SubmitJobsRequest();
    $request->setAcceptFormat('JSON');
    ```

3.  Watermark parameters.
    -   Image watermark

        ```
        $image_watermark_input = array(
                             'Location' => $oss_location,
                             'Bucket' => $oss_bucket,
                             'Object' => urlencode($image_watermark_object)
                            );
         $image_watermark = array(
                     'WaterMarkTemplateId' => $watermark_template_id,
                     'Type' => 'Image',
                     'InputFile' => $image_watermark_input,
                     'ReferPos' => 'TopRight',
                     'Width' => 0.05,
                     'Dx' => 0,
                     'Dy'=> 0
                    );
        ```

    -   Text watermark

        ```
        $text_config = array(
                  'Content' => '5rWL6K+V5paH5a2X5rC05Y2w',
                  'FontName' => 'SimSun',
                  'FontSize' => 16,
                  'FontColor' => 'Red',
                  'FontAlpha' => 0.5,
                  'Top' => 10,
                  'Left' => 10
                 );
         $text_watermark = array(
                     'WaterMarkTemplateId' => $watermark_template_id,
                     'Type' => 'Text',
                     'TextWaterMark' => $text_config
                    );
        ```

    -   Video watermark

        ```
        $video_watermark_input = array (
                            'Location' => $oss_location,
                            'Bucket' => $oss_bucket,
                            'Object' => urlencode($video_watermark_object)
                           );
         $video_watermark = array(
                     'WaterMarkTemplateId' => $watermark_template_id,
                     'Type' => 'Image',
                     'InputFile'=> $video_watermark_input,
                     'ReferPos' => 'BottomLeft',
                     'Height' => 240,
                     'Dx' => 0,
                     'Dy' => 0
                    );
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
$watermark_template_id = 'xxx';
$template_id = 'S00000001-200030';
$oss_location = 'oss-cn-hangzhou';
$oss_bucket = 'presigned';
$oss_input_object = 'input.mp4';
$oss_output_object = 'output.mp4';
$image_watermark_object = 'logo.png';
$video_watermark_object = 'logo.mov';
# DefaultAcsClient
$clientProfile = DefaultProfile::getProfile(
    $mps_region_id,                   # Region ID
    $access_key_id,                   # AccessKey ID
    $access_key_secret                # AccessKey Secret
);
$client = new DefaultAcsClient($clientProfile);
# request
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
## Image Watermark
$image_watermark_input = array(
                          'Location' => $oss_location,
                          'Bucket' => $oss_bucket,
                          'Object' => urlencode($image_watermark_object)
                         );
$image_watermark = array(
                  'WaterMarkTemplateId' => $watermark_template_id,
                  'Type' => 'Image',
                  'InputFile' => $image_watermark_input,
                  'ReferPos' => 'TopRight',
                  'Width' => 0.05,
                  'Dx' => 0,
                  'Dy'=> 0
                 );
## Text Watermark
$text_config = array(
               'Content' => '5rWL6K+V5paH5a2X5rC05Y2w',
               'FontName' => 'SimSun',
               'FontSize' => 16,
               'FontColor' => 'Red',
               'FontAlpha' => 0.5,
               'Top' => 10,
               'Left' => 10
              );
$text_watermark = array(
                  'WaterMarkTemplateId' => $watermark_template_id,
                  'Type' => 'Text',
                  'TextWaterMark' => $text_config
                 );
## Video Watermark
$video_watermark_input = array (
                         'Location' => $oss_location,
                         'Bucket' => $oss_bucket,
                         'Object' => urlencode($video_watermark_object)
                        );
$video_watermark = array(
                  'WaterMarkTemplateId' => $watermark_template_id,
                  'Type' => 'Image',
                  'InputFile'=> $video_watermark_input,
                  'ReferPos' => 'BottomLeft',
                  'Height' => 240,
                  'Dx' => 0,
                  'Dy' => 0
                 );
# Output->Watermarks
$watermarks = array($image_watermark, $text_watermark, $video_watermark);
$output['WaterMarks'] = $watermarks;
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

