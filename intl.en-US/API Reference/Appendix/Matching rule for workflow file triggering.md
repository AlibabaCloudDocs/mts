# Matching rule for workflow file triggering {#reference_m3p_5pn_y2b .reference}

## Matching rule for workflow file triggering {#section_ar1_xpn_y2b .section}

Matching rule executes the strategy in the following way:

Based on the path of new files, the matching rule checks the location where the workflow is bound. If the path of the new file includes the string which the matching rule is bound to, it complies with the matching rule. If the path of the new file does not include the string which the matching rule is bound to, it does not comply with the matching rule. For example, the rule `http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test1.flv`:

```
1. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/         Matched
    2. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/           Matched
    3. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/             Matched
    4. http://bucket.oss-cn-hangzhou.aliyuncs.com/                Matched
    5. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/C/test.flv  Matched
    6. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B/CC/         Not matched
    7. http://bucket.oss-cn-hangzhou.aliyuncs.com/A/B2/           Not matched
    8. http://bucket.oss-cn-hangzhou.aliyuncs.com/A2/B/C/         Not matched
```

**Note:** Do not configure the input path of a workflow as the prefix of the input path of another workflow, or one incremental file triggers two workflow executions. For example, the input paths of two workflows are configured as test and test1 respectively, when an input file is uploaded to the test1 directory, which has the same prefix with test, therefore, two workflow executions are triggered.

## Matching file extension {#section_w2l_1qn_y2b .section}

Triggering requirement is that the file is a multi-media file, Media Files service determines through the extension of a file. The file does not have an extension, when the filename does not include extension separator \(“.”\), or the extension complies with the following rules:

**Note:** For swf, the screenshot and transcoding quality are not guaranteed.

|Type|Extension|
|:---|:--------|
|Video|3gp, asf, avi, dat, dv, flv, f4v, gif, m2t, m3u8, m4v, mj2, mjpeg, mkv, mov, mp4, mpe, mpg, mpeg, mts, ogg, qt, rm, rmvb, swf, vob, wmv, webm.|
|Audios|aac, ac3, acm, amr, ape, caf, flac, m4a, mp3, ra, wav, wma, aiff.|

