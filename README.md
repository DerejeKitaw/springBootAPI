# springBootAPI

## Create pom.xml file
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>com.example</groupId>
<artifactId>myproject</artifactId>
<version>0.0.1-SNAPSHOT</version>
<parent>
 <groupId>org.springframework.boot</groupId>
 <artifactId>spring-boot-starter-parent</artifactId>
 <version>2.0.4.RELEASE</version>
</parent>
<!-- Additional lines to be added here... -->
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
</dependencies>
</project>
```
## To see dependencies
```
mvn dependency:tree
```

## Installing package
```
mvn package
```
## Writing the Code
```java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.web.bind.annotation.*;
@RestController
@EnableAutoConfiguration
public class Example {

  @RequestMapping("/")
  String home() {
    return "Hello World!";
  }

  public static void main(String[] args) throws Exception {
    SpringApplication.run(Example.class, args);
  }
}
 ```
> @RestController : 
  * is known as a stereotype annotation. 
  * It provides hints for people reading the code and for Spring that the class plays a specific role. In this case, our class is a web `@Controller`, so Spring considers it when handling incoming web requests.
  * is annotation tells Spring to render the resulting string directly back to the caller.

  > @RequestMapping :
  * is an annotation provides “routing” information. 
  * It tells Spring that any HTTP request
with the / path should be mapped to the home method.

> The `@RestController` and `@RequestMapping` annotations are Spring MVC annotations.
(They are not specific to Spring Boot.) See the [MVC section in the Spring Reference
Documentation](https://docs.spring.io/spring/docs/5.0.8.RELEASE/spring-framework-reference/web.html#mvc) for more details.

> @EnableAutoConfiguration :
  *  tells Spring Boot to “guess” how you want to configure Spring, based on the jar dependencies that you have added. Since spring-boot-starter-web added Tomcat and Spring MVC, the auto-configuration assumes that you are developing a web application and sets up Spring accordingly.

  ## Running the application
 
> Since `spring-boot-starter-parent` POM used, can use to start the application. Type 
```
mvn spring-boot:run
```

## Creating an Executable Jar
> To create an executable jar, we need to add the `spring-boot-maven-plugin` to our pom.xml. To
do so, insert the following lines just below the dependencies section:
```xml
<build>
<plugins>
 <plugin>
 <groupId>org.springframework.boot</groupId>
 <artifactId>spring-boot-maven-plugin</artifactId>
 </plugin>
</plugins>
</build>
```
run
```
mvn package
```
> If you look in the target directory, you should see myproject-0.0.1-SNAPSHOT.jar. The file
should be around 10 MB in size. If you want to peek inside, you can use `jar tvf`, as follows:
```
jar tvf target/myproject-0.0.1-SNAPSHOT.jar
```
> You should also see a much smaller file named myproject-0.0.1-SNAPSHOT.jar.original in
the target directory. This is the original jar file that Maven created before it was repackaged by Spring
Boot.
> To run that application, use the 
```
java -jar target/myproject-0.0.1-SNAPSHOT.jar
```