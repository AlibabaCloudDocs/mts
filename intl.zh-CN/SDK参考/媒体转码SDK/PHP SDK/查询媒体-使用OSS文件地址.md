# 查询媒体-使用OSS文件地址 {#concept_g1r_dp2_z2b .concept}

如果您不知道媒体ID（直播走工作流转点播），可以通过媒体的输入地址进行媒体信息的查询，接口为 QueryMediaListByURL。

```
<?php
include_once 'aliyun-php-sdk-core/Config.php';
use Mts\Request\V20140618 as Mts;
date_default_timezone_set('PRC');
class QueryMediaListByURLDemo {
    private $client;
    private $region = '<region>';
    private $accessKeyId = '<accessKeyId>';
    private $accessKeySecret = '<accessKeySecret>';
    function __construct() 
    {
        $profile = DefaultProfile::getProfile($this->region, $this->accessKeyId, $this->accessKeySecret);
        $this->client = new DefaultAcsClient($profile);
    }
    function queryMediaListByUrl()
    {
        $request = new Mts\QueryMediaListByURLRequest();
        $ossDomain = 'http://<input-bucket>.<region>.aliyuncs.com/';
        #ossObject需要RFC3986编码
        $ossObject = $this->encodeByRFC3986('test/笑傲江湖.mp4');
        $request->setFileURLs($ossDomain.$ossObject);
        $response = $this->client->getAcsResponse($request);
        echo json_encode($response);
    }
    function encodeByRFC3986($arg_1)
    {
        $encodeOssObject="";
        $arraylist = explode("/", $arg_1);
        for($i = 0; $i < count($arraylist); $i++)
        {
            $tmp = rawurlencode($arraylist[$i]);
            $encodeOssObject = $encodeOssObject.$tmp;
            if ($i !== count($arraylist) -1) {
                $encodeOssObject = $encodeOssObject."/";
            }
        }
        return $encodeOssObject;
    }
}
$demo = new QueryMediaListByURLDemo();
$demo->queryMediaListByUrl();
?>
```

