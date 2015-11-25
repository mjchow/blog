## springmvc-基于maven的搭建
##### 1.如果只想有请求处理请求的话一个maven配置一个jar就够了spring-webmvc
##### 2.如果要配置freemarker的话只需一个freemarker的jar就够了

----
* web.xml
```xml
	<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/j2ee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd"
	version="2.4">
	
	<display-name>mjchow's web project</display-name>
	<!--  spring Web MVC框架提供了org.springframework.web.filter.CharacterEncodingFilter用于解决POST方式造成的中文乱码问题-->
	<filter>      
	    <filter-name>CharacterEncodingFilter</filter-name>      
	    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>      
	    <init-param>      
	        <param-name>encoding</param-name>      
	        <param-value>utf-8</param-value>      
	    </init-param>      
	</filter>      
	<filter-mapping>      
	    <filter-name>CharacterEncodingFilter</filter-name>      
	    <url-pattern>/*</url-pattern>      
	</filter-mapping>
	 
	<!--  配置Servlet-->	  
	<servlet>
		<servlet-name>springmvc</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>classpath:springmvc.xml</param-value>
		</init-param>
	</servlet>
	<servlet-mapping>
		<servlet-name>springmvc</servlet-name>
		<!--  只拦截.x结尾的请求-->
		<url-pattern>*.x</url-pattern>
	</servlet-mapping>
</web-app>
```

* pom.xml
```xml
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-webmvc</artifactId>
		<version>3.1.0.RELEASE</version>
		<type>jar</type>
		<scope>compile</scope>
	</dependency>
	
	<dependency>
		<groupId>org.freemarker</groupId>
		<artifactId>freemarker</artifactId>
		<version>2.3.16</version>
	</dependency>
```
* springmvc.xml
```xml
	<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xmlns:p="http://www.springframework.org/schema/p"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context-3.0.xsd
            http://www.springframework.org/schema/aop
            http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
            http://www.springframework.org/schema/tx
            http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
            http://www.springframework.org/schema/mvc
            http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context-3.0.xsd">
            
            
       <!--  开启扫描的包-->     
       <context:component-scan base-package="zmj.*"/>
       <!-- 
       	该标签隐式的向Spring容器注册了：
		AutowiredAnnotationBeanPostProcessor   
		CommondAnnotationBeanPostProcessor
		PersistenceAnnotationBeanPostProcessor   
		RequiredAnnotationBeanPostProcessor这四个BeanPostProcessor. 
		@Autowired @Resource 等等有关
	   -->
       <context:annotation-config/>
       
       <bean id="freemarkerConfig" class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer">
       		<property name="TemplateLoaderPath" value="/WEB-INF/views/"/>
       		<property name="freemarkerVariables">  
	            <map>  
	                <entry key="webRoot" value="abc"></entry>  
	            </map>  
        	</property>
        	<property name="freemarkerSettings">  
	            <props>  
	            	<!--  模板更新时间默认是5s 如果ftl文件做了修改则会去生效-->
	                <!-- <prop key="template_update_delay">3600</prop> -->  
	                <prop key="tag_syntax">auto_detect</prop><!-- 设置标签类型 两种：[] 和 <> 。[] 这种标记解析要快些 -->  
	                <prop key="default_encoding">UTF-8</prop>  
	                <prop key="output_encoding">UTF-8</prop>  
	                <prop key="locale">zh_CN</prop>  
	                <prop key="date_format">yyyy-MM-dd</prop>  
	                <prop key="time_format">HH:mm:ss</prop>  
	                <prop key="datetime_format">yyyy-MM-dd HH:mm:ss</prop>  
	                <prop key="number_format">#</prop><!-- 设置数字格式 以免出现 000.00 -->  
	                <prop key="classic_compatible">true</prop><!-- 可以满足一般需要。默认情况变量为null则替换为空字符串，如果需要自定义，写上${empty!"EmptyValue of fbysss"}的形式即可  -->  
	                <prop key="template_exception_handler">html_debug</prop><!-- ignore,debug,html_debug,rethrow -->  
	            </props>  
        	</property>
	   </bean>
	   
	   
	   <bean id="viewResolver"
			class="org.springframework.web.servlet.view.freemarker.FreeMarkerViewResolver">
			<property name="cache" value="true" />
			<property name="prefix" value="" />
			<property name="suffix" value=".ftl" />
			<property name="contentType" value="text/html; charset=GBK" />
	   </bean>
</beans>
```


