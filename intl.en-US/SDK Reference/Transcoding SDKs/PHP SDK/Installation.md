# Installation {#concept_k5b_322_z2b .concept}

This article introduces the installation method of Alibaba Cloud PHP SDK.

1.  Download the source code.

    ```
    git clone https://github.com/aliyun/aliyun-openapi-php-sdk.git
    ```

2.  Add the reference.

    Assume the PHP SDK is downloaded to the path `/path/to/aliyun-openapi-php-sdk`.

    ```
    require_once '/path/to/aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php';
    ```

    Assume `aliyun-openapi-php-sdk` is referred to under the current directory of the project.

    ```
    require_once 'aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php';
    ```

3.  Automatically load MPS SDK.

    Edit the file `aliyun-openapi-php-sdk/aliyun-php-sdk-core/Config.php`.

    Find the content `//config sdk auto load path.`, and add `Autoloader::addAutoloadPath("aliyun-php-sdk-mts");` at the end.


