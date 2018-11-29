# JavaScript版本 {#concept_rk5_pv5_y2b .concept}

## 安装 {#section_fws_sv5_y2b .section}

[上传SDK下载](intl.zh-CN/SDK参考/上传SDK/上传SDK下载.md#)

在页面上引入下面两个JS脚本

```
<script src="aliyun-sdk.min.js"></script>
<script src="vod-sdk-upload-1.0.6.min.js"></script>
```

## 创建VODUpload实例 {#section_nfr_vv5_y2b .section}

在这里需要设置回调函数

```
var uploader = new VODUpload({
    // 开始上传
    'onUploadstarted': function (uploadInfo) {
      log("onUploadStarted:" + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
    }
    // 文件上传成功
    'onUploadSucceed': function (uploadInfo) {
      log("onUploadSucceed: " + uploadInfo.file.name + ", endpoint:" + uploadInfo.endpoint + ", bucket:" + uploadInfo.bucket + ", object:" + uploadInfo.object);
    },
    // 文件上传失败
    'onUploadFailed': function (uploadInfo, code, message) {
      log("onUploadFailed: file:" + uploadInfo.file.name + ",code:" + code + ", message:" + message);
    },
    // 文件上传进度，单位：字节
    'onUploadProgress': function (uploadInfo, totalSize, uploadedSize) {
        log("onUploadProgress:file:" + uploadInfo.file.name + ", fileSize:" + totalSize + ", percent:" + Math.ceil(uploadedSize * 100 / totalSize) + "%");
    },
    // 安全令牌超时
    'onUploadTokenExpired': function () {
        console.log("onUploadTokenExpired");
        // uploader.resumeUploadWithToken(accessKeyId, accessKeySecret, secretToken, expireTime);
    }
});
```

## 列表管理 {#section_os1_yv5_y2b .section}

-   添加上传文件

    **说明：** 支持的文件大小≤10G。

    需要使用标准的input方式让用户选择文件。

    ```
    <form action="">
    <input type="file" name="file" id="files" multiple/>
    </form>
    userData = '';
    document.getElementById("files")
         .addEventListener('change', function (event) {
           for(var i=0; i<event.target.files.length; i++) {
             // 逻辑代码
           }
         });
    ```

    获取到用户选择的文件后，添加到上传列表中。

    ```
    uploader.addFile(event.target.files[i], endpoint, bucket, object, userData);
    ```

    上传时，如何指定媒体的属性（标题、标签、描述、类目、用户自定义数据）呢？addFile函数最后的参数userData是一个json对象。第一级的Vod是必须的，Vod下面有5个属性，示例如下：

    ```
    var userData = '{"Vod":{"Title":"我是标题",
                       "Description":"我是描述",
                       "CateId":"1",
                       "Tags":"tag1,tag2,标签3",
                       "UserData":"user data"}}';
    ```

-   删除上传文件，`index`对应listFiles接口返回列表中元素的索引。

    ```
    uploader.deleteFile(index);
    ```

-   取消单个文件上传。

    ```
    uploader.cancelFile(index);
    ```

-   恢复单个文件上传。

    ```
    uploader.resumeFile(index);
    ```

-   获取上传文件列表。

    ```
    uploader.listFiles();
     var list = uploader.listFiles();
        for (var i=0; i<list.length; i++) {
            log("file:" + list[i].file.name + ", status:" + list[i].state + ", endpoint:" + list[i].endpoint + ", bucket:" + list[i].bucket + ", object:" + list[i].object);
        }
    ```

-   清理上传文件列表。

    ```
    uploader.cleanList();
    ```


## 上传控制 {#section_nmd_4w5_y2b .section}

-   开始上传

    ```
    uploader.startUpload();
    ```

-   停止上传

    ```
    uploader.stopUpload();
    ```

-   上传凭证失效后恢复上传

    ```
    uploader.resumeUploadWithToken(accessKeyId, accessKeySecret, secretToken, expireTime);
    ```


