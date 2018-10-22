# Tag management {#concept_d2k_twv_1fb .concept}

## Overview {#section_tmq_5wv_1fb .section}

For more information about how to install and use the SDK, see [Media library SDK-PHP](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Overview.md#).

The media repository does not provide global tag management and setting. Tags of each media set are independent. You can search for APIs of a media set to query all media sets that have the same tags.

The tag-related APIs support addition and deletion of a single tag. You can use [UpdateMedia](../../../../reseller.en-US/API Reference/Media APIs/UpdateMedia.md#) to set multiple tags at a time.

## Add a tag {#section_vkl_vwv_1fb .section}

For more information about the parameters, see [API reference \> Media APIs \> Add a media tag](../../../../reseller.en-US/API Reference/Media APIs/AddMediaTag.md#).

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
function addMediaTag($client, $mediaID, $tag)
  {
      $request = new Mts\AddMediaTagRequest();
      $request->setAcceptFormat('JSON');
      $request->setMediaId($mediaID);
      $request->setTag($tag);
      $response = $client->getAcsResponse($request);
      return $response;
  }
  $mediaID = 'test'; //Replace the value with your desired media ID
  //No result is returned from the API. Capture exceptions to check whether execution succeeds
  try {
      addMediaTag($client, $mediaID, "testtag");
  } catch(ClientException $e) {
      print_r('ClientException:'."\n");
      print_r($e);
  } catch (ServerException $e) {
      print_r('ServerException:'."\n");
      print_r($e);
  }
```

## Delete a tag {#section_jnw_ywv_1fb .section}

For more information about the parameters, see [API reference \> Media APIs \> Delete a media tag](../../../../reseller.en-US/API Reference/Media APIs/DeleteMediaTag.md#).

```
function deleteMediaTag($client, $mediaID, $tag)
  {
      $request = new Mts\DeleteMediaTagRequest();
      $request->setAcceptFormat('JSON');
      $request->setMediaId($mediaID);
      $request->setTag($tag);
      $response = $client->getAcsResponse($request);
      return $response;
  }
  $mediaID = 'test'; //Replace the value with your desired media ID
  //No result is returned from the API. Capture exceptions to check whether execution succeeds
  try {
      deleteMediaTag($client, $mediaID, "testtag");
  } catch(ClientException $e) {
      print_r('ClientException:'."\n");
      print_r($e);
  } catch (ServerException $e) {
      print_r('ServerException:'."\n");
      print_r($e);
  }
```

