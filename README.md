# Part I. Spring框架概述
<br/>
Spring框架是一个轻量级和一个一站式的解决方案，以构建您的企业就应用程序。然而，Spring是模块化的，允许您只使用那些您需要的部分，而不必使用其余的部分。你可以只使用IOC容器，搭配任何的Web框架，但，你只能用Hibernate集成代码或者JDBC抽象层。Spring框架支持声明式事务管理，通过RMI或Web服务的远程访问你的应用程序的逻辑，并得到你期望的各种选项的数据。它提供了一个功能齐全的MVC框架，并且能够透明地集成AOP到您的软件实现。
<br/>
Spring被设计成非侵入性的，这意味着你的逻辑代码通常对框架本身没有依赖性。在您的集成层（如数据访问层），一些依赖于数据访问技术和Spring库将存在。但是，应该很容易从代码库的其余部分隔离这些依赖项。本文档是Spring框架功能的参考指南。如果您对该文档有任何请求、评论或问题，请将其张贴在用户邮件列表上。对框架本身的问题应该问在StackOverflow (see https://spring.io/questions)。
<br/>

## 1. 开始使用Spring
<br/>
本参考指南提供有关Spring框架的详细信息。它提供了所有功能的全面文档，以及Spring提供的基本概念（如“依赖注入”）的一些背景。如果您刚开始使用Spring，您也许应该通过创建Spring Boot应用程序开始使用Spring框架。Spring Boot提供了一个快速（固定）的方法来创建一个准备生产的基于Spring的应用。它是基于Spring框架，该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置，并旨在让你和运行尽可能快。
<br/>

你可以使用[start.spring.io](http://start.spring.io/)生成一个基本的项目或遵循“[Getting Started](https://spring.io/guides)”来[指导构建一个RESTful 风格的Web服务](https://spring.io/guides/gs/rest-service/)。这些指导不仅容易理解，而且对Spring Boot的介绍十分精准，而且大部分都是基于Spring Boot的。他们还涵盖了其他Spring机构项目，可能解决你在考虑的一个特定问题。