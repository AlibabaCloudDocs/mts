# HLS标准加密 {#concept_mhv_cbw_1fb .concept}

视频加密是对视频内容保护的一种手段，对视频中的内容进行加密，可有效防止视频泄露和盗链问题，广泛用于在线教育及财经等领域。

**说明：** 阿里云目前支持两种加密方式: 私有加密 和 HLS标准加密，HLS标准加密需要客户自己保护密钥，此文档介绍HLS标准加密。

## 加密架构 {#section_ssn_2bw_1fb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11402/156568231211385_zh-CN.png)

## 术语介绍 {#section_c54_3bw_1fb .section}

-   秘钥管理服务（Key Management Service，简称KMS）

    一项安全管理服务，主要负责数据秘钥的生产、加密、解密等工作。开通请 [单击这里](https://common-buy.aliyun.com/?spm=a2c4g.11186623.2.4.25be5ef3sQ2xvL&commodityCode=kms#/open)。

-   数据秘钥（Data Key，简称DK）也称明文密钥

    DK为加密数据使用的明文数据密钥。

-   信封数据密钥（Enveloped Data Key，简称EDK）也称密文密钥

    EDK为通过信封加密技术保密后的密文数据密钥。

-   访问控制（Resource Access Management 简称RAM）

    是阿里云为客户提供的用户身份管理与资源访问控制服务。开通请 [单击这里](https://www.aliyun.com/product/ram?spm=a2c4g.11186623.2.5.25be5ef3sQ2xvL)。


## 操作流程 {#section_mj3_kbw_1fb .section}

1.  创建HLS加密工作流。

    **说明：** 控制台支持创建HLS加密工作流。如需通过API进行创建，请查看demo，参见 [创建HLS标准加密工作流](../../../../cn.zh-CN/SDK参考/媒体转码SDK/Java SDK/创建HLS标准加密工作流.md#)。创建好后，不要在控制台对其修改，会使加密配置失效。

    工作流中关键配置：

    -   开始活动节点：`InputFile:{"Bucket":"bucketdemo", "Location ":"oss-cn-hangzhou", "ObjectPrefix":"HLS-Encryption"}` 

        此配置表示内容创作者上传视频到杭州 oss://bucketdemo/HLS-Encryption 这个路径下会自动触发加密转码。

    -   转码活动节点：`Encryption:{"Type":"hls-aes-128", "KeyUri":"https://decrypt.demo.com"}` 

        转码完成后，KeyUri的配置会出现在m3u8文件中，供播放器使用。

        播放时播放器会携带EDK密文密钥请求这个地址，以获取DK明文密钥，进行播放。

2.  上传视频。

    两种方法上传视频，都会自动触发加密转码。

    -   通过MPS控制台上传视频至刚刚创建的工作流。
    -   通过OSS上传工具上传视频至oss://bucketdemo/HLS-Encryption路径。
    转码完成后，m3u8文件内容示例。

    ``` {#codeblock_298_rx6_gob}
    #EXTM3U
         #EXT-X-VERSION:3
         #EXT-X-TARGETDURATION:5
         #EXT-X-MEDIA-SEQUENCE:0
         #EXT-X-KEY:METHOD=AES-128,URI="https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271"
         #EXTINF:4.127544,
         15029611683170-00001.ts
         #EXT-X-ENDLIST
    ```

3.  播放。
    -   获取播放地址，可通过查询媒体接口，参见 [查询媒体-使用媒体ID](../../../../cn.zh-CN/API参考/媒体接口/查询媒体-使用媒体ID.md#) 获取OSS地址，然后把OSS域名，替换为CDN域名, 再拼接上参数MtsHlsUriToken，此参数会作为请求解密密钥的令牌，以下为原理。

        播放时，播放器会访问m3u8文件中EXT-X-KEY标签中的URI以获取解密秘钥，此URI为业务方搭建的解密密钥接口，只允许合法用户访问。 因此，需要播放器在请求解密时，携带一些业务方承认的认证信息。MtsHlsUriToken就是这个作用，业务方颁发一令牌给播放器， 播放器请求解密密钥时，携带此令牌，业务方验证令牌的合法性。

    -   播放器携带令牌，业务方验证服务。

        例如，正常的播放地址为：`https://vod.demo.com/test.m3u8`, 当拼接携带`MtsHlsUriToken`参数后为`https://vod.demo.com/test.m3u8?MtsHlsUriToken=业务方颁发的令牌`。

        播放时，播放器向阿里CDN请求`https://vod.demo.com/test.m3u8?MtsHlsUriToken=业务方颁发的令牌`，阿里CDN会动态修改m3u8文件中的解密URI，如原为`https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271`，修改后为 `https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271&MtsHlsUriToken=业务方颁发的令牌`。

        所以，播放器最终请求解密URI为：`https://decrypt.demo.com?Ciphertext=aabbccddeeff&MediaId=fbbf98691ea44b7c82dd75c5bc8b9271&MtsHlsUriToken=业务方颁发的令牌`。此地址中，携带了业务方搬发的令牌，业务方进行验证即可。

4.  业务方需要完成以下操作。
    1.  搭建颁发及验证MtsHlsUriToken令牌服务。
    2.  校验解密令牌，推荐一个令牌只允许使用一次。
    3.  解密密钥：EDK即Ciphertext，此时，要调用KMS服务的解密接口进行解密，参见 [Decrypt](../../../../cn.zh-CN/API 参考/API列表/Decrypt.md#)。 解密后，可缓存，以减少不必要的网络IO。
    4.  解密拿到DK即明文密钥，需要base64decode，然后返回给播放器。

