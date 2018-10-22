# Query media - Use OSS file address {#concept_g1r_dp2_z2b .concept}

If you do not know the media ID \(a live video converted to an on-demand video using the media workflow\), you can use the media input URL to query the media information over QueryMediaListByURL.

```
<? php
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
        #ossObject must be RFC3986-encoded.
        $ossObject = $this->encodeByRFC3986('test/The Legend of the Swordsman.mp4');
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
            if ($i ! == count($arraylist) -1) {
                $encodeOssObject = $encodeOssObject."/";
            }
        }
        return $encodeOssObject;
    }
}
$demo = new QueryMediaListByURLDemo();
$demo->queryMediaListByUrl();
? >
```

