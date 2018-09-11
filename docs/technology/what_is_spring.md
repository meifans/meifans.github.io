# “Spring” 技术栈

## 当我们在说Spring时，我们在说什么？
`Spring`这个词在不同的Context下有不同的含义，它可以指 `Spring Framework`，也可以代指基于此发展而来的众多组件，或者干脆代表了`The Entire Family of Projects`。

`Spring Framework`划分为不同的模块。应用可以选择需要的模块。起核心作用的模块是`核心容器`，包括配置模型和依赖注入机制。除此以外，`Spring Framework`还为不同的应用架构提供了基础支持，包括消息、事务数据、持久化和web。它还支持基于Servlet 的`Spring MVC` web框架和`Spring WebFlux` 响应式web框架。

### Spring 的历史

Spring于2003年诞生，是一种应对J2EE编程的复杂性的解决方案。有人认为Spring是Java EE 的竞争对手，其实不然，它实际上是Java EE 的补充。Spring 框架不接纳 Java EE 平台的各项标准，相反地，它集成了一些从Java EE 体系精挑细选的JSR (Java Specification Requests) 规范，如下所示：
+ Servlet API (JSR 340)
+ Dependency Injection (JSR 330)
+ Common Annotations (JSR 250)
+ WebSocket API (JSR 356)
+ Concurrency Utilities (JSR 236)
+ JSON Binding API (JSR 367)
+ Bean Validation (JSR 303)
+ JPA (JSR 338)
+ JMS (JSR 914)
+ as well as JTA/JCA setups for transaction coordination, if necessary.

经过了这么多年，Java EE 和 Spring 在应用开发中的作用也在不断演进。最初是用来创建服务端应用程序。今天在Spring Boot 的帮助下，应用以DevOps和云原生的方式被创建，Servlet 容器已经内嵌并且变得微不足道。 在Spring Framework 5 中，WebFlux 应用甚至不在直接需要Servlet API，可以直接运行在服务器 ( 比如Netty ) 上而无需Servlet 容器。

除此以外，Spring Framework 已经衍生出其它项目，比如 Spring Boot, Spring Security, Spring Data, Spring Cloud, Spring Batch。

### Spring Framework 设计原则
+ 在每一层提供选择的能力。Spring 可以让你尽可能的推迟设计决策。比如，你可以通过配置更改持久层框架。这一点在其它基础架构和集成第三方API中都一致。它为各个组件和功能库提供了统一且兼容性极强的抽象。因此，当业务发展需要更换基础组件时，比如缓存，储存，消息等，可以方便的更换而无需更改上层的代码。
+ 兼容并包。Spring更倾向灵活性，并不会强制要求必须要怎么做。因此它能支持广泛和不同的应用需求。
+ 保持强大的向后兼容。Spring 的演变过程处于严格、精心的管理控制下，尽量在不同版本中保持很小的变动。包括JDK的版本和第三方库。
+ 关注 API 设计。直观且富有前瞻性的设计，以便适用多个版本。
+ 设定了极高的代码质量标准。 Spring Framework 更在乎有意义、最新、精确的Javadoc。它是极少数能够做到代码结构干净、包引用之间没有循环依赖的项目。

## 技术栈

### Spring Framework (5.0)

#### Core
+ IoC container
+ AOP

#### Data Access
+ Transactions
+ ORM (Object Relational Mapping)

#### Web
![MVC vs WebFlux](pictures/mvc-andwebflux.png)
+ Spring MVC
  - DispatcherServlet
  - Filters
  - Asynchronous Requests

+ Spring WebFlux
  - Functional Endpoints
  - WebClient

### Spring Boot (2.1)
+ SpringApplication
+ Externalized Configuration
+ Caching
+ Distributed Transactions with JTA (Java Transaction API)
+ Creating Your Own Auto-configuration
+ Actuator (Securing,Configuring,Health)
+ Metrics (Supported monitoring systems: Elastic,Prometheus)

### Spring Cloud (Edgware SR4)
+ Spring Cloud OpenFeign
+ Spring Cloud Sleuth
+ Spring Cloud Consul
+ Spring Cloud Config
+ Spring Cloud Netflix (Eureka,Hystrix,Zuul,Archaius)
