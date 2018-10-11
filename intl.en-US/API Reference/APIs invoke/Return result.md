# Return result {#reference_f5v_gwm_x2b .reference}

After an API is called, data is returned in a unified format. The returned HTTP status code 2xx indicates that the call is successful. The returned HTTP status code 4xx or 5xx indicates that the call fails. For a successful call, the primary formats of returned data are XML and JSON. When a request is sent, an external system can input parameters to specify the format of the returned data. The default format is XML. In this document, examples of returned results are formatted for viewing convenience. The actual returned results have no line breaks, indentation, or other layouts.

## Successful results {#section_gjb_mwm_x2b .section}

XML example

```
<? xml version="1.0" encoding="UTF-8" ? >
    <! -Result root node-->
    <API name+ Response>
        <! -Return request tag-->
        <RequestId>25818875-5F78-4A13-BEF6-D7393642CA58</RequestId>
        <! -Returned results-->
    </API name+Response>
```

JSON example

```
{
        "RequestId": "4C467B38-3910-447D-87BC-AC049166F216", /* Returned results */
    }
```

## Failure results {#section_s1r_pwm_x2b .section}

If an error is reported in an API call, no result data is returned. The caller can locate the cause of an error based on the error code corresponding to each API and [Error code list](reseller.en-US/API Reference/Appendix/Error code list.md#). When an error occurs in a call, an HTTP status code 4xx or 5xx is returned for the HTTP request. The returned message body contains the specific error code and error message. The message body also contains the globally unique request ID \(RequestId\) and the requested host ID \(HostId\). If unable to locate the error cause, the caller can provide Alibaba Cloud customer service with the HostId and RequestId, and we will help solve the problem as soon as possible.

XML example

```
<? xml version="1.0" encoding="UTF-8"? > 
    <Error>
        <RequestId>8906582E-6722-409A-A6C4-0E7863B733A5</RequestId> 
        <HostId>mts.cn-hangzhou.aliyuncs.com</HostId> 
        <Code>UnsupportedOperation</Code>
        <Message>The specified action is not supported. </Message>
    </Error>
```

JSON example

```

{
"RequestId": "8906582E-6722-409A-A6C4-0E7863B733A5", 
"HostId": "mts.cn-hangzhou.aliyuncs.com", 
"Code": "UnsupportedOperation",
"Message": "The specified action is not supported."
}
```

