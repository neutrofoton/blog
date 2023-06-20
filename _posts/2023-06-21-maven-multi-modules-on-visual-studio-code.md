---
layout: post
title: "Maven Multi Modules on Visual Studio Code"
date: 2023-06-21 00:00:09 +0700
comments: true
categories: [java, maven]
tags: [java, maven]
excerpt_separator:  <!--more-->
---

Visual Studio Code has many plugin in supporting various programming languages. One of them is Java. One of pupular plugin of VSCode which supports Java is [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack). In this post will show you how to create Java project using maven by utilizing the VSCode plugin.

## Creating Java (Maven) Project on VSCode
1. Makesure we have Java SDK and VSCode installed in our system.
2. Install VSCode plugin [Extension Pack for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack).  

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-installed.png" alt="" width="35%"/>

3. To create new project, select <code>Create Java Project</code>. Then select type of project you want. In this post we will use maven based.

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-project-type.png" alt="" width="60%"/>

4. Fill out the maven project setting.
   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-maven-setting-version.png" alt="" width="60%"/>

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-maven-setting-groupid.png" alt="" width="60%"/>

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-maven-setting-artifactid.png" alt="" width="60%"/>

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-maven-setting-path.png" alt="" width="60%"/>

5. VSCode will generate a java project for you.

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-generating-project.png" alt="" width="100%"/>

   While generating the Java project, we will be asked for the version. If we agree with default version <code>1.0-SNAPSHOT</code>, we just need to press <code>Enter</code>. Then follow the next question in the terminal tab.

6. Finally the Java project generated and displayed in the File explorer of VSCode.

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-generated-project.png" alt="" width="35%"/>

## Setup Maven Multi Modules Projects
To setup the previous Maven project as Maven Multi Modules projects, let's do the following steps.

1. Delete the <code>src</code> and <code>target</code> folder and their contents on the provious project. Then Edit the root <code>pom.xml</code> as below.

   ``` xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
         
   
   <modelVersion>4.0.0</modelVersion>
   <groupId>io.github.neutrofoton.multimodule</groupId>
   <artifactId>multimodule</artifactId>
   <version>1.0-SNAPSHOT</version>
   <packaging>pom</packaging>

   </project>
   ```

2. Run maven <code>install</code> to ensure the <code>pom.xml</code> is valid.
   
   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-install-empty-root.png" alt="" width="100%"/>

3. If no error on step #2, then add a new maven project as a new maven module. To do that, right click on the VSCode Explorer > select <code>Create Maven Project</code>.

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-create.png" alt="" width="35%"/>

4. Fill out the group and artifact as we did previously.
   
   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-group-artifact.png" alt="" width="60%"/>

   > We use the sama group id as parent/root <code>pom.xml</code>. But a new name for artifact, in this case we named it <code>core</code> module.

5. Select the destionation folder of the module iside the root/parent project.

   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-folder.png" alt="" width="60%"/>

6. Create another module called <code>app</code> by repeating step #3 to #5.
   
7. The <code>pom.xml</code> should be updated as follow.
   
   ``` xml
   <?xml version="1.0" encoding="UTF-8" standalone="no"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
         
   <modelVersion>4.0.0</modelVersion>
   <groupId>io.github.neutrofoton.multimodule</groupId>
   <artifactId>multimodule</artifactId>
   <version>1.0-SNAPSHOT</version>

   <packaging>pom</packaging>

   <modules>
      <module>core</module>
      <module>app</module>
   </modules>
   
   </project>
   ```

   And the project structure should be like this
   <img class="center" src="{{ site.baseurl }}/assets/images/post/maven-vscode/maven-vscode-multi-modules-structure.png" alt="" width="100%"/>

8. To ensure the project well defined, we can run maven install on the root <code>pom.xml</code>

> ### Tips
> To clear the plugin cache of the Java plugin, we can run <br/> 
> (MacOS) : CMD + Shift + P then type <code>Java: Clean Java language Server Workspace</code>