# 如何进行HLS的加密与播放 {#concept_hsy_2kg_x2b .concept}

## 本文目的 {#section_i23_gkg_x2b .section}

示例创建HLS标准加密工作流到播放加密视频的一个完整步骤。

HLS标准加密架构，参见 [HLS的加密与播放](../../../../cn.zh-CN/开发指南/视频加密/HLS标准加密.md#)。

## 操作步骤 {#section_zcj_hkg_x2b .section}

1.  创建HLS加密工作流。

    创建HLS加密工作流，DEMO代码，参见 [创建HLS标准加密工作流](../../../../cn.zh-CN/SDK参考/媒体转码SDK/Python SDK/创建HLS标准加密工作流.md#)。

    **说明：** 创建HLS标准工作流时，为了测试，参数 HLS\_KEY\_URI 值填 http: //127.0.0.1:8888。播放时，播放器会到这个地址请求密钥，我们会在本地起一个服务，进行分发密钥。

2.  上传及加密视频。

    在控制台的媒体库中，上传视频，选择工作流时，选择刚刚创建的HLS标准加密工作流，上传完成后，会自动触发加密转码。待状态为发布时，进行下一步。

3.  开启本地鉴权服务。

    搭建一个本地HTTP服务，作为播放HLS标准加密视频的鉴权服务，颁发及验证MtsHlsUriToken令牌。

    Java示例代码依赖：

    [https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-core](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-core)

    [https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-kms](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-kms)

    ```
    
    package com.aliyun.smallcode;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http.ProtocolType;
    import com.aliyuncs.kms.model.v20160120.DecryptRequest;
    import com.aliyuncs.kms.model.v20160120.DecryptResponse;
    import com.aliyuncs.profile.DefaultProfile;
    import com.sun.net.httpserver.Headers;
    import com.sun.net.httpserver.HttpExchange;
    import com.sun.net.httpserver.HttpHandler;
    import com.sun.net.httpserver.HttpServer;
    import com.sun.net.httpserver.spi.HttpServerProvider;
    import org.apache.commons.codec.binary.Base64;
    import java.io.IOException;
    import java.io.OutputStream;
    import java.net.HttpURLConnection;
    import java.net.InetSocketAddress;
    import java.net.URI;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;
    public class AuthorizationServer {
    private static DefaultAcsClient client;
    static {
    String region = "";
    String accessKeyId = "";
    String accessKeySecret = "";
    client = new DefaultAcsClient(DefaultProfile.getProfile(region, accessKeyId, accessKeySecret));
    }
    public class AuthorizationHandler implements HttpHandler {
    public void handle(HttpExchange httpExchange) throws IOException {
    String requestMethod = httpExchange.getRequestMethod();
    if(requestMethod.equalsIgnoreCase("GET")){
    //从URL中取得密文密钥
    String ciphertext = getCiphertext(httpExchange);
    if (null == ciphertext)
    return;
    //从KMS中解密出来，并Base64 decode
    byte[] key = decrypt(ciphertext);
    //设置header
    setHeader(httpExchange, key);
    //返回密钥
    OutputStream responseBody = httpExchange.getResponseBody();
    responseBody.write(key);
    responseBody.close();
    }
    }
    private void setHeader(HttpExchange httpExchange, byte[] key) throws IOException {
    Headers responseHeaders = httpExchange.getResponseHeaders();
    responseHeaders.set("Access-Control-Allow-Origin", "*");
    httpExchange.sendResponseHeaders(HttpURLConnection.HTTP_OK, key.length);
    }
    private byte[] decrypt(String ciphertext) {
    DecryptRequest request = new DecryptRequest();
    request.setCiphertextBlob(ciphertext);
    request.setProtocol(ProtocolType.HTTPS);
    try {
    DecryptResponse response = client.getAcsResponse(request);
    String plaintext = response.getPlaintext();
    //注意：需要base64 decode
    return Base64.decodeBase64(plaintext);
    } catch (ClientException e) {
    e.printStackTrace();
    return null;
    }
    }
    private String getCiphertext(HttpExchange httpExchange) {
    URI uri = httpExchange.getRequestURI();
    String queryString = uri.getQuery();
    String pattern = "Ciphertext=(\\w*)";
    Pattern r = Pattern.compile(pattern);
    Matcher m = r.matcher(queryString);
    if (m.find())
    return m.group(1);
    else {
    System.out.println("Not Found Ciphertext");
    return null;
    }
    }
    }
    private void startService() throws IOException {
    HttpServerProvider provider = HttpServerProvider.provider();
    //监听端口8888,能同时接受10个请求
    HttpServer httpserver = provider.createHttpServer(new InetSocketAddress(8888), 10);
    httpserver.createContext("/", new AuthorizationHandler());
    httpserver.start();
    System.out.println("server started");
    }
    public static void main(String[] args) throws IOException {
    AuthorizationServer server = new AuthorizationServer();
    server.startService();
    }
    }
    ```

    Python示例代码依赖：

    pip install aliyun-python-sdk-core

    pip install aliyun-python-sdk-kms

    pip install aliyun-python-sdk-mts

    ```
    
    # -*- coding: UTF-8 -*- 
    from BaseHTTPServer import BaseHTTPRequestHandler
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkkms.request.v20160120 import DecryptRequest
    import cgi
    import json
    import base64
    import urlparse
    client = AcsClient("","","");
    class AuthorizationHandler(BaseHTTPRequestHandler):
    def do_GET(self):
    self.check()
    self.set_header()
    cipertext = self.get_cihpertext()
    plaintext = self.decrypt_cihpertext(cipertext)
    print plaintext
    key = base64.b64decode(plaintext)
    print key
    self.wfile.write(key)
    def do_POST(self):
    pass
    def check(self):
    #check MtsHlsUriToken, etc.
    pass
    def set_header(self):
    self.send_response(200)
    #cors
    self.send_header('Access-Control-Allow-Origin', '*')
    self.end_headers()
    def get_cihpertext(self):
    path = urlparse.urlparse(self.path)
    query = urlparse.parse_qs(path.query)
    return query.get('Ciphertext')[0]
    def decrypt_cihpertext(self, cipertext):
    request = DecryptRequest.DecryptRequest()
    request.set_CiphertextBlob(cipertext)
    response = client.do_action_with_exception(request)
    jsonResp = json.loads(response)
    return jsonResp["Plaintext"]
    if __name__ == '__main__':
    # Start a simple server, and loop forever
    from BaseHTTPServer import HTTPServer
    print "Starting server, use  to stop"
    server = HTTPServer(('127.0.0.1', 8888), AuthorizationHandler)
    server.serve_forever()
    ```

4.  获取播放地址。

    多种方式可获取。详情参见 [媒体转码输出文件相关问题](https://help.aliyun.com/document_detail/50628.html)。

5.  播放视频。

    借助一个在线播放器，测试HLS加密视频的播放。详情参见 [阿里云播放器用户诊断工具](http://player.alicdn.com/detection.html)。

    将第 **4**步中获取的播放地址，如图填入对话框中，单击 **视频播放** 即可。

    **说明：** 通过浏览器DEBUG，可以看到播放器自动请求了鉴权服务器，获取解密密钥，并进行解密播放。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11375/154106407710097_zh-CN.png)


