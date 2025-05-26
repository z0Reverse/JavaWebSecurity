1.很多项目jdk版本要求1.8，使用jdk17会导致很多插件安装之后仍然显示不匹配，不存在该插件
2.tomcat需要对应jdk1.8，否会报错
3.主要还是版本问题，serlvet也要对应好jdk版本



# 服务器不能正常启动-配置相关
## 问题1
Cannot find class [] for bean with name 'dataSource' defined in class path resource [spring-service.xml]; 
```
org.springframework.beans.factory.CannotLoadBeanClassException: 
Cannot find class [] for bean with name 'dataSource' defined in class path resource [spring-service.xml]; 
nested exception is java.lang.ClassNotFoundException: 
```

原因：
```
 <bean class="org.springframework.jdbc.datasource.DataSourceTransactionManager" id="transactionManager">         
	 <property name="dataSource" ref="dataSource"/>     
</bean>     
<bean id="dataSource" class=""/>
```
未指定dataSource导致服务器不能运行

解决方案：
1.不能使用gtp给的
```
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource"
    destroy-method="close">
    <property name="driverClassName" value="${jdbc.driver:com.mysql.jdbc.Driver}"/>
    <property name="url" value="${jdbc.url:jdbc:mysql://localhost:3306/test}"/>
    <property name="username" value="${jdbc.username:root}"/>
    <property name="password" value="${jdbc.password:123456}"/>
    <property name="initialSize" value="${jdbc.initialSize:5}"/>
    <property name="maxTotal" value="${jdbc.maxActive:20}"/>
    <property name="maxIdle" value="${jdbc.maxIdle:10}"/>
    <property name="minIdle" value="${jdbc.minIdle:5}"/>
</bean>
```
会导致版本相关问题，麻烦

2.采用这个方案
```
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource"> 
      <property name="driverClassName" value="${jdbc.driver}" />
      <property name="url" value="${jdbc.url}"/>
      <property name="username" value="${jdbc.username}"/>
      <property name="password" value="${jdbc.password}"/>
```
具体的value值要参考datasource.proties文件中的命名
```
jdbc.driver=com.mysql.jdbc.Driver  
jdbc.url=jdbc:mysql://localhost:3306/carrentalsystem?useUnicode=true&characterEncoding=UTF-8&useSSL=false  
jdbc.username=root  
jdbc.password=root
```

