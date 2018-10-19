# Set a subaccount and authorization {#concept_j1l_dvt_1fb .concept}

Perform the following steps to set sub-accounts and authorizations.

1.  Create a subaccount.
    1.  Log on to the [RAM console](https://partners-intl.aliyun.com/login-required#/ram).
    2.  Click **Users** in the left-side navigation pane.
    3.  In **User Management**, click **Create User**.
    4.  In **Create User**, enter user information.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311318_en-US.png)

        **Note:** Select **Automatically generate an Access key for this user**, and properly store the AccessKey. The AccessKey of the subaccount will be used to obtain the token of STS.

2.  Create a role.
    1.  In the left-side navigation pane, click **Roles**.
    2.  Click **Create Role**.
    3.  In **Select Role**, select **User Role**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311319_en-US.png)

    4.  In **Enter Type**, select **Current Alibaba Cloud Account**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311320_en-US.png)

        **Note:** **Trusted Alibaba Cloud Account ID**is set to your current Alibaba Cloud account ID by default, which does not need to be specified. Click **Next**.

    5.  In **Configure Basic Role Information**, enter **Role Name**, and click **Create**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311321_en-US.png)

    6.  In **Roles**, click the created role.
    7.  In **Role Details**, record **Arn** parameter **acs:ram::1351140512345678:role/teststs**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311327_en-US.png)

3.  Set the role authorization.
    1.  Click **Role Authorization Policies**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311328_en-US.png)

    2.  Click **Edit Role Authorization Policy**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566311329_en-US.png)

        **Note:** To adjust the STS permissions of the subaccount \(for example, to modify, add, or delete a permission\), return to this step.

        You can create an authorization policy in **Custom Authorization Policy** and add this policy in Edit Authorization Policy to grant the minimum permission required by the upload SDK. The full policy content is as follows:

        ```
        {
             "Statement": [
               {
                 "Action": [
                   "oss:PutObject",
                   "oss:AbortMultipartUpload",
                   "oss:ListMultipartUploads",
                   "oss:ListParts"
                 ],
                 "Effect": "Allow",
                 "Resource": [
                   "*"
                 ]
               }
             ],
             "Version": "1"
          }
        ```

4.  Associate the subaccount with the role.
    1.  Log on to the RAM console, and click **Policies** in the left-side navigation pane.
    2.  Select **Custom Policy**, and click **Create Authorization Policy**.
    3.  In the text box of **Select an authorization policy template** \> **All templates**, enter the keyword **STS**. Sselect the template for `AliyunSTSAssumeRoleAccess` and go to the next step.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566411330_en-US.png)

    4.  In **Edit permissions and submit**, enter **Authorization Policy Name**.
    5.  In **Policy Content**, set the **Resource** field to the **Arn** parameter**acs:ram::1351140512345678:role/teststs**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566411331_en-US.png)

    6.  In the left-side navigation pane of the RAM console, click **Users**.
    7.  Select the subaccount you have set and click **Authorize** to edit your authorization policy.
    8.  Enter test, the created `teststspolice` is displayed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/153993566411339_en-US.png)


