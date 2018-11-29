# iOS版本 {#concept_m42_q1v_y2b .concept}

## 环境要求 {#section_vhq_r1v_y2b .section}

iOS系统版本：iOS 7.0以上。

## 安装 {#section_e4r_s1v_y2b .section}

[OSS iOS SDK](https://github.com/aliyun/aliyun-oss-ios-sdk/)

[上传SDK下载](intl.zh-CN/SDK参考/上传SDK/上传SDK下载.md#)

-   直接引入Framework。

    需要引入OSS iOS SDK framework和VODUpload iOS SDK framework。

    在Xcode中，直接把framework拖入您对应的Target下即可，在弹出框勾选Copy items if needed。

-   工程中引入头文件。

    ```
    #import <VODUpload/VODUploadClient.h>
    ```

    **说明：** 引入Framework后，需要在工程`Build Settings`的`Other Linker Flags`中加入`-ObjC`。如果工程此前已经设置过`-force_load`选项，那么，需要加入`-force_load <framework path>/AliyunOSSiOS`。

-   兼容IPv6-Only网络。

    OSS移动端SDK为了解决无线网络下域名解析容易遭到劫持的问题，已经引入了HTTPDNS进行域名解析，直接使用IP请求OSS服务端。在IPv6-Only的网络下，可能会遇到兼容性问题。而APP官方近期发布了关于IPv6-only网络环境兼容的APP审核要求，为此，SDK从`2.5.0`版本开始已经做了兼容性处理。在新版本中，除了`-ObjC`的设置，还需要引入两个系统库。

    ```
    libresolv.tbd
    SystemConfiguration.framework
    ```


## 创建VODUpload实例 {#section_wn4_hbv_y2b .section}

在这里需要设置回调函数

```
OnUploadStartedListener testUploadStartedCallbackFunc = ^(UploadFileInfo* fileInfo) {
      NSLog(@"upload started .");
  };
 OnUploadSucceedListener testSuccessCallbackFunc = ^(NSString* filePath){
    NSLog(@"file:%@ upload success!", filePath);
 };
 OnUploadFailedListener testFailedCallbackFunc = ^(NSString* filePath, NSString* code, NSString* message){
    NSLog(@"failed code = %@, error message = %@", code, message);
 };
 // 单位：字节
 OnUploadProgressListener testProgressCallbackFunc = ^(NSString* filePath, long uploadedSize, long totalSize) {
    NSLog(@"progress uploadedSize : %li, totalSize : %li", uploadedSize, totalSize);
 };
 OnUploadTokenExpiredListener testTokenExpiredCallbackFunc = ^{
    NSLog(@"*token expired.");
    // get token and call resmeUploadWithAuth.
 };
 OnUploadRertyListener testUploadRertyListener = ^{
    NSLog(@"retry begin.");
 };
 OnUploadRertyResumeListener testUploadRertyResumeListener = ^{
    NSLog(@"retry resume.");
 };
 VODUploadListener *listener;
 listener = [[VODUploadListener alloc] init];
 listener.started = testUploadStartedCallbackFunc;
 listener.success = testSuccessCallbackFunc;
 listener.failure = testFailedCallbackFunc;
 listener.progress = testProgressCallbackFunc;
 listener.expire = testTokenExpiredCallbackFunc;
 listener.retry = testUploadRertyListener;
 listener.retryResume = testUploadRertyResumeListener;
```

## 初始化 {#section_uds_rjv_y2b .section}

填写授权信息，有2种方式

-   AK方式

    简单但是不够安全，建议您在测试环境下使用。

    ```
    VODUploadClient *uploader;
     [uploader init:<accessKeyId>
              accessKeySecret:<accessKeySecret>
              listener:listener];
    ```

-   安全令牌方式

    安全但是较为复杂，建议您在生产环境下使用。安全令牌是临时、有时效性的，所以传递安全令牌是安全的。

    ```
    VODUploadClient *uploader;
     [uploader init:<accessKeyId>
              accessKeySecret:<accessKeySecret>
              secretToken:<secretToken>
              expireTime:<expireTime>
              listener:listener];
    ```

-   列表管理
    -   添加上传文件。

        **说明：** 支持的文件大小≤4G。

        ```
        [uploader addFile:<uploadFilePath>
                endpoint:<endpoint> //例如：'http://oss-cn-hangzhou.aliyuncs.com'
                bucket:<bucketName> //按实际bucket名称填写
                object:<objectKey>];
        ```

        上传时，如何指定媒体的属性（标题、标签、描述、类目、封面URL、用户自定义数据）呢？addFile有一个重载函数，函数最后的参数是一个VodInfo对象。定义如下：

        ```
        @interface VodInfo : NSObject
        @property (nonatomic, strong) NSString* title;
        @property (nonatomic, strong) NSString* tags;
        @property (nonatomic, strong) NSString* desc;
        @property (nonatomic, strong) NSNumber* cateId;
        @property (nonatomic, strong) NSString* userData;
        @property (nonatomic, strong) NSString* coverUrl;
        ```

    -   删除上传文件。

        ```
        [uploader deleteFile:<index>];
        ```

    -   取消列表中的单个文件上传。

        ```
        [uploader cancelFile:<index>];
        ```

    -   恢复列表中的单个文件上传。

        ```
        [uploader resumeFile:<index>]; 
        ```

    -   获取上传文件列表。

        ```
        [uploader listFiles];
        ```

    -   清理上传文件列表。

        ```
        [uploader clearFiles];
        ```


## 上传控制 {#section_b1q_kkv_y2b .section}

-   开始上传。

    ```
    [uploader start];
    ```

-   停止上传。

    ```
    [uploader stop];
    ```

-   暂停上传。

    ```
    [uploader pause];
    ```

-   恢复上传。

    ```
    [uploader resume];
    ```

-   安全令牌失效后恢复上传。

    ```
    [uploader resumeWithToken:<accessKeyId>
              accessKeySecret:<accessKeySecret>
              secretToken:<secretToken>
              expireTime:<expireTime>]
    ```


