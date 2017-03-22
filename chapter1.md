# Part II. Spring Framework 4.x新特性
<br/>
## 3. Spring Framework 4.0中的新特性和增强功能
<br/>
 spring框架首次发布时在2004年；自从那以后已经出现了显著重大修改：Spring 2.0提供XML命名空间和AspectJ的支持；Spring2.5支持注解驱动配置；Spring3.0引入了很强大的Java5+为基础的框架代码，如基于@configuration的模型功能。

版本4.0是Spring Framework最新的主要版本并且率先全面支持Java8的功能。你依然可以在旧版本的Java下使用Spring，然而，最低的要求已经提高到了Java SE 6。我们也乘这个重大改变的机会，移除了许多过时的类和方法。

升级到[Spring4.0的迁移指南](https://github.com/spring-projects/spring-framework/wiki/Migrating-from-earlier-versions-of-the-spring-framework)可以用[Spring Framework GitHub Wiki](https://github.com/spring-projects/spring-framework/wiki)。
<br/>

## 3.1 开始体验
<br/>
新的[Spring.io](https://spring.io/)网站提供一系列的“[入门](https://spring.io/guides)”指南帮助你学习Spring。你可以阅读更多的关于指南的在[Chapter 1, Getting Started With Spring](README.md#2.2.1-核心容器)部分在这个文档。新的万展也提供全面的概述，关于很多发布在Spring下的额外项目。

如果你是一个Maven用户，你也许会对有用的[bill of materials](README.md#2.2.1-核心容器)POM文件感兴趣，发布在每个Spring框架发行版。
<br/>

## 3.2 移除过时的包和方法
<br/>
所有过时的包和许多过时的类和方法已经从Spring4中移除。如果你从之前的发布版升级Spring，你需要保证已经修复了所有使用过时的API方法。

查看完整的变化： [API差异报告](http://docs.spring.io/spring-framework/docs/3.2.4.RELEASE_to_4.0.0.RELEASE/)。

请注意，所有可选的第三方依赖都已经升级到了最低2010/2011(例如Spring4通常只支持2010年的最新或者现在的最新发布版本):尤其是 Hibernate 3.6+、EhCache 2.1+、Quartz 1.8+、Groovy 1.8+、和Joda-Time 2.0+。但是有一个例外，Spring4依赖最近的Hibernate Validator 4.3+，现在对Jackson的支持集中在2.0+版本 (Spring3.2支持的Jackson 1.8/1.9，现在已经过时）。
<br/>

## 