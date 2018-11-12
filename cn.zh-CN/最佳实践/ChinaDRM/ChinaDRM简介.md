# ChinaDRM简介 {#concept_xpb_rx1_tfb .concept}

ChinaDRM是阿里视频云与获得ChinaDRM lab和好莱坞双认证的DRM服务商爱迪德（Irdeto）合作，推出的国内首款在云端部署的DRM解决方案。

目前，China DRM已经商业化，该方案满足广电行业的内容安全标准，适用于对媒体安全有要求的场景，比如：购买好莱坞版权视频等。

同时，我们正在研发基于Widevine、PlayReady和FairPlay等国际通用 DRM 协议的视频加密方案，进一步加固H5端内容安全。

单击了解[更多技术原理](https://www.atatech.org/articles/122667)。

## 使用须知 {#section_x2d_ry1_tfb .section}

-   使用ChinaDRM前，请联系您的商务经理，开通服务并获取产品报价。
-   播放视频需集成阿里云播放器SDK，目前仅支持Android与iOS移动端播放。

## 方案架构 {#section_mtd_vy1_tfb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61718/154200328931041_zh-CN.png)

## 操作步骤 {#section_qcd_yy1_tfb .section}

1.  创建DRM加密工作流。

    **说明：** 

    -   控制台暂不支持创建DRM加密工作流，请您通过API进行创建。查看demo，请参见 [创建DRM加密工作流](cn.zh-CN/最佳实践/ChinaDRM/创建Java版ChinaDRM工作流.md#)。
    -   转码模板需配置为m3u8格式。
    -   DRM加密工作流创建好后，不要在控制台对其修改，会使加密配置失效。
    工作流中关键配置：

    -   开始活动节点：

        ```
        InputFile:{"Bucket":"bucketdemo", "Location ":"oss-cn-hangzhou", "ObjectPrefix":"ChinaDRM_Encryption"}
        ```

        此配置表示内容创作者上传视频到杭州。

        `oss://bucketdemo/ChinaDRM_Encryption` 这个路径下会自动触发加密转码。

    -   转码活动节点：

        ```
        Encryption:{"Type":"ChinaDRM"}
        ```

2.  上传视频。

    使用以下两种方法上传视频，都会自动触发加密转码。

    -   通过MPS控制台上传视频至刚刚创建的工作流。
    -   通过OSS上传工具上传视频至工作流输入节点配置的路径。
    转码完成后，m3u8文件内容示例。

    ```
    #EXTM3U
         #EXT-X-VERSION:3
         #EXT-X-TARGETDURATION:5
         #EXT-X-MEDIA-SEQUENCE:0
         #EXT-X-KEY:METHOD=AES-128,URI="http://mts.cn-shanghai.aliyuncs.com?DRMServerId=9b2eebe9ced3db90b363c100f8235a2081d14b11&ContentId=56001d830cc84934b424263ba63d6ba9&KeyId=56001d83-0cc8-4934-b424-263ba63d6ba9",IV=0x990d430cc18c44e49417f59b0df5d061,KEYFORMAT="chinadrm",KEYFORMATVERSIONS="1"
         #EXTINF:4.127544,
         15029611683170-00001.ts
         #EXT-X-ENDLIST
    ```

3.  播放。

    关于播放器SDK，详情参见[播放器SDK](../../../../cn.zh-CN/SDK参考/播放器SDK.md#)。


