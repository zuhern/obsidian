---
Created: Invalid date
Updated: Invalid date
---
1. property -> deploy assembly 에 경로 맞는지 확인

2. cos.jar

3. commons-logging.1.1.1.jar

4. quartz-2.2.1.jar 도 tomcat 서버 lib에다가 넣어 줌

5. slf4j-api-1.7.6.jar 도 tomcat 서버 lib에다가 넣어 줌

6. i-sysframe-2.5.8-SNAPSHOT.jar 도 tomcat 서버 lib에다가 넣어 줌

7. jersey-container-servlet-core-2.6.jar

8. jersey-server-2.6.jar

9. jersey-common-2.6.jar

10. javax.ws.rs-api-2.0.jar

11. aopalliance-1.0.jar

12. ojdbc6-11.1.0.7.0.jar

13. ubanks-objects-crm.xml

14. jotm-1.5.3.jar

hk2-utils-2.2.0.jar

jdom-1.1.3.jar

xercesImpl-2.11.0.jar

log4j-1.2.17.jar

xml-apis-1.4.01.jar

oscore-2.2.4.jar

ognl-2.6.9.jar

json-simple-1.1.jar

hk2-api-2.2.0.jar

jersey-guava-2.6.jar

javax.inject-2.2.0.jar

hk2-locator-2.2.0.jar

javassist-3.18.1-GA.jar

javax.annotation-api-1.2.jar

jackson-jaxrs-json-provider-2.3.3.jar

jackson-jaxrs-base-2.3.3.jar

<object id=_"dataSource"_ class=_"com.ubanks.framework.dao.datasource.DriverManagerDataSource"_ singleton=_"true"_>  
        <property name=_"driverClassName"_>  
            <value>${jdbc.driverClassName}</value>  
  
        </property>  
  
        <property name=_"url"_>  
            <value>${jdbc.url}</value>  
  
        </property>  
  
        <property name=_"username"_>  
            <value>${jdbc.username}</value>  
  
        </property>  
  
        <property name=_"password"_>  
            <value>${jdbc.password}</value>  
  
        </property>  
  
    </object>  

<!-- object id="dataSource" class="com.ubanks.framework.bo.jndi.JndiObjectFactoryBO" singleton="true">

<property name="jndiName"><value>jdbc/crmPool</value></property>

</object> -->

<classpathentry kind=_"con"_ path=_"org.maven.ide.eclipse.MAVEN2_CLASSPATH_CONTAINER"_><attributes><attribute name=_"org.eclipse.jst.component.dependency"_ value=_"true"_/></attributes>

</classpathentry>

<webcontent-dir>${basedir}\src\main\webapp\WEB-INF\lib</webcontent-dir>

http://localhost:5681/wbs/wf/app/ifIndex.html\#/view/login