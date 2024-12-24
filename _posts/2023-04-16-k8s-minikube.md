---
layout: post
title: "K8s - Minikube"
date: 2023-04-16 00:00:09 +0700
comments: true
categories: [kubernetes]
tags: [kubernetes]
excerpt_separator:  <!--more-->
---

## Installing kubectl
Installation steps of <code>kubectl</code> can be found [here](https://kubernetes.io/docs/tasks/tools/)

``` bash
# install with brew
brew install kubectl

# check the version
kubectl version --client

# or the new command check version
kubectl version --output=json
```
## Installing minikube
Installation steps of <code>minikube</code> can be found [here](https://minikube.sigs.k8s.io/docs/start/)

``` bash
# install with brew
brew install minikube

# check the installation
minikube version
```

```
minikube version: v1.29.0
commit: ddac20b4b34a9c8c857fc602203b6ba2679794d3
```

Starting the <code>minikube</code>
``` bash
# starting minikube (can be with not default parameter)
# minikube start --driver=virtualbox --container-runtime=cri-o
minikube start

# starting minikube on windows with hyperv
minikube start --driver=hyperv

```
> The environtiment machine I use:
> 1. Macos Monterey 12.6.3
> 2. VirtualBox-6.1.42 for Macos (intel)
> 3. Microsoft Windows 10 Pro
> 
> On Macos, I got an issue when using version 7.0 of virtual box. The issue was <code>["The host-only adapter we just created is not visible"]( https://github.com/kubernetes/minikube/issues/15377)</code>. It is solved by downgrading the VirtualBox version to 6.1.42.
> 
>Meanwhile, on Windows 10 Pro no issue I got by using parameter <code>--driver=hyperv</code>. Don't forget to run the terminal as <code>Administrator</code> otherwise it may get permission issue.


When we successfully starting minikube, checking the version will give us server and client information

``` bash
kubectl version --output=json
```

``` json
{
  "clientVersion": {
    "major": "1",
    "minor": "25",
    "gitVersion": "v1.25.2",
    "gitCommit": "5835544ca568b757a8ecae5c153f317e5736700e",
    "gitTreeState": "clean",
    "buildDate": "2022-09-21T14:33:49Z",
    "goVersion": "go1.19.1",
    "compiler": "gc",
    "platform": "darwin/amd64"
  },
  "kustomizeVersion": "v4.5.7",
  "serverVersion": {
    "major": "1",
    "minor": "26",
    "gitVersion": "v1.26.1",
    "gitCommit": "8f94681cd294aa8cfd3407b8191f6c70214973a4",
    "gitTreeState": "clean",
    "buildDate": "2023-01-18T15:51:25Z",
    "goVersion": "go1.19.5",
    "compiler": "gc",
    "platform": "linux/amd64"
  }
}
```

If we want to access app deployed in the minikube cluster, we use the IP of minikube which can be checked using:
``` bash
minikube ip
```

# Making Minikube connect to a local Docker image
1. Start Minikube

    ```bash
    minikube start
    ```
2. Set the Docker Environment for Minikube<br/>
  Minikube has its own Docker daemon, and you need to point your local shell to it. You can do this with the following command:
  
    ```bash
    eval $(minikube docker-env)
    ```

3. Build Your Docker Image<br/>
  Now, build your Docker image using the local Docker client (which is now connected to the Minikube Docker daemon). For example:

    ```bash
    docker build -t your-image-name .
    ```

4. Verify the Image in Minikube
  To make sure your image is available in Minikube, you can list the images in Minikube's Docker daemon:

    ```bash
    docker images
    ```

5. Use the Image in Kubernetes
  Now, you can use your image in Kubernetes deployments or pods as you normally would. Here's an example of a deployment YAML that uses the local image:

    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-deployment
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: my-app
      template:
        metadata:
          labels:
            app: my-app
        spec:
          containers:
          - name: my-container
            image: your-image-name
            ports:
            - containerPort: 8080

    ```

6. To revert the Docker environment back to your local Docker daemon, you can run:

  ```bash
  eval $(minikube docker-env -u)
  ```