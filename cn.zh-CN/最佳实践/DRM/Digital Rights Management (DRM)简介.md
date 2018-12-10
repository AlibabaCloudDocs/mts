# Digital Rights Management \(DRM\)简介 {#concept_xpb_rx1_tfb .concept}

目前，媒体处理服务支持ChinaDRM和Widevine两种DRM视频加密方案。同时，我们正在研发基于PlayReady和FairPlay等国际通用 DRM 协议的视频加密方案，进一步加固H5端内容安全。

ChinaDRM是阿里视频云与获得ChinaDRM lab和好莱坞双认证的DRM服务商爱迪德（Irdeto）合作，推出的国内首款在云端部署的DRM解决方案。目前，China DRM已经商业化，该方案满足广电行业的内容安全标准，适用于对媒体安全有要求的场景，比如：购买好莱坞版权视频等。

单击了解[更多技术原理](https://www.atatech.org/articles/122667)。

## 使用须知 {#section_x2d_ry1_tfb .section}

-   使用ChinaDRM/Widevine前，请联系您的商务经理，获取产品报价。
-   使用ChinaDRM/Widevine前，请您先 [开通DRM服务](https://common-buy.aliyun.com/?commodityCode=mts_drm#/buy)。
-   ChinaDRM/Widevine目前仅支持上海区域。
-   播放视频需集成阿里云播放器SDK，目前仅支持Android与iOS移动端播放。

## 方案架构 {#section_mtd_vy1_tfb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61718/154440807031041_zh-CN.png)

## ChinaDRM操作步骤 {#section_qcd_yy1_tfb .section}

1.  创建 ChinaDRM加密工作流。

    **说明：** 

    -   控制台暂不支持创建ChinaDRM加密工作流，请您通过API进行创建。查看demo，参见 [如何创建Java版ChinaDRM加密工作流](cn.zh-CN/最佳实践/DRM/ChinaDRM工作流/如何创建Java版ChinaDRM工作流.md#)。
    -   转码模板需配置为m3u8格式。
    -   DRM加密工作流创建好后，请您不要在控制台对其修改，会使加密配置失效。工作流中关键配置：
        -   开始活动节点：

            ```
            InputFile:{"Bucket":"bucketdemo", "Location ":"oss-cn-shanghai", "ObjectPrefix":"ChinaDRM_Encryption"}
            ```

            此配置表示内容创作者上传视频到上海。

            ```
            oss://bucketdemo/ChinaDRM_Encryption
            ```

            这个路径下会自动触发加密转码。

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

    关于播放器SDK，参见 [播放器SDK](../../../../cn.zh-CN/SDK参考/播放器SDK.md#)。


## Widevine操作步骤 {#section_p1m_hmc_bgb .section}

1.  创建 Widevine。

    **说明：** 

    -   控制台暂不支持创建Widevine加密工作流，请您通过API进行创建。查看demo，参见 [如何创建Java版Widevine工作流](cn.zh-CN/最佳实践/DRM/Widevine工作流/如何创建Java版Widevine工作流.md#)。
    -   转码模板需配置为mpd格式。
    -   DRM加密工作流创建好后，请您不要在控制台对其修改，会使加密配置失效。工作流中关键配置：
        -   开始活动节点：

            ```
            InputFile:{"Bucket":"bucketdemo", "Location ":"oss-cn-shanghai", "ObjectPrefix":"DRM/WidevineEncryption"}
            ```

            此配置表示内容创作者上传视频到上海。

            ```
            oss://bucketdemo/DRM/WidevineEncryption
            ```

            这个路径下会自动触发加密转码。

        -   转码活动节点：

            ```
            Encryption:{"Type":"Widevine"}
            ```

2.  上传视频。

    使用以下两种方法上传视频，都会自动触发加密转码。

    -   通过MPS控制台上传视频至刚刚创建的工作流。
    -   通过OSS上传工具上传视频至工作流输入节点配置的路径。
    转码完成后，mpd文件内容示例。

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:cenc="urn:mpeg:cenc:2013" mediaPresentationDuration="PT600.226S" minBufferTime="PT0.021539480521579S" profiles="urn:mpeg:dash:profile:isoff-live:2011" type="static">
    <Period>
    	<AdaptationSet contentType="video" segmentAlignment="true">
    		<ContentProtection cenc:default_KID="f00987db-3122-4a06-9bd9-ca92c7eca48d" schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc"/>
    		<ContentProtection schemeIdUri="urn:uuid:edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
    			<cenc:pssh>AAAAWHBzc2gAAAAA7e+LqXnWSs6jyCfc1R0h7QAAADgIARIQ8AmH2zEiSgab2cqSx+ykjSIgZjAwOTg3ZGIzMTIyNGEwNjliZDljYTkyYzdlY2E0OGQ4AQ==</cenc:pssh>
    		</ContentProtection>
    		<Representation bandwidth="369378" mimeType="video/mp4" codecs="avc1.640015" id="360p" width="636" height="270" scanType="progressive">
    			<SegmentTemplate initialization="videoLD/init-stream1.m4s" media="videoLD/stream1-$Number$.m4s" startNumber="1" timescale="13978">
    				<SegmentTimeline>
    					<S d="139920"/>
    					<S d="63547"/>
    				</SegmentTimeline>
    			</SegmentTemplate>
    		</Representation>
    		<Representation bandwidth="1159436" mimeType="video/mp4" codecs="avc1.64001F" id="720p" width="1356" height="576" scanType="progressive">
    			<SegmentTemplate initialization="videoHD/init-stream1.m4s" media="videoHD/stream1-$Number$.m4s" startNumber="1" timescale="13978">
    				<SegmentTimeline>
    					<S d="139920"/>
    					<S d="63547"/>
    				</SegmentTimeline>
    			</SegmentTemplate>
    		</Representation>
    		<Representation bandwidth="897301" mimeType="video/mp4" codecs="avc1.64001F" id="480p" width="1120" height="476" scanType="progressive">
    			<SegmentTemplate initialization="videoSD/init-stream1.m4s" media="videoSD/stream1-$Number$.m4s" startNumber="1" timescale="13978">
    				<SegmentTimeline>
    					<S d="139920"/>
                          <S d="63547"/>
    				</SegmentTimeline>
    			</SegmentTemplate>
    		</Representation>
    	</AdaptationSet>
    	<AdaptationSet contentType="audio" segmentAlignment="true" lang="chinese">
    		<ContentProtection cenc:default_KID="f00987db-3122-4a06-9bd9-ca92c7eca48d" schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc"/>
    		<ContentProtection schemeIdUri="urn:uuid:edef8ba9-79d6-4ace-a3c8-27dcd51d21ed">
    			<cenc:pssh>AAAAWHBzc2gAAAAA7e+LqXnWSs6jyCfc1R0h7QAAADgIARIQ8AmH2zEiSgab2cqSx+ykjSIgZjAwOTg3ZGIzMTIyNGEwNjliZDljYTkyYzdlY2E0OGQ4AQ==</cenc:pssh>
    		</ContentProtection>
    		<Representation bandwidth="128006" mimeType="audio/mp4" codecs="mp4a.40.2" id="chinese128k" audioSamplingRate="48000">
    			<AudioChannelConfiguration schemeIdUri="urn:mpeg:dash:23003:3:audio_channel_configuration:2011" value="2"/>
    			<SegmentTemplate initialization="audiocn/init-stream1.m4s" media="audiocn/stream1-$Number$.m4s" startNumber="1" timescale="48000">
    				<SegmentTimeline>
    					<S d="96016"/>
    				</SegmentTimeline>
    			</SegmentTemplate>
    		</Representation>
    	</AdaptationSet>
    </Period>
    </MPD>```
    ```


