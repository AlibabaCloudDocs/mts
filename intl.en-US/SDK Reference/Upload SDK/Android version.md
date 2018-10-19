# Android version {#concept_vpn_yw5_y2b .concept}

## Environment requirements {#section_mks_1x5_y2b .section}

Android 2.3 or a later version

## Installation {#section_x5s_bx5_y2b .section}

[OSS Android SDK](https://github.com/aliyun/aliyun-oss-android-sdk/)

[Upload SDK](https://help.aliyun.com/document_detail/48501.html)

-   Directly introduce the JAR package

    After you download the ZIP package of the VODUpload Android SDK, perform the following steps \(applicable to Android Studio or Eclipse\):

    -   Decompress the SDK to obtain the following JAR packages in the libs directory: aliyun-oss-sdk-android-xxx.jar, okhttp-2.7.0.jar, okio-2.6.0.jar, and aliyun-vod-upload-android-sdk-xxx.jar.
    -   Import the four JAR packages to the libs directory of the project.
    -   Set permissions

        The following are the Android permissions required by the VODUpload Android SDK. Make sure that these permissions are already set in your AndroidManifest.xml file. Otherwise, the SDK cannot work normally.

        ```
        <uses-permission android:name="android.permission.INTERNET"></uses-permission>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses-permission>
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"></uses-permission>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"></uses-permission>
        ```


## Create a VODUpload instance {#section_iyt_3x5_y2b .section}

Set the callback function.

```
VODUploadCallback callback = new VODUploadCallback() {
    /**
    * Triggered when the file upload starts
    */
    void onUploadStarted() {;}
    /**
    *  Callback after successful upload
    */
    void onUploadSucceed(UploadFileInfo info) {;}
    /**
    *  Upload failed
    */
    void onUploadFailed(UploadFileInfo info, String code, String message) {;}
    /**
    * Callback upload progress
    * @param uploadedSize The number of uploaded bytes
    * @param totalSize The total number of required bytes
    */
    void onUploadProgress(UploadFileInfo info, long uploadedSize, long totalSize) {;}
    /**
    * This API is called back after the upload credential expires
    * Obtain a new upload credential in the callback and call resumeUploadWithAuth to continue upload
    */
    void onUploadTokenExpired() {;}
    /**
    * Triggered when the status switches from normal to abnormal during upload
    */
    void onUploadRetry(String code, String message) {;}
    /**
    * Triggered when the status is resumed from abnormal during upload
    */
    void onUploadRetryResume() {;}
};
VODUploadClient uploader = new VODUploadClientImpl(getContext());
```

## Initialization {#section_hvr_lx5_y2b .section}

Enter the authorization information in either of the following ways:

-   AccessKey

    It is simple but not safe. It is recommended that this way be used in the test environment.

    ```
    uploader.init("<accessKeyId>", "<accessKeySecret>", callback);
    ```

-   Token

    It is safe but complex. It is recommended that this way be used in the production environment. A token is temporary and valid for a period. Therefore, sending a token is safe.

    ```
    uploader.init("<accessKeyId>", "<accessKeySecret>", "<secretToken>", "<expireTime>", callback);
    ```


## List management {#section_jtm_rx5_y2b .section}

-   Add a file to be uploaded.

    **Note:** The file size cannot exceed 4 GB.

    ```
    uploader.addFile("<uploadFilePath>",
                   "<endpoint>", // For example, the Hangzhou regio "http://oss-cn-hangzhou.aliyuncs.com"
                   "<bucketName>", // Enter the actual bucket name
                   "<objectKey>");
    ```

    During uploading, obtain the attributes \(the title, tag, description, category, cover URL, and custom data\) of a media set in the following way: addFile contains a reload function, in which the last parameter is a VodInfo object. The definitions are as follows:

    ```
    private String title;
    private String desc;
    private Integer cateId;
    private List<String> tags;
    private String userData;
    private String coverUrl;
    ```

-   Delete the uploaded file. `index` corresponds to the index of the elements in the list returned by listFiles.

    ```
    uploader.deleteFile(index);
    ```

-   Cancel upload of a single file in the list.

    ```
    uploader.cancelFile(index);
    ```

-   Resume upload of a single file in the list.

    ```
    uploader.resumeFile(index);
    ```

-   Obtain the upload file list.

    ```
    List list = uploader.listFiles();
    ```

-   Clear the upload file list.

    ```
    upload.clearFiles();
    ```


## Upload control {#section_r1c_dy5_y2b .section}

-   Start upload.

    ```
    uploader.start();
    ```

-   Stop upload.

    ```
    uploader.stop();
    ```

-   Pause upload.

    ```
    uploader.pause();
    ```

-   Resume upload.

    ```
    uploader.resume();
    ```

-   Resume upload after the token is invalid.

    ```
    uploader.resumeWithToken("<accessKeyId>", "<accessKeySecret>", "<secretToken>", "<expireTime>");
    ```


