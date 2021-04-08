# Php SDK

本文介绍了使用Php SDK实现智能标签的示例代码。

## 提交智能标签作业

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('SubmitSmarttagJob')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'Title' => "<yourTitle>",
                                          'Content' => "<yourContent>",
                                          'PipelineId' => "",
                                          'Input' => "oss://xxx.mp4",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 查询智能标签作业

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('QuerySmarttagJob')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'JobId' => "<JobId>",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 添加模板

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('AddSmarttagTemplate')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'Industry' => "media",
                                          'Scene' => "search",
                                          'AnalyseTypes' => "ocr,asr,classification,shows,face,role,object,tvstation,action,emotion,landmark,scene",
                                          'TemplateName' => "test",
                                          'FaceCategoryIds' => "politician,sensitive,celebrity",
                                          'IsDefault' => "false",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 查询模板

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('QuerySmarttagTemplateList')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'TemplateId' => "6407",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 更新模板

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('UpdateSmarttagTemplate')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'TemplateName' => "update测试",
                                          'TemplateId' => "6407",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 删除模板

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('DeleteSmarttagTemplate')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'TemplateId' => "6407",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 注册自定义人脸

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('RegisterCustomFace')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'PersonId' => "<yourPersonId>",
                                          'ImageUrl' => "http://xxxxx.jpeg",
                                          'CategoryId' => "<yourCategoryId>",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 注销自定义人脸

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('UnregisterCustomFace')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'PersonId' => "<yourPersonId>",
                                          'FaceId' => "<FaceId>",
                                          'CategoryId' => "<yourCategoryId>",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 添加自定义人物库或人物标签

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('TagCustomPerson')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'CategoryId' => "<yourCategoryId>",
                                          'CategoryName' => "<yourCategoryaName>",
                                          'CategoryDescription' => "<yourCategoryDescription>",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

## 列出⼈物库所有⼈物和⼈脸信息

```
<?php
use AlibabaCloud\Client\AlibabaCloud;
use AlibabaCloud\Client\Exception\ClientException;
use AlibabaCloud\Client\Exception\ServerException;

// Download：https://github.com/aliyun/openapi-sdk-php
// Usage：https://github.com/aliyun/openapi-sdk-php/blob/master/README.md

AlibabaCloud::accessKeyClient('<accessKeyId>', '<accessSecret>')
                        ->regionId('cn-beijing')
                        ->asDefaultClient();

try {
    $result = AlibabaCloud::rpc()
                          ->product('Mts')
                          // ->scheme('https') // https | http
                          ->version('2014-06-18')
                          ->action('ListCustomPersons')
                          ->method('POST')
                          ->host('mts.cn-beijing.aliyuncs.com')
                          ->options([
                                        'query' => [
                                          'RegionId' => "cn-beijing",
                                          'CategoryId' => "<yourCategoryId>",
                                          'PersonId' => "<yourPersonId>",
                                        ],
                                    ])
                          ->request();
    print_r($result->toArray());
} catch (ClientException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
} catch (ServerException $e) {
    echo $e->getErrorMessage() . PHP_EOL;
}
```

