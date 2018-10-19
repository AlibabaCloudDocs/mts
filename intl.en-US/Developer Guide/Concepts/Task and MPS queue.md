# Task and MPS queue {#concept_e2n_j4j_z2b .concept}

This article introduces several basic concepts and relationships in MPS to help developers better understand and use MPS.

Concept description:

-   Task

    A task in the MPS is an abstract concept which contains a variety of types of tasks: transcoding tasks, screenshot tasks, and media information tasks.

    One task contains three key pieces of information: input, output and parameters. Input and output parameters are used to set the input file and the output file for the completed task. These parameters are used to set the detailed configuration for executing the specific function.

-   Parameters
    -   Template parameters

        Due to the large number of tasks, it is rework to repeat each task submission. Templates are a concept proposed to solve this problem. The essence of the template is a collection of commonly used parameters. This collection can reduce the number of parameters that need to be specified when submitting the task, thus simplifing the submission code.

    -   API parameters

        To create a template for each different combination of parameters can result in a dramatic increase in the number of templates and make template management more complex. Therefore, parameters can be set not only in the template, but also through the API.

    -   Covering order

        The API parameter has a higher priority than the corresponding parameter in the template and will cover the latter.

        For example: the same video can be transcoded to output multiple resolutions \(HD, SD\), different definition formats \(MP4\), encoding standards \(H. 264\) and frame rate. The difference lies only in the rate and resolution. You can create a template with a default combination of parameters \(MP4 + H. 264 +25FPS +2Mbps +1280x720\). When calling the API, if the API parameter is not set, the task is executed according to the default parameters \(2Mbps +1280x720\); and if the API parameter \(4Mbps +1920x1080\) is set, the task is executed according to the API parameters instead \(4Mbps +1920x1080\).

-   MPS queues

    After the user submits a task through the API interface, the task queues in the MPS queue first and then is executed in the order of priority and submission order.

    The tasks in the MPS queueq can have multiple priorities \(10 is the top priority, 1 is the lowest 1, 6 is the default\). In case of the same priority , the taskes submitted earlier are executed first. For tasks submitted at the same time, those with higher priority are executed first.

-   Task execution and completion
    -   Synchronous and asynchronous

        Depending on the type of job, some jobs can be completed quickly, however, most jobs cannot be completed instantly. There are two ways to execute jobs: synchronous and asynchronous. Synchronous types \(such as screenshot tasks\) return results immediately, while asynchronous types \(such as transcoding tasks\) results in two kinds of queries: scheduled polling and message notification.

    -   Regular polling

        Each task is identified by a unique task ID, which is returned synchronously to the caller when the task is submitted, after which task results can be queried by the task ID. The disadvantage of this approach lies in the fact that it is not executed in real time.

        Notifications:

        The MPS queue can be configured to send message notifications, you can get the task results instantly when they are ready. The message notification contains several important pieces of information: task ID, user data, and result.

        -   Task ID

            When you submit a task, record the task ID, and then compare it with the task ID of the message notification to know the result belongs to which task.

        -   User data

            When submitting a task, you can enter custom user data parameters \(such as commodity IDs\) each time you execute. The custom user data parameters are then returned in the message notification without the need to record the task ID in the business system. Meanwhile, you can use custom user data, such as commodity IDs, to associate the business system.


