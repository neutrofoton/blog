---
layout: post
title: "Microservice Short Summary"
date: 2024-05-19 00:07:09 +0700
comments: true
categories: [microservice, pattern]
tags: [microservice, pattern]
excerpt_separator:  <!--more-->
---

# What is Microservice
Based on definition on [wikipedia](https://en.wikipedia.org/wiki/Microservices), a microservice architecture is a variant of the service-oriented architecture structural style. It is an architectural pattern that arranges an application as a collection of loosely coupled, fine-grained services, communicating through lightweight protocols. One of its goals is that teams can develop and deploy their services independently of others. 

In general, microservice has some characteristics
- Microservices achitecture decomposes an application into **small independent services**
- Microservices are **small, independent,** and **loosely coupled** services that can work together
- Each service has a **separate codebase** which can be managed by a small development team
- Microservices communicate each other using **well defined APIs**
- Microservices can be **deployed independently** and **autonomously**
- Microservices may have their own **technology stack**, can work with many **different technology stacks**.
- Microservices has its **own database** that is not shared with other services
- Microservices are organized by **business capability**, with the **bounded contexts**. 
- Following **Single Responsibility Principle** that referring separating responsibilities as per services.

Each microservice may has its own design pattern implemented in. The design pattern implemented on each microservice may different one another on the cluster. Since each microservice is idenpendent each others. The following picture ilustrated how it can be.

 <img class="center" src="{{ site.baseurl }}/assets/images/post/microservice/internal-pattern-microservice.png" alt="" width="90%"/>

The choosing of what design pattern that is suitable applied on each microservice depends on the aim of the microservice itself. Each pattern has pros and cons. So we should be wise on choosing which the best fit to the business need.

# Benefit of Microservices
- **_Agility, Innovation and Time-to-market_**<br/>
    Microservices architectures make applications easier to scale and faster to develop, enabling innovation and accelerating time-to-market for new features.

- **_Flexible Scalability_**<br/>
    Microservices can be scaled independently, so you scale out sub-services that require less resources, without scaling out the entire application.

- **_Small, focused teams_**<br/>
    Microservices should be small enough that a single feature team can build, test, and deploy it.

- **_Small and separated code base_**<br/>
    Microservices are not sharing code or data stores with other services, it minimizes dependencies, and that makes easier to adding new features

- **_Easy Deployment_**<br/>
    Microservices enable continuous integration and continuous delivery, making it easy to try out new ideas and to roll back if something doesn’t work.

- **_Technology agnostic, Right tool for the job_** <br/>
    Small teams can pick the technology that best fits their microservice and using a mix of technology stacks on their services.

- **_Resilience and Fault isolation_** <br/>
    Microservices are fault toleranced and handle faults correctly for example by implementing retry and circuit breaking patterns.

- **_Data isolation_**
    Databases are separated with each other according to microservices design. Easier to perform schema updates, because only a single database is affected.

# Challenges of Microservices Architecture
- **_Complexity_**<br/>
    Each service is simpler, but the entire system is more complex. Deployments and Communications can be complicated for hundreds of microservices.

- **_Network problems and latency_**<br/>
    Microservice communicate with inter-service communication, we should manage network problems. Chain of services increase latency problems and become chatty API calls.
    
- **_Development and testing_**<br/>
    Hard to develop and testing these E2E processes in microservices architectures if we compare to monolithic ones.

- **_Data integrity_**<br/>
    Microservice has its own data persistence. Data consistency can be a challenge. Follow eventual consistency where possible.

- **_Deployment_**<br/>
    Deployments are challenging. Require to invest in quite a lot of devops automation processes and tools. The complexity of microservices becomes overwhelming for human deployment.

- **_Logging & Monitoring_**<br/>
    Distributed systems are required to centralized logs to bring everything together. Centralized view of the system to monitor sources of problems.

- **_Debugging_**<br/>
    Debugging through local IDE isn’t an option anymore. It won’t work across dozens or hundreds of services.

# When to Use Microservices Architecture
- **_Make Sure You Have a “Really Good Reason” for Implementing Microservices_**<br/>
    Check if your application can do without microservices. When your application requires agility to time-to-market with zero-down time deployments and updated independently that needs more flexibility.

- **_Iterate With Small Changes and Keep the Single-Process Monolith as Your “Default”_**<br/>
    Sam Newman and Martin Fowler offers Monolithic-First approach. Single-process monolithic application comes with simple deployment topology. Iterate and refactor with turning a single module from the monolith into a microservices one by one.

- **_Required to Independently Deploy New Functionality with Zero Downtime_**<br/>
    When an organization needs to make a change to functionality and deploy that functionality without affecting rest of the system.

- **_Required to Independently Scale a Portion of Application_**<br/>
    Microservice has its own data persistence. Data consistency can be a challenge. Follow eventual consistency where possible.

- **_Data Partitioning with different Database Technologies_**<br/>
    Microservices are extremely useful when an organization needs to store and scale data with different use cases. Teams can choose the appropriate technology for the services they will develop over time.

- **_Autonomous Teams with Organizational Upgrade_**<br/>
    Microservices will help to evolve and upgrade your teams and organizations. Organizations need to distribute responsibility into teams, where each team makes decisions and develops software autonomously.

# When Not to Use Microservices
- **_Don’t do Distributed Monolith_**<br/>
    Distributed Monolith is the worst case because you increase complexity of your architecture without getting any benefit of microservices.
    <br/>
    Make sure that you decompose your services properly and respecting the decoupling rule like applying bounded context and business capabilities principles.


- **_Don’t do microservices without DevOps or cloud services_**<br/>
    Microservices are embrace the distributed cloud-native approaches. And you can only maximize benefits of microservices with following these cloud-native principles.

        a. CI/CD pipeline with devops automations
        b. Proper deployment and monitoring tools
        c. Managed cloud services to support your infrastructure
        d. Key enabling technologies and tools like Containers, Docker, and Kubernetes
        e. Following asnyc communications using Messaging and event streaming services

- **_Limited Team sizes, Small Teams_**<br/>
    If you don’t have a team size that cannot handle the microservice workloads, This will only result in the delay of delivery.
    
    For a small team, a microservice architecture can be hard to justify, because team is required just to handle the deployment and management of the microservices themselves.

- **_The Shared Database anti-pattern_**<br/>
    Shared database will potentially make each service depends on one onothers. It will break the idea of microservice itself.

# Monolithic vs Microservices

| Focus    | Monolithic                             | Microservice 
| -------- | -------                                | ---
| Application Architecture  | Simple straightforward structure of one undivided unit    | Complex structure that consists of various heterogeneous services and databases
| Scalability  | Scaling a whole single unit   | can be scaled unevenly
| Deployment  | Fast and easy deployment of the whole system   | zero-downtime deployment and CI/CD automation.
| Development team| No need containerazation knowledge| Need containarization knowledge
|Architecture Comparison | |
| Deployment Comparison | |

# The Database-per-Service Pattern
- Core characteristic of the microservices architecture is the loose coupling of services. every service should have its own databases, it can be polyglot persistence among to microservices.

- The service’s database can’t be accessed directly by other microservices. Each service’s persistent data can only be accessed via Rest APIs.

# Benefits of the Database-per-Service Pattern with Polygot Persistence
- Data schema changes made easy without impacting other microservices.
- Each database can be scaled independently.
- Microservices domain data is encapsulated within the service.
- If one of the database server is down, this will not affect to other services.
- Polyglot data persistence gives ability to select the best optimized storage needs per microservices.

# References
- https://martinfowler.com/articles/microservices.html
- https://www.freecodecamp.org/news/solid-principles-single-responsibility-principle-explained/