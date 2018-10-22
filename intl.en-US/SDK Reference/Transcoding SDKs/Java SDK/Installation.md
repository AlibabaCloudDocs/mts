# Installation {#concept_tf1_r2w_y2b .concept}

This article introduces Maven installation method recommended by Alibaba Cloud Java SDK. Specifically, it includes two steps. First, add the Maven repository of Alibaba Cloud Java SDK to the pom.xml configuration file. Then, add MPS dependency.

1.  Add a Maven repository.

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
    ```

2.  Add dependency.

    Alibaba Java SDK Core and MPS Java SDK detailed version:

    -   [Alibaba Cloud Java SDK Core](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-core)

    -   [MPS Java SDK](https://mvnrepository.com/artifact/com.aliyun/aliyun-java-sdk-mts)

    Take the core of V3.5.0 SDK Core and V2.5.2 MPS SDK as an example:

    ```
    <dependency>
             <groupId>com.aliyun</groupId>
             <artifactId>aliyun-java-sdk-core</artifactId>
             <version>3.5.0</version>
       </dependency>
       <dependency>
             <groupId>com.aliyun</groupId>
             <artifactId>aliyun-java-sdk-mts</artifactId>
             <version>2.5.2</version>
       </dependency>
    ```

    In addition, a json repository dependency optional. In MPS API, many parameters are defined through json. And many json repositories for java are available, you can select the repository that you are familiar with. Take V1.2.46 [fastjson](https://github.com/alibaba/fastjson) as an example:

    ```
    <dependency>
           <groupId>com.alibaba</groupId>
           <artifactId>fastjson</artifactId>
           <version>1.2.46</version>
       </dependency>
    ```


pom.xml example:

```
<? xml version="1.0" encoding="UTF-8"? >
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>mps-demo-project</groupId>
  <artifactId>mps-demo-project</artifactId>
  <version>0.0.1-SNAPSHOT</version>
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
          <artifactId>aliyun-java-sdk-core</artifactId>
          <version>3.5.0</version>
      </dependency>
      <dependency>
          <groupId>com.aliyun</groupId>
          <artifactId>aliyun-java-sdk-mts</artifactId>
          <version>2.5.2</version>
      </dependency>
      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>fastjson</artifactId>
          <version>1.2.46</version>
      </dependency>
  </dependencies>
  <build>
      <finalName>${artifactId}-${version}</finalName>
      <plugins>
          <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-compiler-plugin</artifactId>
              <version>2.3.2</version>
              <configuration>
                  <source>1.6</source>
                  <target>1.6</target>
              </configuration>
          </plugin>
      </plugins>
  </build>
  </project>
```

