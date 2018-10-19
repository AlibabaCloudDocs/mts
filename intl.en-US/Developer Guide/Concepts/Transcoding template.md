# Transcoding template {#concept_flv_mrj_z2b .concept}

Due to the many parameters of transcoding job, it is difficult to fill in the transcoding job repeatedly each time, transcoding templates are the concepts proposed to solve this problem, the essence is to combine some common parameters. Transcoding templates are available in two types: Preset templates and Custom templates.

-   Preset templates

    Pre-provided to users based on the common combination of some parameters. For more information, see [Preset template details](../../../../reseller.en-US/API Reference/Appendix/Preset template details.md#).

    Preset templates include several subtypes:

    -   Preset static template

        Can be used directly as transcoding template, including video transcoding, audio transcoding, transfer package and other scenarios. For example, “MP4-HD” and “MP3-128K”.

    -   NarrowBand HD template

        Narrowband HD is a unique technology for media transcoding. In the same bit rate, it can bring higher clarity so as to provide a better user experience at the same cost.

    -   Preset smart template

        The preset smart template automatically adjusts the transcoding parameters according to the characteristics of the input file, resulting in lower bit rate at the same resolution, thus reducing more cost.

        **Note:** When using the preset smart template, you first need to callSubmitAnalysisJob interface \(SubmitAnalysisJob\). After the analysis task successfully completes, you can call the Query Template Analysis Job interface \(QueryAnalysisJobList\) to obtain a valid preset smart template corresponding to the input file list. If the preset smart template specified in the submitted transcoding task is in an invalid list, the transcoding task is invalid and will return a failure.


-   Custom templates

    With a higher requirement, you can use a custom template to define your own combination of transcoding parameters \(audio, video, container, transcode, etc.\). Each custom template has a unique template ID.


