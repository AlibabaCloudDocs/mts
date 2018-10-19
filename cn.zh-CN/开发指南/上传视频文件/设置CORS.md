# 设置CORS {#concept_wvr_qy4_1fb .concept}

由于js文件和视频文件放在不同的域名下，JavaScript上传文件时会发起跨域请求。需要设置OSS的跨域设置，否则无法通过Web端的JavaScript正常上传文件。

1.  打开输入bucket对应的CORS设置页面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11387/153993568111340_zh-CN.png)

2.  添加规则。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11387/153993568111341_zh-CN.png)

    -   **来源**

        填写实际部署js文件的域名，如果需要同时支持http和https访问，需要分别添加。

    -   **Method**

        勾选 **GET**、**POST**、**PUT**、**HEAD**。

    -   **Allowed Header**

        填写`*`。

    -   **Expose Header**

        分两行填写 **etag**和 **x-oss-request-id**。


