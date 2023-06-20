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