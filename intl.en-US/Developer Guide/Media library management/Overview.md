# Overview {#concept_emj_hkv_1fb .concept}

You can access the media library by using the MPS SDK for [Java](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Java SDK/Overview.md#), [PHP](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/PHP SDK/Overview.md#), and [Python](../../../../reseller.en-US/SDK Reference/Transcoding SDKs/Python SDK/Overview.md#).

You can also access the media library through HTTP/HTTPS. For more information, see [API reference](../../../../reseller.en-US/API Reference/Terms.md#).

## Functions {#section_sr4_plv_1fb .section}

Media workflow management: Allows you to add, delete, modify, query, activate, and stop a media workflow.

Management of media workflow execution instances: Allows you to traverse and query execution instances.

Media management: Allows you to add, delete, modify, query, search for a media resource, maintain attributes \(the title, tag, cover, and description\) of a media set, and set the publishing status of a media set.

Media category management: Allows you to add, delete, modify, and query a media category.

## Service scenarios {#section_clj_qlv_1fb .section}

-   Search for a media set

    Search for a media set that meets search criteria in the media library.

    You can use keywords to search for a media set. With logical disjunction, a media set is displayed if and only if one or more of the title, tag, description, and category are matched. With logical conjunction, a media set is displayed if and only if all specified attributes \(the title, tag, description, and category\) are matched.

    In the search criteria, you can specify the creation time range to limit the search range. You can also set whether the return results are sorted by creation time in ascending or descending order.

    In addition, if many APIs are to be returned, you can have them displayed in pages.

-   Maintain attributes of a media set

    Each media set contains basic attributes of the title, tag, description, and category, which can be set using APIs.

    [Basic attributes - Sample code - PHP](reseller.en-US/Developer Guide/Media library management/Basic video attributes.md#)

-   Manage tags of a media set

    Each tag is specific to a media set. No tag can be set for a media library globally. However, you can use API for searching for media sets to query all media sets with the same tags.

    [Manage tags - Sample code - PHP](reseller.en-US/Developer Guide/Media library management/Tag management.md#)


## Manage the category of a media set {#section_mjj_smv_1fb .section}

The media library provides global category management. You can associate each media set with a category and quickly retrieve a media set.

[Manage categories - Sample code - PHP](reseller.en-US/Developer Guide/Media library management/Category management.md#)

## Query details of a media set {#section_dym_tmv_1fb .section}

A media set contains an input file and several output files \(videos and screenshots\). You can query the detailed input and output information of a returned media set.

Input information includes the basic attributes \(width, height, duration, size, bit rate, and frame rate\) and details \(container encapsulation, video, audio, subtitle stream, and detailed attributes of the encapsulation and stream\) of a video.

Output information includes the basic attributes \(width, height, duration, size, bit rate, and frame rate\), OSS URL of a video as well as the type \(single-frame and batch\) and the OSS URL of a screenshot.

[Media set details - Sample code -PHP](reseller.en-US/Developer Guide/Media library management/Media details.md#)

