# Android版本 {#concept_vpn_yw5_y2b .concept}

本节主要介绍Android版本的环境要求，安装、创建VODUpload实例、初始化、列表管理和上传控制。

## 环境要求 {#section_mks_1x5_y2b .section}

Android系统版本：2.3 及以上

## 安装 {#section_x5s_bx5_y2b .section}

[OSS Android SDK](https://github.com/aliyun/aliyun-oss-android-sdk/)

[上传SDK下载](intl.zh-CN/SDK参考/上传SDK/上传SDK下载.md#)

**直接引入jar包**

当您下载了VODUpload Android SDK的zip包后，进行以下步骤（对Android studio或者Eclipse都适用）。

1.  解压后在libs目录下得到jar包，目前包括aliyun-oss-sdk-android-xxx.jar、okhttp-2.7.0.jar、okio-2.6.0.jar、aliyun-vod-upload-android-sdk-xxx.jar。
2.  将以上4个jar包导入工程的libs目录。
3.  设置权限。

    以下是VODUpload Android SDK所需要的Android权限，请确保您的AndroidManifest.xml文件中已经配置了这些权限，否则，SDK将无法正常工作。

    ```
    <uses-permission android:name="android.permission.INTERNET"></uses-permission>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"></uses-permission>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
    ```


## 创建VODUpload实例 {#section_iyt_3x5_y2b .section}

您需要在这里设置回调函数：

```
VODUploadCallback callback = new VODUploadCallback() {
    /**
    * 文件开始上传时触发
    */
    void onUploadStarted() {;}
    /**
    * 上传成功回调
    */
    void onUploadSucceed(UploadFileInfo info) {;}
    /**
    * 上传失败
    */
    void onUploadFailed(UploadFileInfo info, String code, String message) {;}
    /**
    * 回调上传进度
    * @param uploadedSize 已上传字节数
    * @param totalSize 总共需要上传字节数
    */
    void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize) {;}
    /**
    * 上传凭证过期后，会回调这个接口
    * 可在这个回调中获取新的上传，然后调用resumeUploadWithAuth继续上传
    */
    void onUploadTokenExpired() {;}
    /**
    * 上传过程中，状态由正常切换为异常时触发
    */
    void onUploadRetry(String code, String message) {;}
    /**
    * 上传过程中，从异常中恢复时触发
    */
    void onUploadRetryResume() {;}
};
VODUploadClient uploader = new VODUploadClientImpl(getContext());
```

## 初始化 {#section_hvr_lx5_y2b .section}

填写授权信息，有2种方式：

-   AK方式

    简单但是不够安全，建议您在测试环境下使用。

    ```
    uploader.init("<accessKeyId>", "<accessKeySecret>", callback);
    ```

-   安全令牌方式

    安全但是较为复杂，建议您在生产环境下使用。安全令牌是临时、有时效性的，所以传递安全令牌是安全的。

    ```
    uploader.init("<accessKeyId>", "<accessKeySecret>", "<secretToken>", "<expireTime>", callback);
    ```


## 列表管理 {#section_jtm_rx5_y2b .section}

-   添加上传文件。

    **说明：** 支持的文件大小≤4G。

    ```
    uploader.addFile("<uploadFilePath>",
                   "<endpoint>", // 例如杭州区域"http://oss-cn-hangzhou.aliyuncs.com"
                   "<bucketName>", // 按实际bucket名称填写
                   "<objectKey>");
    ```

    上传时，如何指定媒体的属性（标题、标签、描述、类目、封面URL、用户自定义数据）呢？addFile有一个重载函数，函数最后的参数是一个VodInfo对象。定义如下：

    ```
    private String title;
    private String desc;
    private Integer cateId;
    private List<String> tags;
    private String userData;
    private String coverUrl;
    ```

-   删除上传文件，`index`对应listFiles接口返回列表中元素的索引。

    ```
    uploader.deleteFile(index);
    ```

-   取消列表中的单个文件上传。

    ```
    uploader.cancelFile(index);
    ```

-   恢复列表中的单个文件上传。

    ```
    uploader.resumeFile(index);
    ```

-   获取上传文件列表。

    ```
    List list = uploader.listFiles();
    ```

-   清除上传文件列表。

    ```
    upload.clearFiles();
    ```


## 上传控制 {#section_r1c_dy5_y2b .section}

-   开始上传。

    ```
    uploader.start();
    ```

-   停止上传。

    ```
    uploader.stop();
    ```

-   暂停上传。

    ```
    uploader.pause();
    ```

-   恢复上传。

    ```
    uploader.resume();
    ```

-   安全令牌失效后恢复上传。

    ```
    uploader.resumeWithToken("<accessKeyId>", "<accessKeySecret>", "<secretToken>", "<expireTime>");
    ```


