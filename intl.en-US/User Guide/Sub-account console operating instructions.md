# Sub-account console operating instructions {#concept_twb_5x2_x2b .concept}

You can grant related permissions for sub-accounts through accessing Alibaba Cloud Resource Access Management \(RAM\) to enable the sub-accounts to use the MPS console within the authorized scope.

Permissions of the sub-account mainly include authorization to use MPS and the permissions to OSS, CDN, and MNS resource objects. After planning the resource instances of the sub-account with these services, you can create authorization policies based on corresponding authorization templates and grant the permissions to the sub-account.

The following variables are used in the resource authorization policies of each service. Replace them with the actual resource instance name.

## Description of variables {#section_jtg_r1f_x2b .section}

-   $Uid: Cloud account ID. You can query it by logging on to the**console** \> **Account Management** \> **Security Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910075_en-US.png)

-   $Region: Service region. For more information, see [service region](intl.en-US/User Guide/Service regions.md#).
-   $InputBucket: MPS InputBucket.
-   $OutputBucket: MPS Output Bucket.
-   $QueueName: MNS queue name.
-   $TopicName: MNS notification topic.
-   $DomainName: CDN domain name.

## Authorization policy creation descriptions {#section_elg_lbf_x2b .section}

Log on to the **RAM console** \> **Policies**, and create the following example custom authorization policies for the specified resource instance and grant them to the specified sub-account.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910077_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910078_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910080_en-US.png)

**Note:** Copy the authorization policies of each service of the examples in this document, and replace the variables with the corresponding service instance name.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910081_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910082_en-US.png)

**Note:** After the authorization policies are created for various service resource objects, you can grant the permissions to corresponding sub-accounts. See the permission granting instructions of MPS.

## MPS {#section_dq2_22f_x2b .section}

You can directly use the built-in`AliyunMTSFullAccess` authorization policy.

Permission description: Permission granted to a sub-account to use MTS.

Log on to the **RAM console** \> **Users**, and grant the `AliyunMTSFullAccess` permission to the specified sub-account.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910083_en-US.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11369/155436108910084_en-US.png)

## OSS authorization policy {#section_zp4_52f_x2b .section}

Permission description:

Permission for all operations on the specified input and output buckets.

Permission to view the bucket list.

```
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "oss:*"
      ],
      "Resource": [
        "acs:oss:*:*:$InputBucket",
        "acs:oss:*:*:$InputBucket/*",
        "acs:oss:*:*:$OutputBucket",
        "acs:oss:*:*:$OutputBucket/*"
      ],
      "Effect": "Allow"
    },
    {
      "Action": [
        "oss:ListBuckets"
      ],
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}
```

## MNS authorization policy {#section_bgb_dff_x2b .section}

Permission description:

Permission for all operations on the specified queues and topics.

Permission to query queues and topics.

```
{
  "Version": "1",
  "Statement": [
    {
      "Action": [
        "mns:*"
      ],
      "Resource": [
        "acs:mns:$Region:$Uid:/queues/$QueueName",
        "acs:mns:$Region:$Uid:/topics/$TopicName",
        ],
      "Effect": "Allow"
    },
    {
      "Action": [
        "mns:Get*",
        "mns:List*"
      ],
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}
```

## CDN authorization policy {#section_w3z_fff_x2b .section}

Permission description:

Permission for all operations on the specified CDN domain name.

Permission to query the CDN domain name.

```
{
  "Version": "1",
  "Statement": [
    {
      "Action": "cdn:*",
      "Resource": [
        "acs:cdn:*:$Uid:domain/$DomainName"
      ],
      "Effect": "Allow"
    },
    {
      "Action": "cdn:Describe*",
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}
```

