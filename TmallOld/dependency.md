```
<dependencies>  
  <!-- Database -->  
  <dependency>  
    <groupId>mysql</groupId>  
    <artifactId>mysql-connector-java</artifactId>  
    <version>5.1.47</version>  
  </dependency>  <dependency>    <groupId>com.alibaba</groupId>  
    <artifactId>druid</artifactId>  
    <version>1.1.19</version>  
  </dependency>  
  <!-- Json -->  
  <dependency>  
    <groupId>com.alibaba</groupId>  
    <artifactId>fastjson</artifactId>  
    <version>1.2.58</version>  
  </dependency>  
  <!-- Jsp compatible-->  
  <dependency>  
    <groupId>javax.servlet</groupId>  
    <artifactId>jstl</artifactId>  
  </dependency>  <dependency>    <groupId>org.apache.tomcat.embed</groupId>  
    <artifactId>tomcat-embed-jasper</artifactId>  
    <scope>provided</scope>  
  </dependency>  <dependency>    <groupId>org.apache.taglibs</groupId>  
    <artifactId>taglibs-standard-impl</artifactId>  
    <version>1.2.5</version>  
  </dependency>  
  <!-- Mybatis -->  
  <dependency>  
    <groupId>org.mybatis</groupId>  
    <artifactId>mybatis</artifactId>  
    <version>3.5.1</version>  
  </dependency>  <dependency>    <groupId>org.mybatis.spring.boot</groupId>  
    <artifactId>mybatis-spring-boot-starter</artifactId>  
    <version>2.1.0</version>  
  </dependency>  
  <!-- Spring -->  
  <dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter</artifactId>  
    <exclusions>      <exclusion>        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-logging</artifactId>  
      </exclusion>    </exclusions>  </dependency>  <dependency>    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-web</artifactId>  
    <version>2.1.6.RELEASE</version>  
  </dependency>  <dependency>    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-actuator</artifactId>  
    <version>2.1.6.RELEASE</version>  
  </dependency>  <dependency>    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-tomcat</artifactId>  
    <version>2.1.6.RELEASE</version>  
  </dependency>  <dependency>    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-log4j2</artifactId>  
  </dependency>  
  <!-- log4j2 -->  
  <dependency>  
    <groupId>org.apache.logging.log4j</groupId>  
    <artifactId>log4j-slf4j-impl</artifactId>  
    <version>2.10.0</version>  
  </dependency>  <dependency>    <groupId>org.apache.logging.log4j</groupId>  
    <artifactId>log4j-core</artifactId>  
    <version>2.10.0</version>  
  </dependency>  <dependency>    <groupId>org.apache.logging.log4j</groupId>  
    <artifactId>log4j-api</artifactId>  
    <version>2.10.0</version>  
  </dependency></dependencies>
```