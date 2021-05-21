# Transcoding message notifications

MPS fully supports message queue and message notification functions of MNS. The following takes the message notification service as an example. The operation of usig the message queue to receive messages is performed in a similar way. Enable the transcoding message notification function before use.

1.  Create Notification Topics.

    Create the topic in the same region on the MNS console and complete subscription.

    1.  Create a topic.
        1.  Click **Topics**.
        2.  Select the region.
        3.  Click **Create Topic**.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/11355/15434760679977_en-US.png)

        4.  Enter the **Topic Name** on the **Create Topic** page.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/11355/15434760699970_en-US.png)

    2.  Create a subscription.
        1.  Click **Subscribe**.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/11355/15434760699971_en-US.png)

        2.  On the **Subscribe** page, enter the **Subscription Name** and the **Endpoint**.

            ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/11355/15434760709976_en-US.png)

2.  Set the binding relationship between the MPS queue and notification.
    1.  Log on to the [Media Processing console](https://mts.console.aliyun.com/?spm=5176.2020520001.0.0.6RsosT#/mts/oss).
    2.  Click **Settings.**.
    3.  Select the region.
    4.  Click **MPS Queues**.
    5.  Click **Message Notification**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/11355/15434760679978_en-US.png)

    6.  Select the **Message Type** and **Message Name**.

        ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/11355/15434760709974_en-US.png)

        The relationship between the MPS queue and notification is binded successfully.

3.  Establish the message notification receiving service.

    For more information, see Message Notification function description.

4.  Operate messages in the consumer’s queue.

    After MPS completion messages are received using an MNS queue, the message consumer must actively receive and delete messages.

    -   For more information about how to receive messages, see Receive a queue message and Receive queue messages in batches.

    -   For more information about how to delete messages, see Delete a queue message and Delete queue messages in batches.


