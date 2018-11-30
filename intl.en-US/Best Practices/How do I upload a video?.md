# How do I upload a video? {#concept_hs4_4wk_x2b .concept}

## Background {#section_ckk_szk_x2b .section}

The following describes how to quickly build an audio and video file upload service based on the OSS service and MPS’s SDK upload.

## Benefits {#section_djr_tzk_x2b .section}

Uploading audio and video files using MPS’s SDK offers the following advantages:

-   Adds file list management.

-   Adds STS Token timeout update function.

-   Auto-retry function when network jitter occurs in the process of uploading.

-   File resume breakpoint function.

-   Workflow that automatically triggers the MPS service.

-   Configures media titles, tags, descriptions, categories, cover URLs, and more.

    **Note:** 

    -   Restrictions on resuming HTTP: does not allow cross-lifecycle. JS side page can not be refreshed, closed, and Android/iOS can not close the APP and mobile phone.
    -   The same local file can only be uploaded once.

## Server creation { .section}

Consider mobile AK security issues, choose STS to upload files. To learn how using STS increases the security of the upload, see [RAM and STS User Guide](../../../../reseller.en-US/Best Practices/Access control/Overview.md#).

## STS Activation Procedure {#section_azk_bfl_x2b .section}

1.  Activate the OSS service, create a bucket, and log on to the [OSS console](https://partners-intl.aliyun.com/login-required#/oss).
2.  Find the basic configuration area on the OSS overview page and click the **security token**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11376/154357086610124_en-US.png)

3.  Go to the **Security Token Shortcut Configuration** page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11376/154357086610125_en-US.png)

4.  Authorize automatically and save parameters in the text boxes. Click **Save AK Info** to close the dialog and complete STS activation.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11376/154357086610126_en-US.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11376/154357086610127_en-US.png)


## Build an application server {#section_whc_51l_x2b .section}

Configuration of app server sample code

This document provides three development example programs available for download in three languages.

-   Java: [Download](http://shinenuaa.oss-cn-hangzhou.aliyuncs.com/AppTokenServerDemo.zip?spm=a2c4g.11186623.2.10.5e9e2059meVW7L&file=AppTokenServerDemo.zip)

-   PHP: [Download](http://oss-demo.aliyuncs.com/app-server/sts-server.zip?spm=a2c4g.11186623.2.11.5e9e2059meVW7L&file=sts-server.zip)

-   Ruby:[Download](https://github.com/rockuw/sts-app-server?spm=a2c4g.11186623.2.12.5e9e2059meVW7L)


The download for each language pack contains a configuration file: config.json:

```

{
"AccessKeyID" : "",
"AccessKeySecret" : "",
"RoleArn" : "",
"TokenExpireTime" : "900",
"PolicyFile": "policy/all_policy.txt"
}
```

**Note:** 

-   **AccessKeyID**: Set the parameter value marked 1 in the above diagram.

-   **AccessKeySecret**: Set the parameter value marked 2 in the above diagram.

-   **RoleArn**: Set the parameter value marked 3 in the above diagram.

-   **TokenExpireTime**: Indicates the expiration time of the token obtained by the Android/iOS app. Note: The minimum value is 900s. The default value can be retained.

-   **PolicyFile**: Fill in the list of rights to the Token file, the default value can not be modified.


This document has provided three token files defining the most common permissions in the policy directory. They are:

-   all\_policy.txt: Specifies that the token has the authority to create or delete a bucket, to upload or download a file, and to delete a file under this account.

-   bucket\_read\_policy.txt: Specifies that the token has read access to the specified bucket under this account.

-   bucket\_read\_write\_policy.txt: Specifies a token that grants read and write permissions for the specified bucket for this account.


If you want to create a token to grant read and write permissions for the specified bucket, replace $BUCKET\_NAME in the bucket\_read\_policy.txt and bucket\_read\_write\_policy.txt files with the name of the desired bucket.

-   Return format resolution:

    ```
    
    {
    "status":200,
    "AccessKeyId":"STS. 3pYjsdgdgagdasdg",
    "AccessKeySecret":"rpnwO9kvEgetGdrddgsR2YrTtI",
    "Security":"CAES+wMIARKAAZhjH0EUOIhJMQBMjRywXq7MQ/cjLYg80Aho1ek0Jm63XMhr9Oc5s3qaPer8p1YaX1NTDiCFZWFkvlHf1pQhuxfKBc+mRR9KAbHUefqH+rdjZqjTF7p2m1wJXP8S6k+G2MpHrUe6TYBkJ43GhhTVFMuM3BZajY3VjZWOXBIODRIR1FKZjIiEjMzMzE0MjY0NzM5MTE4NjkxMSoLY2xpZGSSDgSDGAGESGTETqOio6c2RrLWRlbW8vKgoUYWNzOm9zczoqOio6c2RrLWRlbW9KEDExNDg5MzAxMDcyNDY4MThSBTI2ODQyWg9Bc3N1bWVkUm9sZVVzZXJgAGoSMzMzMTQyNjQ3MzkxMTg2OTExcglzZGstZGVtbzI=",
    "Expiration":"2015-12-12T07:49:09Z",
    }
    ```

    **Note:** 

    Note \(the four variables shown below comprise a token\) :

    -   **status** indicates the result that the app retrieves the token. The app returns a 200 status code for successful retrieval of the token.

    -   **AccessKeyId** indicates the AccessKeyId the Android/iOS app obtains when initializing the OSS client.

    -   **AccessKeySecret** indicates the AccessKeySecret the Android/iOS app obtains when initializing the OSS client.

    -   **SecurityToken** indicates the token the Android/iOS app initializes.

    -   **Expiration** indicates the time when the token expires. The Android SDK will automatically determine the validity of the token and retrieve a new one as needed.

-   Examples of how to run code:
    -   For JAVA \(based on Java 1.7\), after downloading and unzipping a pack,

        run this command: java -jar oss-token-server.jar \(port\). If you run java –jar oss-token-server.jar without specifying a port, the program listens to Port 7080. To change the listening port to 9000, run java –jar app-token-server.jar 9000. Specify the port number as needed.

    -   For PHP, after you download and decompress the package, modify the config.json file and run php sts.php directly to generate a token. Then set up the app server at the specified address.


## Use the MPS client SDK {#section_kf1_kcl_x2b .section}

-   Client Sample Code

    This document provides three development example programs available for download in three languages.

    -   H5: [Download](http://outline.oss-cn-hangzhou.aliyuncs.com/doc/uploadsdk/MTSUploadDemo-js-1.0.7.zip?spm=a2c4g.11186623.2.13.5e9e2059meVW7L&file=MTSUploadDemo-js-1.0.7.zip)

    -   Android: [Download](http://outline.oss-cn-hangzhou.aliyuncs.com/doc/uploadsdk/MTSUploadDemo-android-1.0.7.zip?spm=a2c4g.11186623.2.14.5e9e2059meVW7L&file=MTSUploadDemo-android-1.0.7.zip)

    -   iOS: [Download](http://outline.oss-cn-hangzhou.aliyuncs.com/doc/uploadsdk/MTSUploadDemo-ios-1.0.7.zip?spm=a2c4g.11186623.2.15.5e9e2059meVW7L&file=MTSUploadDemo-ios-1.0.7.zip)

-   SDK core code

    JS side

    Before using the JS SDK, first open [CORS Access](../../../../reseller.en-US/Developer Guide/Upload videos/Set CORS.md#) to the OSS Bucket where you want to upload the video. Download JS Demo, open in a browser, the parameters on the page configuration are:

    -   Configure the “HTTP Address” as the application server address configured above, for example, [http://127.0.0.1:7080/](http://127.0.0.1:7080/%E3%80%82?spm=a2c4g.11186623.2.17.5e9e2059meVW7L).
    -   Configure user Bucket.
    -   Configure Bucket endpoint.
    -   Click to select the file, select the file to be uploaded.
    -   Click the Start Upload button.
    ```
    
    // Initialize the client
    var uploader = new VODUpload({
    // Start upload
    'onUploadstarted': function (uploadInfo) {;},
    //File uploaded successfully
    'onUploadSucceed': function (uploadInfo) {console.log("Uploaded successfully");},
    //File upload failed
    'onUploadFailed': function (uploadInfo, code, message) {console.log("File upload failed");},
    // File upload progress, in bytes
    'onUploadProgress': function (uploadInfo, totalSize, uploadedSize) {console.log("File upload progress,");},
    //Security token timed out
    'onUploadTokenExpired': function (uploadInfo) {console.log("Token timeout");}
    });
    // Get STS Information
    result = httpGet(httpServer);
    stsToken = JSON.parse(result);
    uploader.init(stsToken.AccessKeyId, stsToken.AccessKeySecret, stsToken.SecurityToken, stsToken.Expiration);
    // Add File
    uploader.addFile(event.target.files[i], endpoint, bucket, object, userData);
    // Start uploading
    uploader.startUpload();
    ```

    Android end

    Make sure Android has added the following permissions:

    ```
    <uses-permission android:name="android.permission.INTERNET"></uses-permission>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"></uses-permission>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
    ```

    Download Android Demo, make the following changes:

    -   Modify MainActivity inside serverUrl for the application server configuration address, such as [http://192.168.0.2:7080/](http://192.168.0.2:7080/%E3%80%82?spm=a2c4g.11186623.2.18.5e9e2059meVW7L).
    -   Configure user Bucket.
    -   Configure the endpoint corresponding to the user Bucket.
    -   Run Demo, click Add File.
    -   Click Upload to check whether the file has been uploaded successfully under the uploadtest / directory of the OSS Bucket.
    Main code:

    ```
    
    VODUploadClient uploader = new VODUploadClientImpl(getApplicationContext());
    VODUploadCallback callback = new VODUploadCallback() {
    @Override
    public void onUploadSucceed(UploadFileInfo info) {;}
    @Override
    public void onUploadFailed(UploadFileInfo info, String code, String message) {;}
    @Override
    public void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize) {;}
    @Override
    public void onUploadTokenExpired(UploadFileInfo info) {
    // Get and update STS token.
    uploader.resumeWithToken("", "", "", "");
    }
    @Override
    public void onUploadRetry(UploadFileInfo info, String code, String message) {;}
    @Override
    public void onUploadRetryResume(UploadFileInfo info) {;}
    @Override
    public boolean onUploadStarted(UploadFileInfo uploadFileInfo) {;}
    };
    // Get STS token and initialize
    uploader.init("", "", "", "", callback);
    // Add File
    uploader.addFile("", "", "", "");
    // Start uploading
    uploader.start();
    ```

    IOS end

    Download iOS Demo, make the following changes:

    -   Modify the serverUrl in VODUploadDemo.m to configure the address for the application server, such as [http://192.168.0.2:7080/](http://192.168.0.2:7080/%E3%80%82?spm=a2c4g.11186623.2.19.5e9e2059meVW7L).
    -   Configure user Bucket.
    -   Configure the endpoint corresponding to the user Bucket.
    -   Run Demo, click Add File.
    -   Click Upload to check whether the file has been uploaded successfully under the uploadtest / directory of the OSS Bucket.
    Main code:

    ```
    
    // Callback Initialization
    OnUploadStartedListener testUploadStartedCallbackFunc = ^(UploadFileInfo* fileInfo) {;};
    OnUploadSucceedListener testSuccessCallbackFunc = ^(NSString* filePath){;};
    OnUploadFailedListener testFailedCallbackFunc = ^(NSString* filePath, NSString* code, NSString* message){;};
    OnUploadProgressListener testProgressCallbackFunc = ^(NSString* filePath, long uploadedSize, long totalSize) {;};
    OnUploadTokenExpiredListener testTokenExpiredCallbackFunc = ^{
    // Get and update STS token
    [uploader resumeWithToken:
    accessKeySecret:
    secretToken:
    expireTime:]
    };
    OnUploadRertyListener testUploadRertyListener = ^{;};
    OnUploadRertyResumeListener testUploadRertyResumeListener = ^{;};
    VODUploadListener *listener;
    listener = [[VODUploadListener alloc] init];
    listener.started = testUploadStartedCallbackFunc;
    listener.success = testSuccessCallbackFunc;
    listener.failure = testFailedCallbackFunc;
    listener.progress = testProgressCallbackFunc;
    listener.expire = testTokenExpiredCallbackFunc;
    listener.retry = testUploadRertyListener;
    listener.retryResume = testUploadRertyResumeListener;
    // Get Token
    // Upload client Initialization
    VODUploadClient *uploader;
    [uploader init:
    accessKeySecret:
    secretToken:
    expireTime:
    listener:listener];
    // Add File
    [uploader addFile:
    endpoint:
    bucket:
    object:];
    // Start uploading
    [uploader start];
    ```


