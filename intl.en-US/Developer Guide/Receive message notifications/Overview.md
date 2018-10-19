# Overview {#concept_hcp_ccv_1fb .concept}

## Message format {#section_igy_j2v_1fb .section}

When media workflow execution starts or completes, a message is sent to the queue or topic \(notification\) specified by MNS.

-   Format definition

    A message body is in JSON format. For details about the field names, types, and descriptions, see **Media workflow message** in [AddMedia](../../../../reseller.en-US/API Reference/Media APIs/AddMedia.md#).

    The structure layers are defined as follows:

    -   Top layer

        It is a JSON object. Definition:

        \{`Basic attribute of the current activity`, `object to be executed by the workflow`\}

    -   `Basic attribute of the current activity`

        It is a top-layer key value attribute, rather than an independent object. See the following example. Definition:

        Workflow execution ID, activity name, activity type, activity state, error information.

    -   `Details of the object to be executed by the workflow`

        It is a JSON object. Definition:

        \{Workflow execution ID, media workflow ID, media workflow name, media ID, input file, workflow execution type, `activity object array`, creation time\}.

    -   `Activity object array`

        It is a JSON array, containing all activities executed to the current state. For example, a start message contains only the Start activity object, while a completion message contains all activity objects. Definition:

        \[`Activity object`, `activity object`…\]

    -   `Activity object`

        It is a JSON object. Definition:

        \{Activity name, activity type, task ID, activity state, start time, end time, error information\}.

-   Start

    “Activity type” in `activity basic attribute` is “Start”.

-   Complete

    “Activity type” in `activity basic attribute` is “Report”.

-   Example:

    ```
    {
          "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
          "Name": "Act-4",
          "Type": "Report",
          "State": "Success",
          "MediaWorkflowExecution": {
            "Name": "ConcurrentSuccess",
            "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
            "Input": {
                "InputFile": {
                    "Bucket": "inputfirst",
                    "Location": "oss-test",
                    "Object": "mediaWorkflow/ConcurrentSuccess/01.wmv"
                }
            },
            "State": "Success",
            "MediaId": "2be491ab4cb6499cd0befe5fcf0cb670",
            "ActivityList": [
                {
                    "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                    "Name": "Act-1",
                    "Type": "Start",
                    "State": "Success",
                    "StartTime": "2016-03-15T02: 53: 41Z",
                    "EndTime": "2016-03-15T02: 53: 41Z"
                },
                {
                    "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                    "Name": "Act-2",
                    "Type": "Transcode",
                    "JobId": "f34b6d1429dd491faa7a6c1c8f905285",
                    "State": "Success",
                    "StartTime": "2016-03-15T02: 53: 43Z",
                    "EndTime": "2016-03-15T02: 53: 47Z"
                },
                {
                    "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                    "Name": "Act-3",
                    "Type": "Snapshot",
                    "JobId": "c14150be33304825a5d67cd5364c35cb",
                    "State": "Success",
                    "StartTime": "2016-03-15T02: 53: 44Z",
                    "EndTime": "2016-03-15T02: 53: 45Z"
                },
                {
                    "RunId": "8f8aba5a62ab4127ae2add18da20b0f2",
                    "Name": "Act-4",
                    "Type": "Report",
                    "State": "Success",
                    "StartTime": "2016-03-15T02: 53: 49Z",
                    "EndTime": "2016-03-15T02: 53: 49Z"
                }
            ],
            "CreationTime": "2016-03-15T02: 53: 39Z"
          }
      }
    ```


## How to receive and resolve a message {#section_kvh_p2v_1fb .section}

-   Queue

    [PHP sample code](reseller.en-US/Developer Guide/Receive message notifications/Receive notification through queues.md#)

-   Topic \(notification\)

    [PHP sample code](reseller.en-US/Developer Guide/Receive message notifications/Receive message through topic notification.md#)


