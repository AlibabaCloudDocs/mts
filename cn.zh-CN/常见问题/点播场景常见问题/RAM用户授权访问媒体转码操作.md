# RAM用户授权访问媒体转码操作

本文介绍了通过阿里云主账号授权RAM用户访问媒体转码的操作步骤及说明。

## 场景

通过阿里云访问控制服务（RAM）可为RAM用户授予相关权限，以达到RAM用户在授权范围使用媒体转码（MTS）控制台的目的。RAM用户的权限主要包括MTS、OSS、CDN和MNS产品使用权限，规划RAM用户拥有这些服务的资源实例后即可按相应的授权模版创建授权策略，并授予给RAM用户即可。

## 操作步骤

1.  子账户创建

    1.  登录[RAM控制台](https://ram.console.aliyun.com/overview)。

    2.  单击**用户** \> **新建用户**。

    3.  创建登录名称及密码。

    4.  单击**确定**，子账号创建成功。

        ![图片](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2308767061/p198784.png)

2.  子账户授权

    1.  选择新建的子账户，并单击添加权限。

        ![图片](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2308767061/p198786.png)

    2.  选择AliyunOSSFullAccess，AliyunCDNFullAccess，AliyunMTSFullAccess和AliyunMNSFullAccess并单击确定，授权完成。

        ![图片](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2308767061/p198788.png)

        **说明：** 此处授权的是MPS服务中所需要的四个产品的全部权限，如果需要更细粒度的权限控制看高级设置。

3.  子账户登录

    1.  单击**概览**。

    2.  获取RAM用户登录地址，单击**链接**。

    3.  输入账户密码登录体bucket，进入媒体转码控制台操作。

        **说明：** 子账户初次登录需要重置密码。

4.  高级设置存在用户需求对各个产品进行更细权限的控制，可以创建自定义权限，将对应的自定义权限授权子账户。

    -   创建自定义授权策略
        1.  选择**权限管理** \> **权限策略管理** 。
        2.  单击**新建授权策略**，填入对应授权策略。

            ![图片](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2308767061/p198794.png)

            **说明：** 授权策略可以看OSS授权策略、CDN授权策略或MNS授权策略。

    -   OSS授权策略

        权限描述：

        -   对指定的输入、输出Bucket有所有操作权限
        -   查看Bucket列表权限，示例如下：

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

            **说明：**

            -   $InputBucket：VOD媒体输入Bucket，填入具体工作流中要涉及到的bucket名称。$OutputBucket：VOD媒体输出Bucket，填入具体工作流中要涉及到的bucket名称。
            -   这里的oss:ListBuckets权限是子账号需要通过可视化工具操作OSS必备的权限，该权限赋予后子账号登录可以查看到所有的bucket列表，但是仅能操作前面赋权的$InputBucket和$OutputBucket这两个bucket，并且该权限暂时仅支持赋权给所有的bucket，不支持赋权给某个bucket。
    -   MNS授权策略

        权限描述：

        -   对指定的Queue、Topic有所有权限
        -   有查询Queue、Topic的权限，示例如下：

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

            **说明：**

            -   $QueueName：MNS队列名称，填入具体工作流中要涉及到的队列名称。
            -   $TopicName：MNS通知主题名称，填入具体工作流中要涉及到的通知名称。
    -   CDN授权策略

        权限描述：

        -   对指定的CDN加速域名有所有权限
        -   有查询CDN加速域名的权限，示例如下：

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

            **说明：** $DomainName：CDN加速域名名称，填入具体工作流中要涉及到的cdn域名名称。


