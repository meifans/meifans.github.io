## bean

### Spring Ioc容器

+ 什么是Ioc

依赖注入（Dependency Injection），即把某个对象依赖的所有对象注入进去，相比于在对象内直接显式的new出来，把创建依赖对象的权利反转，交给了容器，所以也叫控制反转（Inverse of Control）。

`优势`： 可以根据配置或环境自由决定注入对象的具体类型,增加灵活性。避免了硬编码方便mock，测试方便。

+ bean 生命周期

1. 寻找bean的BeanDefinition（xml方式或注解Java对象方式），并实例化bean
  > 提供元数据的三种方式
    1. Xml配置文件
    2. 基于注解的配置
    3. 基于Java的配置

2. 对bean进行依赖注入。

3. 注入实现各种Aware。
  + BeanNameAware        注入bean的名字
  + BeanClassLoaderAware 注入bean的classloader
  + BeanFactoryAware     注入bean所在的factory

4. BeanPostProcessor 的before方法 -> InitializingBean.afterPropertiesSet()（bean的初始化方法） -> BeanPostProcessor 的after方法

5. DisposableBean.destory 释放资源 ？ -> destory (指定的bean销毁方法)

+ bean 类型
  + singleton 单例（默认）
  + prototype 原型 每个bean都是新的
  + request：每次http请求都会创建一个bean，该作用域仅在基于web的Spring ApplicationContext情形下有效。
  + session：在一个HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring   + ApplicationContext情形下有效。
  + global-session：在一个全局的HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。

+ ApplicationContext 相比 BeanFactory的优势
  + 支持多于一种配置（不止xml文件）
  + 支持bean注册观察者，publish event
  + I18n ...and so on

+ 自动装配

  + no：
    这是Spring框架的默认设置，在该设置下自动装配是关闭的，开发者需要自行在bean定义中用标签明确的设置依赖关系。

  + byName：
    该选项可以根据bean名称设置依赖关系。当向一个bean中自动装配一个属性时，容器将根据bean的名称自动在在配置文件中查询一个匹配的bean。如果找到的话，就装配这个属性，如果没找到的话就报错。

  + byType：
    该选项可以根据bean类型设置依赖关系。当向一个bean中自动装配一个属性时，容器将根据bean的类型自动在在配置文件中查询一个匹配的bean。如果找到的话，就装配这个属性，如果没找到的话就报错。

  + constructor：
    造器的自动装配和byType模式类似，但是仅仅适用于与有构造器相同参数的bean，如果在容器中没有找到与构造器参数类型一致的bean，那么将会抛出异常。

  + autodetect：
    该模式自动探测使用构造器自动装配或者byType自动装配。首先，首先会尝试找合适的带参数的构造器，如果找到的话就是用构造器自动装配，如果在bean内部没有找到相应的构造器或者是无参构造器，容器就会自动选择byTpe的自动装配方式。

+ 常见的ApplicationContext 的实现方式
  1. ClassPathXmlApplicationContext：从classpath的XML配置文件中读取上下文，并生成上下文定义。应用程序上下文从程序环境变量中取得。

         ApplicationContext context = new ClassPathXmlApplicationContext(“bean.xml”);

  2. FileSystemXmlApplicationContext ：由文件系统中的XML配置文件读取上下文。

         ApplicationContext context = new FileSystemXmlApplicationContext(“bean.xml”);

  3. XmlWebApplicationContext：由Web应用的XML文件读取上下文。

+ ApplicationContext中的事件类型

  一个bean实现了ApplicationListener接口，当一个ApplicationEvent 被发布以后，bean会自动被通知。

  1. 上下文更新事件（ContextRefreshedEvent）：该事件会在ApplicationContext被初始化或者更新时发布。也可以在调用ConfigurableApplicationContext 接口中的refresh()方法时被触发。

  2. 上下文开始事件（ContextStartedEvent）：当容器调用ConfigurableApplicationContext的Start()方法开始/重新开始容器时触发该事件。

  3. 上下文停止事件（ContextStoppedEvent）：当容器调用ConfigurableApplicationContext的Stop()方法停止容器时触发该事件。

  4. 上下文关闭事件（ContextClosedEvent）：当ApplicationContext被关闭时触发该事件。容器被关闭时，其管理的所有单例Bean都被销毁。

  5. 请求处理事件（RequestHandledEvent）：在Web应用中，当一个http请求（request）结束触发该事件。

  6. 自定义事件 ： customEvent 继承 ApplicationEvent,customListener实现ApplicationListener接口。 

+ spring 常用模块
  + The Core container module

    >提供 Spring 框架的基本功能。核心容器的主要组件是BeanFactory，它是工厂模式的实现。BeanFactory 使用控制反转 （IOC） 模式将应用程序的配置和依赖性规范与实际的应用程序代码分开。

  + Application context module

    >Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。Spring 上下文包括企业服务，例如 JNDI、EJB、电子邮件、国际化、校验和调度功能。

  + AOP module (Aspect Oriented Programming)
  + JDBC abstraction and DAO module

    >JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次结构。

  + O/R mapping integration module (Object/Relational)

    >Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。

  + Web module

    >Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。

  + MVC framework module

    >MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。通过策略接口，MVC 框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。

### Spring 事务管理

+  类型 ：声明式事务管理、编程式事务管理。
+ Advice类型：
