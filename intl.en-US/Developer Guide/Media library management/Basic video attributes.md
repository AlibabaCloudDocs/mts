# Basic video attributes {#concept_qrr_fnv_1fb .concept}

## Overview {#section_fzm_vnv_1fb .section}

The following example describes how to query and update the basic information of a media set. For more information about how to install and use the SDK, see [Media library SDK-PHP](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Overview.md#).

## Query the basic information of a media set {#section_usl_xnv_1fb .section}

You can use the media ID or OSS file URL to query a media set.

-   Query a media set by media ID

    For more information about the parameters, see [API reference \> Media APIs \> Query media sets by media IDs](../../../../reseller.en-US/API Reference/Media APIs/QueryMediaList.md#).

    ```
    include_once 'aliyun-php-sdk-core/Config.php';
    use Mts\Request\V20140618 as Mts;
    $accessKeyID = 'test'; //eplace the value with your AccessKeyID
    $accessKeySecret = 'test'; //Replace the value with your AccessKeySecret
    $profile = DefaultProfile::getProfile('cn-hangzhou',
                                          $accessKeyID,
                                          $accessKeySecret);
    $client = new DefaultAcsClient($profile);
    ```

    ```
    function queryMediaById($client, $mediaID)
    {
         $request = new Mts\QueryMediaListRequest();
         $request->setAcceptFormat('JSON');
         $request->setMediaIds($mediaID);
         $response = $client->getAcsResponse($request);
         return $response;
    }
    function printMedia($media)
    {
         if (array_key_exists('Title', $media)) {
           print_r('Title: '.$media->{'Title'}."\n");
         }
         if (array_key_exists('Description', $media)) {
           print_r('Description: '.$media->{'Description'}."\n");
         }
         if (array_key_exists('Tags', $media)) {
           print_r('Tags: '.$media->{'Tags'}->{'Tag'}[0]."\n");
         }
         if (array_key_exists('CoverURL', $media)) {
           print_r('CoverURL: '.$media->{'CoverURL'}."\n");
         }
         print_r('Format: '.$media->{'Format'}."\n");
         print_r('Resolution: '.$media->{'Width'}.'x'.$media->{'Height'}."\n");
         print_r('FileSize: '.$media->{'Size'}."\n");
         print_r('Bitrate: '.$media->{'Bitrate'}."\n");
         print_r('FPS: '.$media->{'Fps'}."\n");
    }
    $mediaID = 'test'; // Replace the value with your desired media ID
    $medias = queryMediaById($client, $mediaID)->{'MediaList'}->{'Media'};
    for ($i=0; $i < count($medias); $i++) {
         printMedia($medias[$i]);
    }
    ```

-   Query a media set by an OSS file URL

    For more information about the parameters, see [API reference \> Media APIs \> Query media sets by URLs](../../../../reseller.en-US/API Reference/Media APIs/QueryMediaListByURL.md#).

    ```
    function queryMediaByURL($client, $mediaURL)
    {
         $request = new Mts\QueryMediaListByURLRequest();
         $request->setAcceptFormat('JSON');
         $request->setFileURLs($mediaURL);
         $response = $client->getAcsResponse($request);
         return $response;
    }
    $ossEndpoint = 'http://test.oss-cn-hangzhou.aliyuncs.com/';
    // An OSS object does not have to start with "/". Replace the value with your OSS object
    $ossObject = 'test/test.mp4';
    $medias = queryMediaByURL($client,$ossEndpoint.urlencode($ossObject))->{'MediaList'}->{'Media'};
    for ($i=0; $i < count($medias); $i++) {
         printMedia($medias[$i]);
    }
    ```

-   Update attributes

    You can update full attributes or a single attribute.

    -   Full attribute update

        For more information about about the parameters, see [API reference \> Media APIs \> Update media set basic information](../../../../reseller.en-US/API Reference/Media APIs/UpdateMedia.md#).

        Specify all fields when updating attributes. Fields not set are cleared.

        ```
        function updateMediaAllField($client, $mediaID, $title, $description, $tags, $coverURL)
        {
             $request = new Mts\UpdateMediaRequest();
             $request->setAcceptFormat('JSON');
             $request->setMediaId($mediaID);
             $request->setTitle($title);
             $request->setCateId(2663987);
             $request->setDescription($description);
             $request->setTags($tags);
             $request->setCoverURL($coverURL);
             $response = $client->getAcsResponse($request);
             return $response;
        }
        $mediaID = 'test'; //Replace the value with your desired media ID
        $media = updateMediaAllField($client, $mediaID,
                                'title', 'description', 'tags', 'coverURL')->{'Media'};
        ```

    -   Single attribute update

        You can use different APIs to conveniently update single fields without modifying other fields.

        The following section uses the “publishing state” as an example. For more information about the parameters, see [API reference \> Media APIs \> Update media publishing state](../../../../reseller.en-US/API Reference/Media APIs/UpdateMediaPublishState.md#).

        ```
        function updateMediaPublishState($client, $mediaID, $state)
        {
             $request = new Mts\UpdateMediaPublishStateRequest();
             $request->setAcceptFormat('JSON');
             $request->setMediaId($mediaID);
             $request->setPublish($state);
             $response = $client->getAcsResponse($request);
             return $response;
        }
        $mediaID = 'test'; //Replace the value with your desired media ID
        //No result is returned from the API that updates the publishing state. Capture exceptions to check whether execution succeeds
        try {
             updateMediaPublishState($client, $mediaID, "true");
        } catch(ClientException $e) {
             print_r('ClientException:'."\n");
             print_r($e);
        } catch (ServerException $e) {
             print_r('ServerException:'."\n");
             print_r($e);
        }
        ```


