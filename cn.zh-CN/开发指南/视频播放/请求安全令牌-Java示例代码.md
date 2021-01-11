# 请求安全令牌-Java示例代码

1.  pom.xml中引用STS的SDK。

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

2.  代码。

    STS需要一个角色的参数`roleArn`。登录 [RAM 控制台](https://ram.console.aliyun.com/#/overview)，单击 **角色管理**，再单击具体 **角色名称** 后，在基本信息中有一个参数`Arn`，例如`1351140512345678:role/teststs`。

    -   main函数

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

    -   生成临时AK和Token的函数

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

3.  Token有效期。

    示例代码中生成的Token有效时间为900秒，可以根据实际需求调整（最小900秒，最大3,600秒）。

    在有效期内，不需要反复生成新的Token，可以复用已经生成的Token。您可以通过以下方式判断何时需要重新生成token：

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


