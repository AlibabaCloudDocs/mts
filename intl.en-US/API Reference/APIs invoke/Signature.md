# Signature {#reference_m3m_wwm_x2b .reference}

Media Processing performs identity authentication on each access request. Therefore, both the HTTP and HTTPS request must contain signature information. MPS uses symmetric encryption with a pair of Access Key ID and Access Key Secret to authenticate the identity of a request sender. Access Key ID and Access Key Secret are officially issued by Alibaba Cloud to visitors \(visitors can apply for and manage them at Alibaba Cloud’s official website\). The Access Key ID indicates the identity of the visitor. The Access Key Secret is the secret key used to encrypt and verify the signature string on the server. It must be kept confidential and should only be available to Alibaba Cloud and the user.

Follow these steps to sign the access request:

1.  Construct the Canonicalized Query String using the request parameters.
    1.  The request parameters are ordered alphabetically by parameter name \(this includes the “public request parameters” and custom parameters for the given request APIs described in this document, but not the Signature parameter mentioned in “public request parameters”\).

        **Note:** For a request submitted using the GET method, these parameters constitute the parameter section of the request URI \(that is, the section in the URI following `?` and connected by `&`.

    2.  Encode the name and value of each request parameter. URL encoding using the UTF-8 character set is required. URL encoding rules are as follows:
        -   The letters \(A–Z and a–z\), the numerals \(0–9\), and the characters, hyphen `-`, underscore `_`, period `.`, and tilde `~` are not encoded.
        -   Other characters are encoded into `%XY` format, where XY represents the characters’ ASCII code in hexadecimal notation. For example, the double quotes \(“\) are encoded as `%22`.
        -   Extended UTF-8 characters are encoded into the `%XY%ZA…` “
        -   Note that an English space \( \) is encoded into `%20` rather than the plus sign \(+\).

            **Note:** Generally, libraries that support URL encoding \(for example, java.net.URLEncoder of Java\) are all encoded according to the rules for the `application/x-www-form-urlencoded` MIME-type. You can use this encoding method directly by replacing the plus sign \(+\) with %20 and the asterisk \(\*\) with `%2A`in the encoded string, and change `%7E` back to the tilde \(~\) to conform to the preceding encoding rules.

    3.  Connect the encoded parameter names and values with the equal sign \(=\).
    4.  Then, sort the parameter name and value pairs connected by equal sign in alphabetical order, and connect them with `&` to produce the Canonicalized Query String.
2.  The following example shows the pseudocode to create a canonical request.

    ```
    
    StringToSign=
    HTTPMethod + "&" +
    percentEncode("/") + "&" +
    percentEncode(CanonicalizedQueryString)
    ```

    Here, HTTPMethod is the HTTP method used for request submission, for example, GET.

    percentEncode\(“/“\) is the coded value for the character `/` according to the URL encoding rules described in 1.b, namely, `%2F`.

    percentEncode\(CanonicalQueryString\) is the Canonicalized Query String \(constructed in Step 1\) that is encoded according to the URL encoding rules described in 1.b.

3.  According to RFC2104 definitions, use the preceding signature string to calculate the signature’s HMAC value.

    **Note:** The Key used for calculating the signature is the "Access Key Secret" held by the user, ending with the `&` character \(ASCII:38\) based on the SHA1 hashing.

4.  Encode the HMAC value into a string based on Base64 encoding rules to obtain the signature.
5.  Add the obtained signature value as the Signature parameter to the request parameters to complete the request signing process.

    **Note:** The obtained signature value requires URL encoding based on the RFC3986 rule like other parameters before it is submitted as the final request parameter value to the Media Transcoding server.


Using SearchTemplate as an example, the request URL before signing is:

```
http://mts.cn-hangzhou.aliyuncs.com/?Timestamp=2015-05-14T09%3A03%3A45Z&Format=XML&AccessKeyId=testId&Action=SearchTemplate&PageSize=2&SignatureMethod=HMAC-SHA1&SignatureNonce=4902260a-516a-4b6a-a455-45b653cf6150&SignatureVersion=1.0&Version=2014-06-18
```

herefore, the Canonicalized Query String is:

```
AccessKeyId=testId&Action=SearchTemplate&Format=XML&PageSize=2&SignatureMethod=HMAC-SHA1&SignatureNonce=4902260a-516a-4b6a-a455-45b653cf6150&SignatureVersion=1.0&Timestamp=2015-05-14T09%3A03%3A45Z&Version=2014-06-18
```

Thus, the StringToSign is:

```
GET&%2F&AccessKeyId%3DtestId%26Action%3DSearchTemplate%26Format%3DXML%26PageSize%3D2%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D4902260a-516a-4b6a-a455-45b653cf6150%26SignatureVersion%3D1.0%26Timestamp%3D2015-05-14T09%253A03%253A45Z%26Version%3D2014-06-18
```

Assume that the Access Key ID parameter value is `testId` and, the Access Key Secret parameter value is `testKeySecret`, then, the key used for HMAC calculation is `testKeySecret&` and the calculated signature value is:

```
kmDv4mWo806GWPjQMy2z4VhBBDQ%3D
```

The signed request URL is \(with the Signature parameter added\):

```
http://mts.cn-hangzhou.aliyuncs.com/?Signature=kmDv4mWo806GWPjQMy2z4VhBBDQ%3D&SignatureVersion=1.0&Action=SearchTemplate&Format=XML&SignatureNonce=4902260a-516a-4b6a-a455-45b653cf6150&PageSize=2&Version=2014-06-18&AccessKeyId=testId&SignatureMethod=HMAC-SHA1&Timestamp=2015-05-14T09%3A03%3A45Z
```

For more information about code, see [Call an API](reseller.en-US/API Reference/APIs invoke/Call an API.md#).

