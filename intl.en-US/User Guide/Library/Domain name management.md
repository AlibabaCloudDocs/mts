# Domain name management {#concept_ovj_dmy_w2b .concept}

1.  Log on to the [CCDN console](https://partners-intl.aliyun.com/login-required#/cdn).
2.  Click **Domain Names**.
3.  Click **Add Domain Name**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11359/15392613809992_en-US.png)

4.  Enter domain name information and click **Next**.

    **Domain Name**: Set this parameter to your on-demand CDN domain name.

    **Business Type**: Set this parameter to **Acceleration of On-demand Video/Audio**.

    **Origin Site Type**: Set this parameter to the OSS bucket bound to the**Output Media Bucket**.

    **Note:** The CDN origin site does not support the OSS bucket whose read/write permission is **Private**. Log on to the [OSS console](https://partners-intl.aliyun.com/login-required#/oss) and verify that the read/write permission is **Public-read**.

5.  Review and configure the domain name.

    If your domain name has been filed, the review is quickly completed. Click **Domain name configuration** to go to the configuration page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11359/15392613809994_en-US.png)

    1.  Configure DNS resolution for the on-demand CDN domain**CNAME**.

        Configure the CNAME at the location of your DNS service provider. For more information, seeUse HiChina CNAME to access CDN, Use DNSPod CNAME to access CDN, and Use Xinnet CNAME to access CDN.

    2.  Configure **Back-to-source Host**.

        Configure the **Back-to-source Host**to**Origin Site Domain Name**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11359/15392613809995_en-US.png)

    3.  Enable **Enable Drag/Drop Playback**.

        After this function is enabled, CDN allows the Alibaba Cloud Web player to play back MP4 and FLV files through drag and drop operations.

        Drag/drop playback is supported for M3U8 files even if this function is not enabled.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11359/15392613809996_en-US.png)


