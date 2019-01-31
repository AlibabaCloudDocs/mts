# Set a subaccount and authorization {#concept_j1l_dvt_1fb .concept}

Perform the following steps to set sub-accounts and authorizations.

1.  Create a subaccount.
    1.  Log on to the [RAM console](https://partners-intl.aliyun.com/login-required#/ram).
    2.  In the left-side navigation pane, click **Identities** \> **Users**.
    3.  Click **Create User**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238142_en-US.png)

    4.  In**Create user**, create a subaccount which has the same permissions as the primary account to access MPS.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238144_en-US.png)

        **Note:** Tick **Programmatic Access**.

    5.  Generate AccessKey for this account, copy and save the AccessKey for subsequent access.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238167_en-US.png)

2.  Create a role.
    1.  In the left-side navigation pane, click **RAM Roles**.
    2.  Click **Create RAM Role**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238200_en-US.png)

    3.  In **Select type of trusted entity**, select **Alibaba Cloud Account**.

        In **Select Trusted Alibaba Cloud Account**, select **Current Alibaba Cloud Account**, and click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238201_en-US.png)

    4.  In **RAM Roles**, click the created role.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238216_en-US.png)

    5.  In **Basic Information**, copy **ARN** parameter **acs:ram::1612618906552077:role/mps**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404238202_en-US.png)

3.  Set the role authorization.
    1.  On the page of the created role, click **Add Permissions**.
    2.  Select policy.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404338204_en-US.png)

        **Note:** To adjust the STS permissions of the subaccount \(for example, to modify, add, or delete a permission\), return to this step.

        You can create a policy in **Custom Policy** and add this policy in editing policy to grant the minimum permission required by the upload SDK. The full policy content is as follows:

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
    1.  Log on to the RAM console, and click **Permissions** \> **Policies** in the left-side navigation pane.
    2.  Click **Create Policy**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404338208_en-US.png)

    3.  In **Create Custom Policy**, set **Resource** field to **ARN** parameter **acs:ram::1612618906552077:role/mps**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404338218_en-US.png)

    4.  In the left-side navigation pane, click **Identities** \> **Users**.
    5.  Select the subaccount you have set, and click **Add Permissions**.
    6.  Enter the created test policy and `teststspolicy` is displayed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11386/154891404338232_en-US.png)


