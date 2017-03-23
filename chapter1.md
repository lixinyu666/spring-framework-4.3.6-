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

## 3.3 Java 8 (以及6和7)
<br/>
Spring4支持Java8的一些特性。你可以在Spring的回调接口中使用lambda表达式和方法引用。支持`java.time`([JSR-310](https://jcp.org/en/jsr/detail?id=310))的值类型和一些改进过的注解，例如`@Repeatable`。你还可以使用Java8的参数名称发现机制（基于`-parameters`编译器标志）。

Spring仍然兼容老版本的Java和JDK：Java SE 6（具体来说，支持JDK6 update 18）以上版本，我们建议新的基于Spring4的项目使用Java7或Java8。
<br/>

## 3.4 Java EE 6 and 7
<br/>
Java EE 6 或以上版本是Spring4的底线,与JPA2.0和Servlet3.0规范有着特殊的意义。为了保持与Google App Engine和旧的应用程序服务器兼容,Spring4可以部署在Servlet2.5运行环境。但是我们强烈的建议您在Spring测试和模拟测试的开发环境中使用Servlet3.0+。

![java](/assets/note1.png) | 如果你是WebSphere 7的用户，一定要安装JPA2.0功能包。在WebLogic 10.3.4或更高版本，安装附带的JPA2.0补丁。这样就可以将这两种服务器变成Spring4兼容的部署环境。

从长远的观点来看，Spring4.0现在支持Java EE 7级别的适用性规范：尤其是JMS 2.0, JTA 1.2, JPA 2.1, Bean Validation 1.1 和JSR-236并发工具类。像往常一样，支持的重点是独立的使用这些规范。例如在Tomcat或者独立环境中。但是，当把Spring应用部署到Java EE 7服务器时它同样适用。

注意，Hibernate 4.3是JPA 2.1的提供者，因此它只支持Spring4。同样适用用于作为Bean Validation 1.1提供者的Hibernate Validator 5.0。这两个都不支持Spring3.2。
<br/>

## 3.5 Groovy DSL定义Bean
<br/>
Spring4.0支持使用Groovy DSL来进行外部的bean定义配置。这在概念上类似于使用XML的bean定义，但是支持更简洁的语法。使用Groovy还允许您轻松地将bean定义直接嵌入到引导代码中。例如：

```
def reader = new GroovyBeanDefinitionReader(myApplicationContext)
reader.beans {
    dataSource(BasicDataSource) {
        driverClassName = "org.hsqldb.jdbcDriver"
        url = "jdbc:hsqldb:mem:grailsDB"
        username = "sa"
        password = ""
        settings = [mynew:"setting"]
    }
    sessionFactory(SessionFactory) {
        dataSource = dataSource
    }
    myService(MyService) {
        nestedBean = { AnotherBean bean ->
            dataSource = dataSource
        }
    }
}
```

有关更多信息，请参阅`GroovyBeanDefinitionReader` [javadocs](http://docs.spring.io/spring-framework/docs/4.3.7.RELEASE/javadoc-api/org/springframework/beans/factory/groovy/GroovyBeanDefinitionReader.html)。
<br/>

## 3.6 核心容器改进
<br/>
有几种对核心容器的常规改进：
* Spring现在注入Bean的时候把[泛型类型当成一种形式的限定符](README.md#2.2.1-核心容器)。例如：如果你使用Spring Data `Repository`你可以方便的插入特定的实现：`@Autowired Repository<Customer> customerRepository`。
* 如果你使用Spring的元注解支持，你现在可以开发自定义注解来[公开源注解的特定属性](README.md#2.2.1-核心容器)。
* 当[自动装配到lists和arrays](README.md#2.2.1-核心容器)时，Beans现在可以被排序了。支持`@Order`注解和`Ordered`接口两种方式。
* `@Lazy`注解现在可以用在注入点以及`@Bean`定义上。
* 引入`@Description`[注解](README.md#2.2.1-核心容器),开发人员可以使用基于Java方式的配置。
* [根据条件筛选Beans](README.md#2.2.1-核心容器)的广义模型通过`@Conditional`注解加入。这和`@Profile`支持的类似，但是允许以编程式开发用户定义的策略。
* [基于CGLIB的代理类](README.md#2.2.1-核心容器)不在需要默认的构造方法。这个支持是由[objenesis](https://github.com/easymock/objenesis)库提供。这个库重新打包到Spring框架中，作为Spring框架的一部分发布。通过这个策略，针对代理实例被调用没有构造可言了。
* 框架现在支持管理时区。例如`LocaleContext`。
<br/>

## 3.7 常规Web改进
<br/>
现在仍然可以部署到Servlet 2.5服务器，但是Spring4.0现在主要集中在Servlet 3.0+环境。如果你使用[Spring MVC测试框架](README.md#2.2.1-核心容器)，你需要将Servlet 3.0兼容的JAR包放到 测试的classpath下。

除了稍后会提到的WebSocket支持外，下面的常规改进已经加入到Spring的Web模块：

* 你可以在Spring MVC应用中使用新的`@RestController`[注解](README.md#2.2.1-核心容器)，不在需要给`@RequestMapping`的方法添加`@ResponseBody`注解。
* `AsyncRestTemplate`类已被添加进来，当开发REST客户端时，[允许非阻塞异步支持](README.md#2.2.1-核心容器)。
* 当开发Spring MVC应用时，Spring现在提供了全面的时区支持 。