# Receive notification through queues {#concept_t4f_t2v_1fb .concept}

This section briefly introduces the requirements and installation instructions of MNS.

For more information, see the MNS documentation SDK download and Queue user manual.

The example language is PHP. For more information about the usage instructions of other languages, see the MNS SDK user manual.

## Environment requirements {#section_u2x_x2v_1fb .section}

PHP 5.5+

## Installation {#section_ibq_y2v_1fb .section}

Download the MNS SDK for PHP from Alibaba Cloud.

Decompress the file to the project directory. The decompressed directory is `php_sdk`.

## Sample code {#section_tsj_z2v_1fb .section}

-   Reference the MNS SDK

    ```
    require_once(dirname(__FILE__).'/php_sdk/mns-autoloader.php');
    ```

-   Initialize MNS

    MNS configures an independent service domain name for each region of users. The rule is `https://${UserId}.mns. ${Region}.aliyuncs.com`. **China East 1 \(Hangzhou\) \(cn-hangzhou\)**is used in the following example. You can also use another region, for example, **China North 2 \(Beijing\) \(cn-beijing\)**.

    ```
    use AliyunMNS\Client;
     use AliyunMNS\Exception\MnsException;
    ```

    ```
    $mns_client = new Client('https://'.$user_id.'.mns.cn-hangzhou.aliyuncs.com',
                              $access_key_id, $access_key_secret);
     $queue = $mns_client->getQueueRef($queue_name);
    ```

-   Receive a message

    Each message received by MNS corresponds to a handle, which can be used later to operate the message \(for example, delete the message\).

    In addition, MNS supports receiving messages in batches to improve the performance. For more information, see the MNS BatchReceiveMessage.

    A timeout time can be specified when a message is received. \(The timeout time is set to 3s in the following example.\) If no message exists in the queue, timeout occurs and an exception is returned.

    ```
    $receipt_handle = NULL;
     $message = null;
     try
     {
          $res = $queue->receiveMessage(3);
          echo "ReceiveMessage Succeed! \n";
          $message = $res->getMessageBody();
          $receipt_handle = $res->getreceiptHandle();
     }
     catch (MnsException $e)
     {
          echo "ReceiveMessage Failed: " . $e . "\n";
     }
    ```

-   Delete a message

    A message is not actively deleted from a queue. You must call DeleteMessage to delete the message. Otherwise, the message is always in the queue, and you will receive the same message next time. In addition, DeleteMessage can be called successfully only within the specified time after the message is received. For more information, see MNS - DeleteMessage.

    ```
    try
     {
          $res = $queue->deleteMessage($receipt_handle);
          echo "DeleteMessage Succeed! \n";
     }
     catch (MnsException $e)
     {
          echo "DeleteMessage Failed: " . $e . "\n";
     }
    ```

-   Analyze a message

    The message body is a string while the content is a JSON object. After converting the string to the object using `json_decode`, you can analyze the JSON object to obtain details of the message. The output file that triggers media workflow execution is printed in the following example.

    ```
    $json_message = json_decode($message);
     $input_file = $json_message->{'MediaWorkflowExecution'}->{'Input'}->{'InputFile'};
     echo 'input_filelocation:'.$input_file->{'Location'}.
          ' bucket:'.$input_file->{'Bucket'}.
          ' object:'.$input_file->{'Object'}."\n";
    ```

-   Obtain video output details

    After obtaining details of a message, you can use the media library API to obtain details of a video executed by a workflow. The output URL of the transcoding and screenshot tasks is printed in the following example.

    For more information about how to install and configure the SDK for PHP of the media library, see [Media Library SDK-PHP](../../../../reseller.en-US//PHP SDK/Overview.md#).

    ```
    include_once 'aliyun-php-sdk-core/Config.php';
     use Mts\Request\V20140618 as Mts;
    ```

    Initialize the client of the media library.

    ```
    $profile = DefaultProfile::getProfile('cn-hangzhou',
                                      $access_key_id,
                                      $access_key_secret);
     $mts_client = new DefaultAcsClient($profile);
    ```

    Print the output URLs and basic information of all transcoding tasks.

    ```
    If (strbmp ($ json_message-> {'type'}, 'report ') = 0 ){
          $activities = $json_message->{'MediaWorkflowExecution'}->{'ActivityList'};
          $transcode_job_ids = Array();
          for ($i=0; $i < count($activities); $i++) {
            if (strcmp($activities[$i]->{'Type'}, 'Transcode') == 0) {
              $transcode_job_ids[] = $activities[$i]->{'JobId'};
            }
          }
          $request = new Mts\QueryJobListRequest();
          $request->setJobIds(join(',', $transcode_job_ids));
          $request->setRegionId('cn-hangzhou');
          $response = $mts_client->getAcsResponse($request);
          for ($i=0; $i < count($response->{'JobList'}->{'Job'}); $i++) {
            $output = $response->{'JobList'}->{'Job'}[$i]->{'Output'};
            $output_file = $response->{'JobList'}->{'Job'}[$i]->{'Output'}->{'OutputFile'};
            $video_properties = $response->{'JobList'}->{'Job'}[$i]->{'Output'}->{'Properties'};
            echo 'URLs of the transcoding output files'.'http://'.$output_file->{'Bucket'}.'.'.
                            $output_file->{'Location'}.'.aliyuncs.com/'.
                            urldecode($output_file->{'Object'})."\n";
            echo 'basic information of the transcoding output files'.$video_properties->{'Width'}.'x'.$video_properties->{'Height'}.
                            ' duration:'.$video_properties->{'Duration'}."\n";
          }
     }
    ```

    Print the output URLs of all screenshot tasks.

    ```
    if (strcmp($json_message->{'Type'}, 'Report') == 0) {
          $activities = $json_message->{'MediaWorkflowExecution'}->{'ActivityList'};
          $snapshot_job_ids = Array();
          for ($i=0; $i < count($activities); $i++) {
            if (strcmp($activities[$i]->{'Type'}, 'Snapshot') == 0) {
              $snapshot_job_ids[] = $activities[$i]->{'JobId'};
            }
          }
          $request = new Mts\QuerySnapshotJobListRequest();
          $request->setSnapshotJobIds(join(',', $snapshot_job_ids));
          $request->setRegionId('cn-hangzhou');
          $response = $mts_client->getAcsResponse($request);
          for ($i=0; $i < count($response->{'SnapshotJobList'}->{'SnapshotJob'}); $i++) {
            $snapshot_config = $response->{'SnapshotJobList'}->{'SnapshotJob'}[$i]->{'SnapshotConfig'};
            $output_file = $response->{'SnapshotJobList'}->{'SnapshotJob'}[$i]->{'SnapshotConfig'}->{'OutputFile'};
            echo 'URLs of the screenshot output files'.'http://'.$output_file->{'Bucket'}.'.'.
                            $output_file->{'Location'}.'.aliyuncs.com/'.
                            urldecode($output_file->{'Object'})."\n";
          }
     }
    ```


