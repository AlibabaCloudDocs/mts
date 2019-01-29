# Call an API {#reference_ozp_l1n_x2b .reference}

The Media Processing APIs are called by sending a request \(an HTTP or HTTPS request\) to the Media Processing server and receiving the server’s response to this request. Upon receiving the user request, the Media Processing server verifies the identity and parameters for the request. After all verification procedures are passed, the Media Processing server submits and completes relevant operations based on the specified parameter in the request, and returns the processing result to the caller through an HTTP response.

## Procedure {#section_nzc_s1n_x2b .section}

-   Prepare request parameters.
-   Construct the Canonicalized Query String using the request parameters.
-   Construct the signature string.
-   Calculate the signature \(including the HMAC signature and Base64 code\).
-   Construct the request URL.

The following uses Java to show how to construct a request:

Global definition.

```

private static final String ENCODE_TYPE = "UTF-8";
private static final String ALGORITHM = "HmacSHA1";
private static final String HTTP_METHOD = "GET";
private static final String SEPARATOR = "&";
private static final String EQUAL = "=";
```

Prepare request parameters.

```

Map parameterMap = new HashMap();
// Request public parameters.
parameterMap.put("Action", "SearchTemplate");
parameterMap.put("Version", "2014-06-18");
parameterMap.put("AccessKeyId", "testId"); //Replace AccessKeyId with your AccessKeyId.
parameterMap.put("Timestamp", "2015-05-14T09:03:45Z");//This timestamp is fixed for test. The signature value generated in the sample code remains unchanged. You can easily compare and verify the data. To generate a variable timestamp, replace this sentence with the following sentence:
//parameterMap.put("Timestamp", formatIso8601Date(new Date())); 
parameterMap.put("SignatureMethod", "HMAC-SHA1");
parameterMap.put("SignatureVersion", "1.0");
parameterMap.put("SignatureNonce", "4902260a-516a-4b6a-a455-45b653cf6150"); //The unique random number is fixed for test. The signature value generated in the sample code remains unchanged. You can easily compare and verify the data. To generate a variable unique random number, replace this sentence with the following sentence:
//parameterMap.put("SignatureNonce", UUID.randomUUID().toString());
parameterMap.put("Format", "XML"); //The JSON format is also supported.
```

Construct the Canonicalized Query String using the request parameters.

```

private static String percentEncode(String value) throws UnsupportedEncodingException {
return URLEncoder.encode(value, ENCODE_TYPE).replace("+", "%20").replace("*", "%2A").replace("%7E", "~");
}
private static String buildCanonicalizedQueryString(Map parameterMap) throws UnsupportedEncodingException {
// Sort the parameters.
List sortedKeys = new ArrayList(parameterMap.keySet());
Collections.sort(sortedKeys);
StringBuilder temp = new StringBuilder();
for (String key : sortedKeys) {
// The key and value need to be encoded.
String value = parameterMap.get(key);
temp.append(SEPARATOR).append(percentEncode(key)).append(EQUAL).append(percentEncode(value));
}
return temp.toString().substring(1);
}
```

Calculate the signature \(including the HMAC signature and Base64 code\).

```

private static String buildStringToSign(String canonicalizedQueryString) throws UnsupportedEncodingException {
// Generate the stringToSign characters.
StringBuilder temp = new StringBuilder();
temp.append(HTTP_METHOD).append(SEPARATOR);
temp.append(percentEncode("/")).append(SEPARATOR);
// The Canonicalized Query String needs to be encoded.
temp.append(percentEncode(canonicalizedQueryString));
return temp.toString();
}
private static String buildSignature(String keySecret, String stringToSign) throws UnsupportedEncodingException, InvalidKeyException, NoSuchAlgorithmException {
SecretKey key = new SecretKeySpec((keySecret + SEPARATOR).getBytes(ENCODE_TYPE), SignatureMethod.HMAC_SHA1);
Mac mac = Mac.getInstance(ALGORITHM);
mac.init(key);
byte[] hashBytes = mac.doFinal(stringToSign.toString().getBytes(ENCODE_TYPE));
byte[] base64Bytes = new Base64().encode(hashBytes);
String base64UTF8String = new String(base64Bytes, "utf-8");
return URLEncoder.encode(base64UTF8String, ENCODE_TYPE);
}
```

Construct the request URL.

```

private static String buildRequestURL(String signature, Map parameterMap) throws UnsupportedEncodingException {
// Generate the request URL.
StringBuilder temp = new StringBuilder("http://mts.aliyuncs.com/?") ;
temp.append(URLEncoder.encode("Signature", ENCODE_TYPE)).append("=").append(signature);
for (Map.Entry e : parameterMap.entrySet()) {
temp.append("&").append(percentEncode(e.getKey())).append("=").append(percentEncode(e.getValue()));
}
return temp.toString();
}
```

## Examples {#section_knr_fbn_x2b .section}

-   Prepare request parameters.
    -   The value of Access Key ID is `testId`.
    -   The value of Access Key Secret is `testKeySecret`.
    -   The value of Timestamp is `2015-05-14T09:03:45Z`.
    -   The value of SignatureNonce is `4902260a-516a-4b6a-a455-45b653cf6150`.
    -   The value of Action is `SearchTemplate`, and the value of PageSize is `2`.
    -   The value of Format is `XML`.
-   Construct the Canonicalized Query String using the request parameters.

    ```
    AccessKeyId=testId&Action=SearchTemplate&Format=XML&PageSize=2&SignatureMethod=HMAC-SHA1&SignatureNonce=4902260a-516a-4b6a-a455-45b653cf6150&SignatureVersion=1.0&Timestamp=2015-05-14T09%3A03%3A45Z&Version=2014-06-18
    ```

-   Construct the signature string.

    ```
    GET&%2F&AccessKeyId%3DtestId&Action%3DSearchTemplate&Format%3DXML&PageSize%3D2&SignatureMethod%3DHMAC-SHA1&SignatureNonce%3D4902260a-516a-4b6a-a455-45b653cf6150&SignatureVersion%3D1.0&Timestamp%3D2015-05-14T09%253A03%253A45Z&Version%3D2014-06-18
    ```

-   Calculate the signature \(including the HMAC signature and Base64 code\).

    ```
    kmDv4mWo806GWPjQMy2z4VhBBDQ%3D
    ```

-   Construct the request URL.

    ```
    http://mts.cn-hangzhou.aliyuncs.com/?Signature=kmDv4mWo806GWPjQMy2z4VhBBDQ%3D&SignatureVersion=1.0&Action=SearchTemplate&Format=XML&SignatureNonce=4902260a-516a-4b6a-a455-45b653cf6150&PageSize=2&Version=2014-06-18&AccessKeyId=testId&SignatureMethod=HMAC-SHA1&Timestamp=2015-05-14T09%3A03%3A45Z
    ```

-   Next, send an HTTP request \(for example, curl\) to the URL and obtain the response result \(the response result in the sample code is in XML format\) from the server.

    ```
    <SearchTemplateResponse>
            <RequestId>017F1B2D-2B5B-4441-ABBA-E0DC08F5AFEC</RequestId>
            <Template>
                <Id>88c6ca184c0e47098a5b665e2a126799</Id>
                <Name>MTS-example</Name>
                <Container>
                    <Format>mp4</Format>
                </Container>
                <Video>
                    <Codec>H. 264</Codec>
                    <Profile>high</Profile>
                    <Bitrate>Auto</Bitrate>
                    <Crf>15</Crf>
                    <Width>256</Width>
                    <Height>800</Height>
                    <Fps>25</Fps>
                    <Gop>10</Gop>
                    <Preset>lower</Preset>
                    <ScanMode></ScanMode>
                    <Bufsize>6000</Bufsize>
                    <Maxrate></Maxrate>
                    <BitrateBnd>
                       <Max></Max>
                       <Min></Min>
                    </BitrateBnd>
                </Video>
                <Audio>
                    <Codec>aac</Codec>
                    <Samplerate>44100</Samplerate>
                    <Bitrate>500</Bitrate>
                    <Channels>2</Channels>
                </Audio>
                <State>Normal</State>
            </Template>
        </SearchTemplateResponse>
    ```


## Complete sample code {#section_sz2_kdn_x2b .section}

The sample code is written in Java, and the package manager is Maven.

[Code download](http://outline.oss-cn-hangzhou.aliyuncs.com/doc/mts/demo/mts-signature-sample-source-0.1.zip)

[JAR binary distribution download](http://outline.oss-cn-hangzhou.aliyuncs.com/doc/mts/demo/mts-signature-sample-all-0.1.jar)

Execution command: java -jar mts-signature-sample-all-0.1.jar testId testKeySecret 4902260a-516a-4b6a-a455-45b653cf6150 2015-05-14T09:03:45Z SearchTemplate XML PageSize@=2

