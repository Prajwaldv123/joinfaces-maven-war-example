JoinFaces War Example
=====
[![Build Status](https://github.com/joinfaces/joinfaces-maven-war-example/actions/workflows/maven.yml/badge.svg)](https://github.com/joinfaces/joinfaces-maven-war-example/actions)
[![Codecov](https://codecov.io/gh/joinfaces/joinfaces-maven-war-example/branch/4.7.x/graph/badge.svg)](https://codecov.io/gh/joinfaces/joinfaces-maven-jar-example)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=joinfaces_joinfaces-maven-war-example&metric=bugs)](https://sonarcloud.io/dashboard?id=joinfaces_joinfaces-maven-war-example)
[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

This SAP (Single Page Application) illustrates JSF usage inside WAR packaged Spring Boot Application.

[JoinFaces](https://joinfaces.org) autoconfigures 
[PrimeFaces](https://primefaces.org/), 
[PrimeFaces Extensions](https://primefaces-extensions.github.io/), 
[Apache MyFaces Tobago](https://github.com/apache/myfaces-tobago), 
[OmniFaces](https://omnifaces.org/), 
[AdminFaces](https://adminfaces.github.io/site/), 
[Mojarra](https://eclipse-ee4j.github.io/mojarra/) and 
[MyFaces](http://myfaces.apache.org) libraries to run at embedded 
[Tomcat](https://tomcat.apache.org/), 
[Jetty](https://www.eclipse.org/jetty) or 
[Undertow](https://undertow.io/). 
It autoconfigures [Weld](https://weld.cdi-spec.org),
[Apache OpenWebBeans](https://openwebbeans.apache.org/) and
[Rewrite](https://www.ocpsoft.org/rewrite/) too.

## Run Example Application locally

1- Clone this project
```Shell
git clone https://github.com/joinfaces/joinfaces-example-war.git
```

2- Build
```Shell
mvn clean install
```

3- Copy into tomcat

4- Start tomcat

5- Access starter page at **http://localhost:8080/joinfaces-example/**. This page can help you to choose the JoinFaces Starter that fits your needs. You may log in with credentials

| User       | Password | Roles      |
|------------|----------|------------|
| persapiens | 123      | ROLE_ADMIN |
| nyilmaz    | qwe      | ROLE_USER  |

Optional: If your IDE is showing build errors install [Lombok](https://projectlombok.org/setup/overview)

## Key Files

### pom.xml

Includes joinfaces starter dependency. All other jsf dependencies are included transitively.

```xml
<properties>
   <joinfaces.version>5.3.1</joinfaces.version>
</properties>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.joinfaces</groupId>
            <artifactId>joinfaces-dependencies</artifactId>
            <version>${joinfaces.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>org.joinfaces</groupId>
    <artifactId>faces-spring-boot-starter</artifactId>
  </dependency>
</dependencies>
```

Note that **security-spring-boot-starter** is included to secure the application.

```xml
<dependencies>
    <dependency>
        <groupId>org.joinfaces</groupId>
        <artifactId>security-spring-boot-starter</artifactId>
    </dependency>
</dependencies>
```

### src/main/resources/application.yml

Configure faces.PROJECT_STATE and faces.primefaces.THEME properties.

```yml
joinfaces:
  faces:
    PROJECT_STAGE: Development
  primefaces: 
    theme: overcast
```

### src/main/webapp/starter.xhtml

Example page to help you choose the right JoinFaces Starter for you. 

Note that xhtml, js, css and images files should be located at **src/main/resources/META-INF/resources** directory to JSF use them.

Look at **authorize** and **anonymous** jsf spring security facelet tags in action to secure page information.

```xhtml
  <sec:authorize access="hasRole('ROLE_ADMIN')">
    <p:panelGrid columns="1" rendered="#{sec:isFullyAuthenticated()}">
      <p:link title="Logout" href="/logout">
        <p:outputLabel value="You are logged in as an ADMIN" />
      </p:link>
    </p:panelGrid>
  </sec:authorize>
```

### src/main/java/org/joinfaces/example/JoinFacesExampleApplication.java

Very simple spring main application. Only SpringBootApplication configuration is required.

<pre>
@SpringBootApplication
public class JoinFacesExampleApplication {
</pre>

### src/main/java/org/joinfaces/example/SecurityConfig.java

Spring Security configuration class to secure authentication with credentials to persapiens and nyilmaz users.

### src/main/java/org/joinfaces/example/view/HelloWorldMBean.java

Managed bean using ViewScoped CDI annotation. The equivalent spring scope of ViewScoped annotation is configured automatically by JoinFaces Starter.

<pre>
@Named
<b>@ViewScoped</b>
public class StarterMBean {
</pre>

## Getting Help

* Report questions and bugs at [github.com/joinfaces/joinfaces/issues](https://github.com/joinfaces/joinfaces/issues).

## Contributing

* Report documentation, features, enhancement and bugs at [github.com/joinfaces/joinfaces/issues](https://github.com/joinfaces/joinfaces/issues).
* Pull requests are welcome.
