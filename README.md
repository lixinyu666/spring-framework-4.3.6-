


#Part I. Spring框架概述
<br/>
Spring框架是一个轻量级和一个一站式的解决方案，以构建您的企业就应用程序。然而，Spring是模块化的，允许您只使用那些您需要的部分，而不必使用其余的部分。你可以在任何web框架上使用IoC容器，也可以只使用Hibernate集成代码或JDBC抽象层。Spring框架支持声明式事务管理，通过RMI或Web服务的远程访问你的应用程序的逻辑，并且支持多种持久化数据的方式。它提供了一个功能齐全的MVC框架，并且能够透明地集成AOP到您的软件实现。

Spring被设计成非侵入性的，这意味着你的逻辑代码通常情况下不依赖于框架本身。在您的集成层（如数据访问层），将会存在一些数据访问技术的依赖和Spring的库。不管怎样，从你其余的代码中分离这些依赖应该是很容易的。

本文档是Spring框架功能的参考指南。如果您对该文档有任何请求、评论或问题，请将其张贴在用户邮件列表上。对框架本身的问题应该问在StackOverflow (see https://spring.io/questions)。
<br/>

##1. 开始使用Spring
<br/>
本参考指南提供有关Spring框架的详细信息。它提供了所有功能的全面文档，以及Spring提供的基本概念（如“依赖注入”）的一些背景。

如果您刚开始使用Spring，您也许应该通过创建Spring Boot应用程序开始使用Spring框架。Spring Boot提供了一个快速（和武断的）的方法来创建用于生产环境的基于Spring的应用。它是基于Spring框架的，支持约定大于配置，被设计为可以快速启动并且尽可能快的运行起来。

你可以使用[start.spring.io](http://start.spring.io/)生成一个基本的项目或遵循“[Getting Started](https://spring.io/guides)”指南中的一个，例如[指导构建一个RESTful 风格的Web服务](https://spring.io/guides/gs/rest-service/)指南。除了容易理解吸收之外，这些指南主要是基于任务的，它们中的大多数是基于Spring Boot的。它们也包含了Spring的其它工程，当解决一个特定问题时你可能会考虑它们。
<br/>

##2. Spring框架介绍
<br/>
Spring框架是一个为开发java应用的综合基础架构提供支持的java平台。Spring处理基础架构，以便您可以专注于应用程序。

Spring使你能创建“普通java对象构建应用程序”(POJOs)并能非侵入式的将企业服务应用到普通Java对象(POJOs)上。
此功能完全适用于Java SE项目模型，部分适用于java EE。

作为应用程序开发人员，您可以从Spring平台获益的例子：

* 在一个数据库事务中执行一个Java方法而不必处理事务APIs 
* 使一个本地的Java方法可以远程调用而不必处理远程APIs 
* 使一个本地Java方法变为管理操作而不必处理JMX APIs 
* 使一个本地Java方法变为消息处理器而不必处理JMS APIs
<br/>

##2.1 依赖注入与控制反转
<br/>
Java应用——一个不精确的术语，既可以表示受限制的嵌入式应用又可以表示N层服务端的企业级应用——通常由许多对象构成，这些对象协作形成完整的应用程序。因此一个应用程序中的对象是相互依赖的。

尽管Java平台提供了丰富的应用开发功能，但是它缺少把这些基本构建模块组织成一个连贯整体的方法，并把组织基本构建模块的任务留给了架构师和开发者。虽然你可以使用设计模式例如工厂模式、抽象工厂模式、生成器模式、装饰模式、服务定位模式来创建构成应用的各种类和对象实例，但这些设计模式很简单：命名的最佳方法、模式的作用描述、应用模式的位置、模式解决的问题等等。模式使最佳实践形式化了，这意味着你必须在你的应用中自己实现它。

Spring框架中的控制反转(IoC)组件通过提供一种形式化方法解决了这个问题，这个形式化方法将不同的组件创建到一个随时可用的完整的工作应用中。Spring框架将形式化的设计模式编码成了你可以集成到你自己的应用中的最好对象。许多组织和机构用这种方式应用Spring框架来构建鲁棒的、可维护的应用。

>    
`背景`
“问题是什么是控制反转？” 2004年Martin Fowler在他的网站上提出了这个关于控制反转(IoC)问题。Fowler建议重新命名这个原理使它更一目了然并且提出了依赖注入。

<br/>

##2.2 模块
<br/>
Spring框架包含的功能大约由20个模块组成。这些模块按组可分为核心容器、数据访问/集成，Web，AOP(面向切面编程)、设备、消息和测试，如下图所示。
<br/>
**Spring框架概述**

![Spring框架概述](/assets/spring-overview.png)

接下来的章节列出了每个功能可用的模块、它们的工件名字以及它们包含的主题。工件名字与[依赖管理工具](#2.2.1-核心容器)中使用的artifact IDs有关。
<br/>

###2.2.1 核心容器

[核心容器](README.md#2.2.1-核心容器)功能包括`spring-core`, `spring-beans`, `spring-context`, `spring-context-support`, 和 `spring-expression(Spring表现语言)`模块。

`spring-core`和`spring-beans`模块[提供了框架的基础结构部分](README.md#2.2.1-核心容器)，包含控制反转(IoC)和依赖注入(DI)功能。BeanFactory是工厂模式的高级实现。它去掉了程序单例模式的需求并且允许你从实际的程序逻辑中解耦配置和依赖关系。

上下文(`spring-context`)模块建立在由[Core模块和Beans模块](README.md#2.2.1-核心容器)提供的坚实基础上：它是在类似于JNDI注册表式的框架风格模式中访问对象的一种方法。上下文模块继承了Beans模块的功能，并添加了对国际化（例如使用资源捆绑）、事件传播、资源加载和上下文透明创建（例如通过Servlet容器）的支持。上下文模块也支持Java EE功能例如EJB，JMX和基本的远程。`ApplicationContext`接口是上下文模块的焦点。`spring-context-support`支持将缓存(EhCache, Guava, JCache), 邮件(JavaMail),调度(CommonJ, Quartz)和模板引擎(FreeMarker, JasperReports, Velocity)等第三方库集成进Spring应用程序上下文中。

`spring-expression`模块提供了强大的[表达式语言](README.md#2.2.1-核心容器)用来在运行时查询和操作对象图。它是JSP 2.1规范中统一表达式语言(unified EL)的扩展。这个语言支持setting和getting属性值，属性分配，方法调用，访问数组、集合和索引器的内容，逻辑和算术操作，变量命名，从Spring Ioc容器中通过名字检索对象。它也支持它还支持列表投影、选择以及常见的列表聚合。
<br/>

###2.2.2 AOP和仪器

`spring-aop`模块提供了[AOP](README.md#2.2.1-核心容器) Alliance-compliant(AOP联盟)面向切面编程的实现，例如允许你自定义方法拦截器和切入点来清晰的解耦功能实现上应该分开的代码。使用源码级的元数据功能，你也可以将行为信息合并到你的代码中，在某种程度上这类似于.NET的属性值。

独立的`spring-aspects`模块提供了与AspectJ的集成。

`spring-instrument`模块提供了类设备支持和类加载器的实现，它们可以在某些应用服务器中使用。`spring-instrument-tomcat`模块包含了Tomcat的Spring设备代理。
<br/>
###2.2.3 信息

Spring 4框架中包含了`spring-messaging`模块，它对Spring集成项目例如`Message`, `MessageChannel`, `MessageHandler`和其它作为消息应用服务基础的项目进行了重要的抽象。这个模块也包含了一系列将消息映射到方法上的注解，这个注解与基于编程模型Spring MVC注解类似。
<br/>

###2.2.4 数据访问/集成

数据访问/集成层包括JDBC,ORM,OXM,JMS和业务模块。

`spring-jdbc`模块提供了[JDBC](#README.md#2.2.1-核心容器)抽象层，不需要再编写单调的JDBC代码，解析数据库提供商指定的错误编码。

`spring-tx`模块为实现指定接口和所有的普通Java对象(POJOs)的类提供[编程式(programmatic)和声明式(declarative)的业务管理](#README.md#2.2.1-核心容器)。

`spring-orm`模块提供流行的[对象关系映射](#README.md#2.2.1-核心容器)APIs的集成层，包括[JPA](#README.md#2.2.1-核心容器), [JDO](#README.md#2.2.1-核心容器)和[Hibernate](#README.md#2.2.1-核心容器)。在使用`spring-orm`模块时，你可以将Spring的其它功能与这些O/R-mapping框架结合起来使用，例如前面提到的简单声明式业务管理的功能。

`spring-oxm`模块提供对[Object/XML映射](#README.md#2.2.1-核心容器)实现例如JAXB，Castor，XMLBeans, JiBx和XStream的抽象层。

`spring-jms`模块（[Java消息服务](#README.md#2.2.1-核心容器)）包含产生和处理消息的功能。从Spring 4.1框架开始它提供了与`spring-messaging`的集成。
<br/>

###2.2.5 Web

网络层包含`spring-web`, `spring-webmvc`, `spring-websocket`和`spring-webmvc-portlet`模块。

`spring-web`模块提供基本的面向网络集成功能，例如multipart文件上传功能，使用Servlet监听器来初始化Ioc容器和面向网络的应用程序上下文。它也包含了HTTP客户端和Spring远程支持中网络相关的部分。

`spring-webmvc`模块（也被称为Web-Servlet模块）包含了Spring的model-view-controller([MVC](#README.md#2.2.1-核心容器))和REST Web Services的网络应用实现。Spring的MVC框架提供了对领域模型代码，web表单，Spring框架其他功能的完全分离。

`spring-webmvc-portlet`组件（也称为Web-Portlet模块）提供的MVC实现，用于portlet环境和镜子的春天webmvc模块的功能。