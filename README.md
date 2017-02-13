****# Part I. Spring框架概述
<br/>
Spring框架是一个轻量级和一个一站式的解决方案，以构建您的企业就应用程序。然而，Spring是模块化的，允许您只使用那些您需要的部分，而不必使用其余的部分。你可以在任何web框架上使用IoC容器，也可以只使用Hibernate集成代码或JDBC抽象层。Spring框架支持声明式事务管理，通过RMI或Web服务的远程访问你的应用程序的逻辑，并且支持多种持久化数据的方式。它提供了一个功能齐全的MVC框架，并且能够透明地集成AOP到您的软件实现。

Spring被设计成非侵入性的，这意味着你的逻辑代码通常情况下不依赖于框架本身。在您的集成层（如数据访问层），将会存在一些数据访问技术的依赖和Spring的库。不管怎样，从你其余的代码中分离这些依赖应该是很容易的。

本文档是Spring框架功能的参考指南。如果您对该文档有任何请求、评论或问题，请将其张贴在用户邮件列表上。对框架本身的问题应该问在StackOverflow (see https://spring.io/questions)。
<br/>

## 1. 开始使用Spring
<br/>
本参考指南提供有关Spring框架的详细信息。它提供了所有功能的全面文档，以及Spring提供的基本概念（如“依赖注入”）的一些背景。

如果您刚开始使用Spring，您也许应该通过创建Spring Boot应用程序开始使用Spring框架。Spring Boot提供了一个快速（和武断的）的方法来创建用于生产环境的基于Spring的应用。它是基于Spring框架的，支持约定大于配置，被设计为可以快速启动并且尽可能快的运行起来。

你可以使用[start.spring.io](http://start.spring.io/)生成一个基本的项目或遵循“[Getting Started](https://spring.io/guides)”指南中的一个，例如[指导构建一个RESTful 风格的Web服务](https://spring.io/guides/gs/rest-service/)指南。除了容易理解吸收之外，这些指南主要是基于任务的，它们中的大多数是基于Spring Boot的。它们也包含了Spring的其它工程，当解决一个特定问题时你可能会考虑它们。
<br/>

## 2. Spring框架介绍
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

## 2.1 依赖注入与控制反转
<br/>
Java应用——一个不精确的术语，既可以表示受限制的嵌入式应用又可以表示N层服务端的企业级应用——通常由许多对象构成，这些对象协作形成完整的应用程序。因此一个应用程序中的对象是相互依赖的。

尽管Java平台提供了丰富的应用开发功能，但是它缺少把这些基本构建模块组织成一个连贯整体的方法，并把组织基本构建模块的任务留给了架构师和开发者。虽然你可以使用设计模式例如工厂模式、抽象工厂模式、生成器模式、装饰模式、服务定位模式来创建构成应用的各种类和对象实例，但这些设计模式很简单：命名的最佳方法、模式的作用描述、应用模式的位置、模式解决的问题等等。模式使最佳实践形式化了，这意味着你必须在你的应用中自己实现它。

Spring框架中的控制反转(IoC)组件通过提供一种形式化方法解决了这个问题，这个形式化方法将不同的组件创建到一个随时可用的完整的工作应用中。Spring框架将形式化的设计模式编码成了你可以集成到你自己的应用中的最好对象。许多组织和机构用这种方式应用Spring框架来构建鲁棒的、可维护的应用。

>    
****背景**** 
“问题是什么是控制反转？” 2004年Martin Fowler在他的网站上提出了这个关于控制反转(IoC)问题。Fowler建议重新命名这个原理使它更一目了然并且提出了依赖注入。

<br/>

## 2.2 