---
layout: post
title: "Spring Boot Maven Multi Modules on Visual Studio Code"
date: 2023-06-21 00:10:09 +0700
comments: true
categories: [java, maven, spring]
tags: [java, maven, spring]
excerpt_separator:  <!--more-->
---

In this we would like to add a new Spring Boot Web API module to the previous Maven Multi Modules project. To do that do the following steps.

1. Install [Spring Boot Extension Pack](https://marketplace.visualstudio.com/items?itemName=vmware.vscode-boot-dev-pack) on the VSCode plugin central.

2. Open the previous project on VSCode and open command palette <code>CMD + SHIFT + P</code> (for MacOS). Then select <code>Spring Initializr: Create a Maven Project</code>

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-spring-init.png" alt="" width="100%"/>

3. Select the Spring boot version, fill out the group and artifact id

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-spring-version-group-artifact.png" alt="" width="65%"/>

4. Select the packaging and Java version

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-spring-packaging-java-version.png" alt="" width="65%"/>

5. Select dependency of the Spring Boot

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-spring-dependency.png" alt="" width="65%"/>

6. Finally select the module location as we did previously (inside the parent/root project)

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-spring-location.png" alt="" width="65%"/>

7. Update the <code>pom.xml</code> of the Spring Boot project <code>api</code> by changing the parent to the root of the project.
   ``` xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
   
      <parent>
         <artifactId>multimodule</artifactId>
         <groupId>io.github.neutrofoton.multimodule</groupId>
         <version>1.0-SNAPSHOT</version>
      </parent>

      <groupId>io.github.neutrofoton.multimodule</groupId>
      <artifactId>api</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>api</name>
      <description>Demo project for Spring Boot</description>
      
      <dependencies>

         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
         </dependency>

         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
         </dependency>

         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
         </dependency>

         <dependency>
            <groupId>io.github.neutrofoton.multimodule</groupId>
            <artifactId>core</artifactId>
            <version>1.0-SNAPSHOT</version>
         </dependency>
      
         <dependency>
            <groupId>javax</groupId>
            <artifactId>javaee-api</artifactId>
            <version>8.0.1</version>
         </dependency>
         

      </dependencies>

      <build>
         <plugins>
            <!-- This plugin is optional if you like want to provide feature to let user build individual modules as well-->
            <plugin>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
         </plugins>
      </build>
      <repositories>
         <repository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>https://repo.spring.io/milestone</url>
            <snapshots>
               <enabled>false</enabled>
            </snapshots>
         </repository>
         <repository>
            <id>spring-snapshots</id>
            <name>Spring Snapshots</name>
            <url>https://repo.spring.io/snapshot</url>
            <releases>
               <enabled>false</enabled>
            </releases>
         </repository>
      </repositories>
      <pluginRepositories>
         <pluginRepository>
            <id>spring-milestones</id>
            <name>Spring Milestones</name>
            <url>https://repo.spring.io/milestone</url>
            <snapshots>
               <enabled>false</enabled>
            </snapshots>
         </pluginRepository>
         <pluginRepository>
            <id>spring-snapshots</id>
            <name>Spring Snapshots</name>
            <url>https://repo.spring.io/snapshot</url>
            <releases>
               <enabled>false</enabled>
            </releases>
         </pluginRepository>
      </pluginRepositories>

   </project>
   ```
   <!--more-->
8. The root of <code>pom.xml</code> should be:
   ``` xml

   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
         
   <modelVersion>4.0.0</modelVersion>
   <groupId>io.github.neutrofoton.multimodule</groupId>
   <artifactId>multimodule</artifactId>
   <version>1.0-SNAPSHOT</version>
   
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>3.1.1-SNAPSHOT</version>
      <relativePath/> 
   </parent>

   <packaging>pom</packaging>

   <modules>
      <module>core</module>
      <module>app</module>
      <module>api</module>
   </modules>
   

   <properties>
      <maven.compiler.source>20</maven.compiler.source>
      <maven.compiler.target>20</maven.compiler.target>
      <java.version>20</java.version>
   </properties>

   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>3.1.1-SNAPSHOT</version>
         </dependency>
         <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <version>3.1.1-SNAPSHOT</version>
            <scope>test</scope>
         </dependency>
         <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
            <scope>test</scope>
         </dependency>
         <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>4.10.0</version>
         </dependency>
         <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.8.0</version>
            <scope>test</scope>
         </dependency>
         <dependency>
            <groupId>io.github.bonigarcia</groupId>
            <artifactId>webdrivermanager</artifactId>
            <version>5.3.3</version>
         </dependency>
      </dependencies>
   </dependencyManagement>

   <build>
      <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
         <plugins>
         <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
         <plugin>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.1.0</version>
         </plugin>
         <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
         <plugin>
            <artifactId>maven-resources-plugin</artifactId>
            <version>3.0.2</version>
         </plugin>
         <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.0</version>
         </plugin>
       
         <plugin>
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.0.2</version>
         </plugin>
         <plugin>
            <artifactId>maven-install-plugin</artifactId>
            <version>2.5.2</version>
         </plugin>
         <plugin>
            <artifactId>maven-deploy-plugin</artifactId>
            <version>2.8.2</version>
         </plugin>
         <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
         <plugin>
            <artifactId>maven-site-plugin</artifactId>
            <version>3.7.1</version>
         </plugin>
         <plugin>
            <artifactId>maven-project-info-reports-plugin</artifactId>
            <version>3.0.0</version>
         </plugin>
         
         </plugins>
      </pluginManagement>
   </build>
   
   </project>

   ```

9. Create a simple REST api in the Api project. The detail code can be found [here](https://github.com/neutrofoton/maven-multiproject/tree/main)