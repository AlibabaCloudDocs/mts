# Set CORS {#concept_wvr_qy4_1fb .concept}

As JavaScript files and video files are stored in different regions, a cross-region request is initiated when a JavaScript file is uploaded. In this case, cross-region settings must be implemented on OSS. Otherwise, files cannot be uploaded using JavaScript at the web end.

1.  Open the CORS settings page of the input bucket.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11387/153993568611340_en-US.png)

2.  Add a rule.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11387/153993568611341_en-US.png)

    -   **Source**

        Enter the name of the region in which JavaScript files are deployed. If access through both HTTP and HTTPS is required, add them respectively.

    -   **Method**

        Select **GET**, **POST**, **PUT**, **HEAD**.

    -   **Allowed Header**

        Enter `*`.

    -   **Expose Header**

        Enter **etag** and **x-oss-request-id** in two lines.


