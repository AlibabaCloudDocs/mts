# iOS version {#concept_m42_q1v_y2b .concept}

## Environment requirements {#section_vhq_r1v_y2b .section}

iOS 7.0 or a later version

## Installation {#section_e4r_s1v_y2b .section}

[OSS iOS SDK](https://github.com/aliyun/aliyun-oss-ios-sdk/)

[Download the upload SDK](reseller.en-US/SDK Reference/Upload SDK/Upload SDK.md#)

-   Directly introduce the frameworks

    Introduce the frameworks of the OSS iOS SDK and VODUpload iOS SDK.

    In Xcode, drag the frameworks and drop them to your target, and select “Copy items if needed” in the displayed dialog box.

-   Introduce the header file to your project

    ```
    #import <VODUpload/VODUploadClient.h>
    ```

    **Note:** After you introduce the frameworks, add `-ObjC` to `Other Linker Flags` of `Build Settings` in your project. If the `-force_load` option has been configured for your project, add `-force_load <framework path>/AliyunOSSiOS`.

-   Compatible with IPv6-Only networks.

    The OSS mobile SDK has introduced the HTTPDNS for domain name resolution to avoid domain name resolution hijacking in a wireless network and directly uses IP addresses for requests to the server. In an IPv6-Only network, compatibility issues may occur. The app officially issued the review requirements for apps, requiring apps to be IPv6-only network compatible. To this end, the SDK starts to be compatible from `V2.5.0`. In the new version, apart from `-ObjC` settings, two system libraries must be introduced:

    ```
    libresolv.tbd
    SystemConfiguration.framework
    ```


## Create a VODUpload instance {#section_wn4_hbv_y2b .section}

Set the callback function.

```
OnUploadStartedListener testUploadStartedCallbackFunc = ^(UploadFileInfo* fileInfo) {
      NSLog(@"upload started .") ;
  };
 OnUploadSucceedListener testSuccessCallbackFunc = ^(NSString* filePath){
    NSLog(@"file:%@ upload success!", filePath);
 };
 OnUploadFailedListener testFailedCallbackFunc = ^(NSString* filePath, NSString* code, NSString* message){
    NSLog(@"failed code = %@, error message = %@", code, message);
 };
 //  Unit: byte
 OnUploadProgressListener testProgressCallbackFunc = ^(NSString* filePath, long uploadedSize, long totalSize) {
    NSLog(@"progress uploadedSize : %li, totalSize : %li", uploadedSize, totalSize);
 };
 OnUploadTokenExpiredListener testTokenExpiredCallbackFunc = ^{
    NSLog(@"*token expired.");
    // get token and call resmeUploadWithAuth.
 };
 OnUploadRertyListener testUploadRertyListener = ^{
    NSLog(@"retry begin.") ;
 };
 OnUploadRertyResumeListener testUploadRertyResumeListener = ^{
    NSLog(@"retry resume.") ;
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

## Initialize the upload SDK {#section_uds_rjv_y2b .section}

Enter the authorization information in either of the following ways:

-   AccessKey

    It is simple but not safe. It is recommended that this way be used in the test environment.

    ```
    VODUploadClient *uploader;
     [uploader init:<accessKeyId>
              accessKeySecret:<accessKeySecret>
              listener:listener];
    ```

-   Token

    It is safe but complex. It is recommended that this way be used in the production environment. A token is temporary and valid for a period. Therefore, sending a token is safe.

    ```
    VODUploadClient *uploader;
     [uploader init:<accessKeyId>
              accessKeySecret:<accessKeySecret>
              secretToken:<secretToken>
              expireTime:<expireTime>
              listener:listener];
    ```

-   List Management
    -   Add a file to be uploaded.

        **Note:** The file size cannot exceed 4 GB.

        ```
        [uploader addFile:<uploadFilePath>
                endpoint:<endpoint> //Example: 'http://oss-cn-hangzhou.aliyuncs.com'
                bucket:<bucketName> //Enter the actual bucket name
                object:<objectKey>];
        ```

        During uploading, obtain the attributes \(the title, tag, description, category, cover URL, and custom data\) of a media set in the following way: addFile contains a reload function, in which the last parameter is a VodInfo object. The definitions are as follows:

        ```
        @interface VodInfo : NSObject
        @property (nonatomic, strong) NSString* title;
        @property (nonatomic, strong) NSString* tags;
        @property (nonatomic, strong) NSString* desc;
        @property (nonatomic, strong) NSNumber* cateId;
        @property (nonatomic, strong) NSString* userData;
        @property (nonatomic, strong) NSString* coverUrl;
        ```

    -   Delete the uploaded file.

        ```
        [uploader deleteFile:<index>];
        ```

    -   Cancel upload of a single file in the list.

        ```
        [uploader cancelFile:<index>];
        ```

    -   Resume upload of a single file in the list.

        ```
        [uploader resumeFile:<index>]; 
        ```

    -   Obtain the upload file list.

        ```
        [uploader listFiles];
        ```

    -   Clear the upload file list.

        ```
        [uploader clearFiles];
        ```


## Upload control {#section_b1q_kkv_y2b .section}

-   Start upload.

    ```
    [uploader start];
    ```

-   Stop upload.

    ```
    [uploader stop];
    ```

-   Pause upload.

    ```
    [uploader pause];
    ```

-   Resume upload.

    ```
    [uploader resume];
    ```

-   Resume upload after the token is invalid.

    ```
    [uploader resumeWithToken:<accessKeyId>
              accessKeySecret:<accessKeySecret>
              secretToken:<secretToken>
              expireTime:<expireTime>]
    ```


