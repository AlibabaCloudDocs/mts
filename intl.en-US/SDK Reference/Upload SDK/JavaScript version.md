# JavaScript version {#concept_rk5_pv5_y2b .concept}

## Installation {#section_fws_sv5_y2b .section}

[Download the upload SDK](https://help.aliyun.com/document_detail/48501.html)

Introduce the following two JavaScript scripts on the page:

```
<script src="aliyun-sdk.min.js"></script>
<script src="vod-sdk-upload-1.0.6.min.js"></script>
```

## Create a VODUpload instance. {#section_nfr_vv5_y2b .section}

Set the callback function.

```
var uploader = new VODUpload({
    // Starts upload
    'onUploadstarted': function (uploadInfo) {
      log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
    }
    //File upload succeeds
    'onUploadSucceed': function (uploadInfo) {
      log("onUploadSucceed: " + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
    },
    //File upload fails
    'onUploadFailed': function (uploadInfo, code, message) {
      log("onUploadFailed: file:" + uploadInfo.file.name + ",code:" + code + ", message:" + message);
    },
    // The file upload progress, in bytes
    'onUploadProgress': function (uploadInfo, totalSize, uploadedSize) {
        log("onUploadProgress:file:" + uploadInfo.file.name + ", fileSize:" + totalSize + ", percent:" + Math.ceil(uploadedSize * 100 / totalSize) + "%");
    },
    // Token expires
    'onUploadTokenExpired': function () {
        console.log("onUploadTokenExpired");
        // uploader.resumeUploadWithToken(accessKeyId, accessKeySecret, secretToken, expireTime);
    }
});
```

## List management {#section_os1_yv5_y2b .section}

-   Add a file to be uploaded

    **Note:** The file size cannot exceed 10 GB.

    Use the standard input mode for selecting a file.

    ```
    <form action="">
    <input type="file" name="file" id="files" multiple/>
    </form>
    userData = '';
    document.getElementById("files")
         .addEventListener('change', function (event) {
           for(var i=0; i<event.target.files.length; i++) {
             // The logic code
           }
         });
    ```

    Obtain the selected file and add it to the upload list.

    ```
    uploader.addFile(event.target.files[i], endpoint, bucket, object, userData);
    ```

    During uploading, obtain the attributes \(the title, tag, description, category, and custom data\) of a media set in the following way: The last parameter userData of the addFile function is a JSON object. The first-level VOD is required, and VOD contains the five attributes. Example:

    ```
    var userData = '{"Vod":{"Title":"I am the title",
                       "Description":"I am the description",
                       "Cateoid": "1 ",
                       "Tags":"tag1,tag2,tag3",
                       "UserData":"user data"}}';
    ```

-   Delete the uploaded file. `index` corresponds to the index of the elements in the list returned by listFiles.

    ```
    uploader.deleteFile(index);
    ```

-   Cancel upload of a single file.

    ```
    uploader.cancelFile(index);
    ```

-   Resume upload of a single file.

    ```
    uploader.resumeFile(index);
    ```

-   Obtain the upload file list.

    ```
    uploader.listFiles();
     var list = uploader.listFiles();
        for (var i=0; i<list.length; i++) {
            log("file:" + list[i].file.name + ", status:" + list[i].state + ", endpoint:" + list[i].endpoint + ", bucket:" + list[i].bucket + ", object:" + list[i].object);
        }
    ```

-   Clear the upload file list.

    ```
    uploader.cleanList();
    ```


## Upload control {#section_nmd_4w5_y2b .section}

-   Start upload.

    ```
    uploader.startUpload();
    ```

-   Stop upload

    ```
    uploader.stopUpload();
    ```

-   Resume upload after the upload credential becomes invalid.

    ```
    uploader.resumeUploadWithToken(accessKeyId, accessKeySecret, secretToken, expireTime);
    ```


