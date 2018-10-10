# Transcoding message notifications {#concept_jzv_wzx_w2b .concept}

MPS fully supports message queue and message notification functions of MNS. The following takes the message notification service as an example. The operation of usig the message queue to receive messages is performed in a similar way. Enable the transcoding message notification function before use.

1.  Create Notification Topics.

    Create the topic in the same region on the MNS console and complete subscription.

    1.  Create a topic.
        1.  Click **Topics**.
        2.  Select the region.
        3.  Click **Create Topic**.
        4.  Enter the **Topic Name** on the **Create Topic** page.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11355/15391631299970_en-US.png)

    2.  Create a subscription.
        1.  Click **Subscribe**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11355/15391631299971_en-US.png)

        2.  On the **Subscribe**page, enter the **Subscription Name**and the **Endpoint**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11355/15391631299976_en-US.png)

2.  Set the binding relationship between the MPS queue and notification.
    1.  Log on to the [Media Processing console](https://partners-intl.aliyun.com/login-required#/mts).
    2.  Click **Settings.**.
    3.  Select the region.
    4.  Click **MPS Queues**.
    5.  Click **Message Notification**.
    6.  Select the **Message Type** and **Message Name**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/11355/15391631309974_en-US.png)

        The relationship between the MPS queue and notification is binded successfully.

3.  Establish the message notification receiving service.

    For more information, see [Message Notification function description](https://help.aliyun.com/document_detail/38991.html?spm=a2c4g.11186623.2.13.b4c74810VYzSwJ).

4.  Operate messages in the consumer’s queue.

    After MPS completion messages are received using an MNS queue, the message consumer must actively receive and delete messages.

    -   For more information about how to receive messages, see [Receive a queue message](https://help.aliyun.com/document_detail/35136.html?spm=a2c4g.11186623.2.14.b4c74810VYzSwJ) and [Receive queue messages in batches](https://help.aliyun.com/document_detail/35137.html?spm=a2c4g.11186623.2.15.b4c74810VYzSwJ).

    -   For more information about how to delete messages, see [Delete a queue message](https://help.aliyun.com/document_detail/35138.html?spm=a2c4g.11186623.2.16.b4c74810VYzSwJ) and [Delete queue messages in batches](https://help.aliyun.com/document_detail/35139.html?spm=a2c4g.11186623.2.17.b4c74810VYzSwJ).


