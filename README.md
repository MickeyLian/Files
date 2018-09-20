#lianjunning
applicationContest.xml:
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.1.xsd">
<!-- 扫描基包 -->
<context:component-scan base-package="com.ljn"/>
<!-- 数据库加载的配置文件 -->
<context:property-placeholder location="classpath:jdbc.properties"/>
<!-- 数据库连接 -->
<bean id="dateSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
	<property name="driverClass" value="${jdbc.driverClassName}"/>
	<property name="jdbcUrl" value="${jdbc.url}"/>
	<property name="user" value="${jdbc.username}"/>
	<property name="password" value="${jdbc.password}"/>
	<property name="maxPoolSize" value="${c3p0.pool.maxPoolSize}"/>
	<property name="minPoolSize" value="${c3p0.pool.minPoolSize}"/>
	<property name="initialPoolSize" value="${c3p0.pool.initialPoolSize}"/>
	<property name="acquireIncrement" value="${c3p0.pool.acquireIncrement}"/>
</bean>
<!-- sqlSessionFactory -->
<bean id="sqlSesssionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	<property name="dataSource" ref="dateSource"></property>
	<!-- configLocation指定全局配置文件的位置 -->
	<!-- <property name="configLocation"  value="classpath:mybatis-config.xml"></property> --> 
	
	<property name="mapperLocations" value="classpath:com/ljn/mapper/*.xml"></property>
</bean>
<!-- mapper扫描器 -->
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
	<property name="basePackage" value="com.ljn.dao"></property>
	
</bean>
<!-- 事务管理器 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
	<property name="dataSource" ref="dateSource"></property>
</bean>
</beans>

springmvc.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">
<!-- 包扫描 -->
<context:component-scan base-package="com.ljn.controller"></context:component-scan>
<!-- 视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
	<property name="prefix" value="/jsp/"></property>
	<property name="suffix" value=".jsp"></property>
</bean>

<mvc:annotation-driven/>
</beans>

jdbc.properties:
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=utf-8&allowMultiQueries=true
jdbc.username=root
jdbc.password=123456
c3p0.pool.maxPoolSize=20
c3p0.pool.minPoolSize=5
c3p0.pool.initialPoolSize=3
c3p0.pool.acquireIncrement=2

mybatis-config.xml:
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

</configuration>

web.xml:
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">
  <display-name>Archetype Created Web Application</display-name>
  <!-- spring框架 -->
  <!-- needed for ContextLoaderListener -->
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath:applicationContext.xml</param-value>
	</context-param>

	<!-- Bootstraps the root web application context before servlet initialization -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
  <!-- springmvc前端控制器 -->
  <!-- The front controller of this Spring Web application, responsible for handling all application requests -->
	<servlet>
		<servlet-name>springDispatcherServlet</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>classpath:springmvc.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>

	<!-- Map all requests to the DispatcherServlet for handling -->
	<servlet-mapping>
		<servlet-name>springDispatcherServlet</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
  <!-- 编码过滤器 -->
  <filter>
  	<filter-name>encodingFilter</filter-name>
  	<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
  	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>
  	</init-param>
  </filter>
  <filter-mapping>
  	<filter-name>encodingFilter</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>
</web-app>





