# Public parameters {#reference_zzt_mvm_x2b .reference}

## Public request parameters {#section_utv_nvm_x2b .section}

Public request parameters are the request parameters used by each API.

|Parameters|Type|Required or not|Description|
|:---------|:---|:--------------|:----------|
|Format|String|No|Format of the return value, which can be JSON or XML \(default\).|
|Version|String|Yes|API version, in the format of YYYY-MM-DD. The current version is 2014-06-18.|
|AccessKeyId|String|Yes|Your Access Key ID issued by Alibaba Cloud.|
|Signature|String|Yes|Signature result string. For more information about the signature calculation method, see [Signature mechanism](https://help.aliyun.com/document_detail/29217.html).|
|SignatureMethod|String|Yes|Signature method. Currently, HMAC-SHA1 is supported.|
|Timestamp|String|Yes|Timestamp of a request. The date format follows the ISO8601 standard and uses the UTC time. The format is YYYY-MM-DDThh:mm:ssZ. Example: 2014-7-29T12:00:00Z \(July 29, 2014 at 20:00:00, Beijing time\).|
|SignatureVersion|String|Yes|Signature algorithm version. The current version is 1.0.|
|SignatureNonce|String|Yes|Unique random number, used to prevent replay attacks. You must use different random numbers for different requests.|

Example

```

http://mts.cn-hangzhou.aliyuncs.com/
? Format=json 
&Version=2014-06-18
&Signature=vpEEL0zFHfxXYzSFV0n7%2FZiFL9o%3D 
&SignatureMethod=Hmac-SHA1
&SignatureNonce=9166ab59-f445-4005-911d-664c1570df0f
&SignatureVersion=1.0
&Action=SubmitJobs
&AccessKeyId=tkHh5O7431CgWayx 
&Timestamp=2014-07-29T09%3A22%3A32Z
```

## Public return parameters {#section_z42_zvm_x2b .section}

The system returns a unique identification code \(RequestId\) each time you send a request to call an API, no matter whether the call is successful or not.

XML example

```
<? xml version="1.0" encoding="UTF-8"? >
    <!—Result root node--> 
    <API name+Response> <!—Returned request tag-->
        <RequestId>4C467B38-3910-447D-87BC-AC049166F216</RequestId>
        <!—Returned results--> 
    </API name+Response>
 

```

JSON example

```

{
"RequestId": "4C467B38-3910-447D-87BC-AC049166F216", /* Returned results */
}
```

