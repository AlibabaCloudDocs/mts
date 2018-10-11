# Request security token - Java sample code {#concept_lsq_fbv_1fb .concept}

1.  Reference the STS SDK in pom.xml.

    ```
    <repositories>
         <repository>
             <id>sonatype-nexus-staging</id>
             <name>Sonatype Nexus Staging</name>
             <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
             <releases>
                 <enabled>true</enabled>
             </releases>
             <snapshots>
                 <enabled>true</enabled>
             </snapshots>
         </repository>
     </repositories>
    <dependencies>
     <dependency>
       <groupId>com.aliyun</groupId>
       <artifactId>aliyun-java-sdk-sts</artifactId>
       <version>2.1.6</version>
     </dependency>
     <dependency>
       <groupId>com.aliyun</groupId>
       <artifactId>aliyun-java-sdk-core</artifactId>
       <version>2.2.0</version>
     </dependency>
    </dependencies>
    ```

2.  Code.

    STS requires the role parameter `roleArn`. Log on to the [RAM console](https://partners-intl.aliyun.com/login-required#/ram), click **Roles**, and then click a specific **Role Name**. The `Arn` parameter is displayed in the basic information, for example, `1351140512345678:role/teststs`.

    -   Main Function.

        ```
        public static void main(String[] args) throws Exception {
           IClientProfile profile = DefaultProfile.getProfile(
                                                  "cn-hangzhou",
                                                  <accessKeyId>,
                                                  <accessKeySecret>);
           DefaultAcsClient client = new DefaultAcsClient(profile);
           AssumeRoleResponse response = assumeRole(client, <roleArn>);
           AssumeRoleResponse.Credentials credentials = response.getCredentials();
           System.out.println(credentials.getAccessKeyId() + "\n" +
                              credentials.getAccessKeySecret() + "\n" +
                              credentials.getSecurityToken() + "\n" +
                              credentials.getExpiration());
        }
        ```

    -   Function that generates the temporary AccessKey and token.

        ```
        private static AssumeRoleResponse assumeRole(
                                           DefaultAcsClient client,
                                           String roleArn)
                                           throws ClientException {
           final AssumeRoleRequest request = new AssumeRoleRequest();
           request.setVersion("2015-04-01");
           request.setMethod(MethodType.POST);
           request.setProtocol(ProtocolType.HTTPS);
           request.setDurationSeconds(900L);
           request.setRoleArn(roleArn);
           request.setRoleSessionName("test-token");
           return client.getAcsResponse(request);
        }
        ```

3.  Token validity period.

    The token generated in the sample code is valid for 900s, which can be adjusted as required \(ranging from 900s to 3600s\).

    You can use a generated token in the validity period, instead of repeatedly generating new tokens. The following example shows how to check whether a token needs to be generated again.

    ```
    private static boolean isTimeExpire(String expiration) {
         Date nowDate = new Date();
         Date expireDate = javax.xml.bind.DatatypeConverter.parseDateTime(expiration).getTime();
         if (expireDate.getTime() <= nowDate.getTime()) {
             return true;
         } else {
             return false;
         }
    }
    ```


