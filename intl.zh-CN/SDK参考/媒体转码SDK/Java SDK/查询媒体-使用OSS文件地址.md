# 查询媒体-使用OSS文件地址 {#concept_r3f_jhx_y2b .concept}

如果您在不知道媒体ID（直播走工作流转点播），可以通过媒体的输入地址进行媒体信息的查询，接口为 QueryMediaListByURL。

```
package com.aliyun.mts.api.demo
import com.alibaba.fastjson.JSONObject;
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.mts.model.v20140618.QueryMediaListByURLRequest;
import com.aliyuncs.mts.model.v20140618.QueryMediaListByURLResponse;
import com.aliyuncs.profile.DefaultProfile;
import java.io.UnsupportedEncodingException;
import java.net.URLEncoder;
public class QueryMediaListByURLDemo {
    private DefaultAcsClient client = null;
    private final String REGION = "<region>";
    private final String ID="<accessKeyId>";
    private final String KEY ="<accessKeySecret>";
    public QueryMediaListByURLDemo() throws ClientException {
        this.client = new DefaultAcsClient(DefaultProfile.getProfile(REGION, ID, KEY));
    }
    //根据视频源OSS地址查询媒体信息， 如: 媒体ID, 媒体状态及其他属性
    private void queryMediaListByURL() throws ClientException, UnsupportedEncodingException {
        QueryMediaListByURLRequest request = new QueryMediaListByURLRequest();
        String ossHost = 'http://<input-bucket>.<region>.aliyuncs.com/';
        String ossObject = "test/笑傲江湖.mp4";
        //ossObject需要符合rfc3986标准
        String rfc3986Object = encodeByRFC3986(ossObject);
        request.setFileURLs(ossHost + rfc3986Object);
        QueryMediaListByURLResponse response = this.client.getAcsResponse(request);
        System.out.println(JSONObject.toJSONString(response.getMediaList()));
    }
    private String encodeByRFC3986(String object) throws UnsupportedEncodingException {
        StringBuilder builder = new StringBuilder();
        String[] segments = object.split("/");
        for (int i = 0; i < segments.length; i++) {
            builder.append(percentEncode(segments[i]));
            if (i != segments.length - 1) {
                builder.append("/");
            }
        }
        return builder.toString();
    }
    private static String percentEncode(String value) throws UnsupportedEncodingException {
        if (value == null)
            return null;
        return URLEncoder.encode(value, "UTF-8").replace("+", "%20").replace("*", "%2A").replace("%7E", "~");
    }
    public static void main(String[] args) {
        try {
            QueryMediaListByURLDemo demo = new QueryMediaListByURLDemo();
            demo.queryMediaListByURL();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

