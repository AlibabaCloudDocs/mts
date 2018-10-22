# Add media {#concept_vj3_qhx_y2b .concept}

Add media file to Media Files, and the user can specify workflow ID to trigger the workflow, which then processes the video file:

```
package com.aliyun.mts;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.aliyuncs.mts.model.v20140618. AddMediaRequest;
    import com.aliyuncs.mts.model.v20140618. AddMediaResponse;
    import com.aliyuncs.profile.DefaultProfile;
    import org.apache.commons.lang.exception.ExceptionUtils;
    public class AddMedia {
        //Step 1 .set region：cn-hangzhou、cn-shenzhen、cn-shanghai、cn-beijing
        private static final String REGION = "cn-shenzhen";
        private static final String OSS_REGION = "oss-cn-shenzhen";
        private static final String mtsEndpoint = "mts." + REGION + ".aliyuncs.com";
        //Step 2.set accesskey & keySecret
        private static String accessKeyId = "";
        private static String accessKeySecret = "";
        private static DefaultAcsClient aliyunClient;
        static {
            try {
                DefaultProfile.addEndpoint(REGION, REGION, "Mts", mtsEndpoint);
            } catch (ClientException e) {
                System.out.print(ExceptionUtils.getStackTrace(e));
                System.exit(1);
            }
            aliyunClient = new DefaultAcsClient(DefaultProfile.getProfile(REGION, accessKeyId, accessKeySecret));
        }
        public static void main(String[] args) throws ClientException {
            AddMediaRequest request = new AddMediaRequest();
            request.setFileURL("http://mtb-sz-in.oss-cn-shenzhen.aliyuncs.com/media/r180-ABC.mp4");
            request.setMediaWorkflowId("829bed0300994057a49e4f16de957e34");
            try {
                AddMediaResponse response = aliyunClient.getAcsResponse(request);
                System.out.println(JSONObject.toJSONString(response));
            } catch (ServerException e) {
                System.out.println("Code:" + e.getErrCode() + " Msg:" + e.getMessage());
            } catch (ClientException e) {
                System.out.println("Code:" + e.getErrCode() + " Msg:" + e.getMessage());
            }
        }
    }
```

