# Receive message through topic notification {#concept_hly_zfv_1fb .concept}

MNS actively pushes message notifications by topic to users. You can conveniently receive the messages if an HTTP service can be publicly accessed.

## Basic structure {#section_k3f_dgv_1fb .section}

The basic structure of a video media repository notification is as follows:

-   The outermost layer is the structure body of MNS.

-   The `message body` of MNS is the structure body of the media repository.

    After receiving the `message body`, MNS further resolves the message of the media repository. For more information about the resolution steps and sample codes, see [Receive a message in queue mode](reseller.en-US/Developer Guide/Receive message notifications/Receive notification through queues.md#).


## Security {#section_fbl_2gv_1fb .section}

