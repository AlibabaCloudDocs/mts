# HLS encryption and play {#concept_hsy_2kg_x2b .concept}

## Purpose {#section_i23_gkg_x2b .section}

This document describes the complete procedure of creating HLS standard encryption workflow to play the encrypted video.

For more information about the architecture of HLS standard encryption, see [HLS standard encryption](https://help.aliyun.com/document_detail/59885.html).

## Procedure {#section_zcj_hkg_x2b .section}

1.  Create HLS encryption workflow.

    For more information about creating HLS encryption workflow and DEMO code, see [Create HLS standard encryption workflow](https://help.aliyun.com/document_detail/59854.html).

    **Note:** When creating HLS standard workfow, enter http: //127.0.0.1:8888 in the value of the HLS\_KEY\_URI parameter for a test. During playing, the player request the key to this address, and we create a service to distribute key.

2.  Upload and encrypt video.

    Upload a video by using Media Files in the MPS console. When selecting workflow, select the newly created HLS standard encryption workflow. After uploading, the workflow automatically triggers encryption transcoding. When the video is in the published status, follow these steps.

3.  Create local authentication service.

    Create a local HTTP service, which serves as authentication service in playing HLS standard encryption video, to issue and verify MtsHlsUriToken token.

    Java code dependency example:

    [https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-core](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-core)

    [https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-kms](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-kms)

    ```
    
    package com.aliyun.smallcode;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http.ProtocolType;
    import com.aliyuncs.kms.model.v20160120. DecryptRequest;
    import com.aliyuncs.kms.model.v20160120. DecryptResponse;
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
    String accessKeyId = "<your-access-key-id>"
    String accessKeySecret = "<your-access-key-secret>";
    client = new DefaultAcsClient(DefaultProfile.getProfile(region, accessKeyId, accessKeySecret));
    }
    public class AuthorizationHandler implements HttpHandler {
    public void handle(HttpExchange httpExchange) throws IOException {
    String requestMethod = httpExchange.getRequestMethod();
    if(requestMethod.equalsIgnoreCase("GET")){
    //Get ciphertext and key from URL
    String ciphertext = getCiphertext(httpExchange);
    if (null == ciphertext)
    return;
    //decrypt ciphertext from KMS, and Base64 decode
    byte[] key = decrypt(ciphertext);
    //Set header
    setHeader(httpExchange, key);
    //Response key
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
    //Note: require base64 decode
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
    //listening port 8888 can accept 10 request simultaneously
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

    Python sample code:

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

4.  Obtain playback addresses.

    You can obtain playback address by multiple ways. For more information, see [Questions about MPS file output](https://help.aliyun.com/document_detail/50628.html).

5.  Play video.

    By using an online player, test the playback of HLS encryption video. For more information, see [Alibaba Cloud player user diagnositc tool](http://player.alicdn.com/detection.html).

    Enter the playback address obtained from step **4** to the dialogue box as shown in the following figure, and click **Play**.

    **Note:** By using browser DEBUG, the player automatically request authentication server, obtain decryption key and do the playback operation after decryption.

    ![](images/10097_en-US.png)


