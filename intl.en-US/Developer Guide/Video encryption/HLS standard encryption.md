# HLS standard encryption {#concept_mhv_cbw_1fb .concept}

Video encryption is a measure to protect the video content. Encrypting the video content can effectively avoid video leaks and leeching problems, thus being widely used in online education, finance and economics and other fields.

**Note:** Alibaba Cloud currently supports encryption in two ways. One is private encryption, and the other is HLS standard encryption. Using HLS standard encryption, users must protect the encryption key. This document introduces HLS standard encryption.

## Complete encryption architecture {#section_ssn_2bw_1fb .section}

![](images/11385_en-US.png)

## Terms {#section_c54_3bw_1fb .section}

-   Key Management Service \(KMS\)

    A security management service, mainly responsible for the production, encryption and deceyption of data key and other operations.

-   Data Key \(DK\), also called plaintext key

    DK is plaintext data key used in data encryption.

-   Enveloped Data Key \(EDK\), also called ciphertext key.

    EDK is the ciphertext data key, encrypted by using envelope encryption technology.

-   Resource Access Management \(RAM\)

    User identification management and resource access management service provided by Alibaba Cloud.


## Procedure {#section_mj3_kbw_1fb .section}

1.  Create HLS encryption workflow.

    **Note:** The console currently does not support creating HLS encryption workflow. You can create HLS encryption workflow by using API. For more information about demo, see [Create HLS standard encryption workflow](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Java SDK/Create HLS standard encryption workflow.md#). After creating, the workflow cannot be modified on the console, or the encryption setting goes invalid.

    Key settings in workflow:

    -   Start activity node: `InputFile:{"Bucket":"bucketdemo", "Location ":"oss-cn-hangzhou", "ObjectPrefix":"HLS-Encryption"}`

        This setting indicates the content creater uploads a video under this path oss://bucketdemo/HLS-Encryption to Hangzhou, and encryption transcoding is triggered automatically.

    -   Transcoding activity node: `Encryption:{"Type":"hls-aes-128", "KeyUri":"https://decrypt.demo.com"}`

        After transcoding operation is completed, the setting of KeyUri appears in m3u8 file for player to use.

        During play, the player carries EDK ciphertext key to request the address so as to get DK plaintext key for play.

2.  Upload video.

    Either way to upload video can trigger encryption transcoding automatically.

    -   Upload the video to the created workflow by using the MPS console.
    -   Upload the video under the path oss://bucketdemo/HLS-Encryption by using OSS uploading tool.
    After transcoding is completed, the content of the m3u8 file is showned as follows.

    ```
    #EXTM3U
         #EXT-X-VERSION:3
         #EXT-X-TARGETDURATION:5
         #EXT-X-MEDIA-SEQUENCE:0
         #EXT-X-KEY:METHOD=AES-128,URI="https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271"
         #EXTINF:4.127544,
         15029611683170-00001.ts
         #EXT-X-ENDLIST
    ```

3.  Play.
    -   Use the QueryMediaList interface to get playback address. For more information, see [QueryMediaList](../../../../reseller.en-US/API Reference/Media APIs/QueryMediaList.md#). Get the OSS address, replace the OSS domain name with CDN domain name, and splice the parameterMtsHlsUriToken, which serves as the token to request the decryption key. The principle is as follows.

        During play, the player accesses the URI in the EXT-X-KEY tag in the m3u8 file to get decryption key. The URI is a decryption key interface built by the business side. Therefore, while requesting decryption, the player must carry some authentication information recognized by the business side. MtsHlsUriToken plays the role in a similar way. The business side issues a token to the player, which carries the token when requesting the decryption key, and the business side checks the validity of the token.

    -   The player carry the token to the business side for authentication service.

        For example, the normal playback address is `https://vod.demo.com/test.m3u8`. Splice and carry the parameter `MtsHlsUriToken`, the playback address is `https://vod.demo.com/test.m3u8?MtsHlsUriToken=Token issued by the business side`.

        During playback, the player request`https://vod.demo.com/test.m3u8? MtsHlsUriToken=Token issued by the business side` to CDN of Alibaba Cloud, and the CDN of Alibaba Cloud dynamically modifies the decryption URI in the m3u8 file. For example, the original `https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271` is modified to `https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271&MtsHlsUriToken=Token issued by the business side`.

        Therefore, the final decryption URI which the player requests is `https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271&MtsHlsUriToken=Token issued by the business side`. This address carries the token issued by the business side, which can be identified by the business side.

4.  The business side need to do the following operations.
    1.  Build, issue and identify MtsHlsUriToken service.
    2.  Identify decryption token. One token is allowed to use only once.
    3.  Decrypt key: EDK, which is Ciphertext, calls decryption interface of the KMS service for decryption. For more information, see [Decrypt](../../../../reseller.en-US/API Reference/API list/Decrypt.md#). After decryption, the information can be cached to reduce network IO.
    4.  After decryption, you can get DK \(the plaintext key\) which needs base64decodd, and return it to the player.

