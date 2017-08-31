Jersey
==

### Build RESTful Server with Jersey 2.x and Tomcat8 in Intellij
 
 - #### 1.Create Module/Project of RESTful Web Service
 
  a) File-->New-->Module...
 
  b) Choose 'Java Enterprise' in left side, and choose 'RESTful Web Service' in right side and finish.
 
 - #### 2.Add Framework Support to Module
 
  a) Right Click on the module created, choose 'Add Framework Support...'
  b) Select 'Web Application' for creating 'web.xml', and select 'Maven'
 
 - #### 3.Config pom.xml (Ignore the regular config content such as groupId .etc)
 
  a) Add Jersey Dependency:
  
 ```xml
 <dependencies> 
  <dependency> 
   <groupId>org.glassfish.jersey.containers</groupId> 
   <artifactId>jersey-container-servlet</artifactId> 
   <version>2.2</version> 
  </dependency> 
 </dependencies> 
 ```
 
  b) Add packaging config:
  
  ```xml
    <packaging>war</packaging>
    <name>test</name>
  ```
  
  - #### 4.Create Server and config the web.xml
  For example the package of Server class is com.test.package
  
  ```xml
   <servlet> 
<servlet-name>JAX-RS Servlet</servlet-name> 
<servlet-class>org.glassfish.jersey.servlet.ServletContainer</servlet-class> 
<init-param> 
<param-name>jersey.config.server.provider.packages</param-name> 
<param-value>com.test.package</param-value> 
</init-param> 
<init-param> 
<param-name>jersey.config.server.provider.classnames</param-name> 
<param-value>com.fasterxml.jackson.jaxrs.json.JacksonJsonProvider</param-value> 
</init-param> 
<load-on-startup>1</load-on-startup> 
</servlet> 
<servlet-mapping> 
<servlet-name>JAX-RS Servlet</servlet-name> 
<url-pattern>/rest/*</url-pattern> 
</servlet-mapping> 
  ```
  
  - #### 5.Create the Server Class:
  ```java
  package com.test.pacakge;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;
import javax.ws.rs.core.MediaType;
import javax.ws.rs.core.Response;

@Path("hello")
public class TestResource {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public Response hello() {
       
        return Response.status(200).entity("hello").build();
    }
}
  ```
  
  - #### 5.Choose the war in the configuration of Tomcat
  
  - #### 6.Run the Tomcat Server
  
  - #### 7.Test
   Process GET request with uri: 'http://localhost:8080/rest/hello' and the result is 'hello'
