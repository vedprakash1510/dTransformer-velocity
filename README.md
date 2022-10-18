### Dynamic-template based JSON to JSON transformer based on Velocity

We need only one line of code for this -

```java
from("undertow:{{server}}/search?useStreaming=true").to("velocity:test.vm").log("${body}");
```


- In the first part of this code we are using an undertow (jboss) to consume REST API.
- In the middle part of this code we are passing rest JSON body into a Velocity template. 
- In the last part of this code we are logging the transformed JSON body.

### How to run this project 

This project is a Spring Boot Maven project and can be easily run using maven command

```
mvn spring-boot:run
```

or import this project in any IDE as a maven project.

### Step by Step guide to create this project from scratch

- Create a Spring boot starter project in your favorite IDE.
- Add the following dependencies in the project pom.xml file. 

```xml
<properties>
    <java.version>17</java.version>
	<camel.version>3.9.0</camel.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>org.apache.camel.springboot</groupId>
			<artifactId>camel-spring-boot-starter</artifactId>
			<version>${camel.version}</version>
		</dependency>

		<dependency>
			<groupId>org.apache.camel.springboot</groupId>
			<artifactId>camel-jackson-starter</artifactId>
			<version>${camel.version}</version>
		</dependency>
		<dependency>
			<groupId>org.apache.camel.springboot</groupId>
			<artifactId>camel-undertow-starter</artifactId>
			<version>${camel.version}</version>
		</dependency>
		<dependency>
			<groupId>org.apache.camel.springboot</groupId>
			<artifactId>camel-velocity-starter</artifactId>
			<version>${camel.version}</version>
		</dependency>
	</dependencies>
  ```
- Create a new java class 

```java
import org.apache.camel.builder.RouteBuilder;
import org.springframework.stereotype.Component;

@Component
public class TransformerRouter extends RouteBuilder {
	@Override
	public void configure() throws Exception {

		from("undertow:{{server}}/search?useStreaming=true").to("velocity:test.vm").log("${body}");
	}

}

```
- In the above java code we extended the class and overrided public void configure() method
- After overriding method we used two components 1) Undetow for REST API and 2) Velocity for transformation
- Create a JSON transformation Velocity Template and put it in the classpath (e.g test.vm in resource folder) 
- Now this project is ready, run this project and it will transform JSON based on Velocity template.

Undertow official website - https://undertow.io/

Velocity official website - https://velocity.apache.org/
