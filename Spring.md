# Spring

## IOC
- inversion of control
    -  IoC enables a framework to take control of the flow of a program and make calls to our custom code
    -  maintains the life cycle of the objects.
    -  not spring unique
    -  We can **achieve** Inversion of Control through various mechanisms such as: Strategy design pattern, Service Locator pattern, Factory pattern, and Dependency Injection (DI).
#### advatage
- make the code loosely coupled

### DI
- Dependency injection
    - Dependency injection is a pattern we can use to implement IoC, where the control being inverted is **setting an object's dependencies**.
    - “injecting” objects into other objects, is done by an assembler rather than by the objects themselves.
### Spring IoC Container
- ApplicationContext
    - In the Spring framework, the interface ApplicationContext represents the IoC container. 
    - The Spring container is responsible for instantiating, configuring and assembling objects known as beans, as well as managing their life cycles.
    - The Spring framework provides several implementations of the ApplicationContext interface: WebApplicationContext for web applications.
    - In order to assemble beans, the container uses configuration metadata, which can be in the form of XML configuration or annotations. (applicationContext.xml)
- BeanFactory vs ApplicationContext
    - BeanFactory is lightweight, for bean instantiation/wiring
    - Application Context
        - Bean instantiation/wiring
        - Automatic BeanPostProcessor registration
        - Automatic BeanFactoryPostProcessor registration
        - Convenient MessageSource access (for i18n)
        - ApplicationEvent publication
    - ![](https://i.stack.imgur.com/EweA3.jpg) 
- scope of spring bean
    - singleton (default) | so the objects could be reused
    - prototype | every time create a new object
    - request | every time send a request, create a new object
    - session
    - global session

### Dependency Injection in Spring
- Injection type
    - field | clean, not easy for testing
    - constructor | recommmend 
    - setter
- four modes of autowiring a bean 
    - no: the default value – this means no autowiring is used for the bean and we have to explicitly name the dependencies.
    - byName: autowiring is done based on the name of the property, therefore Spring will look for a bean with the same name as the property that needs to be set.
    - byType: similar to the byName autowiring, only based on the type of the property. This means Spring will look for a bean with the same type of the property to set. If there's more than one bean of that type, the framework throws an exception.
    - constructor: autowiring is done based on constructor arguments, meaning Spring will look for beans with the same type as the constructor arguments.
- @Primary and @Qualifier
    - If there's more than one bean of the same type, we can use the @Qualifier annotation to reference a bean by name
    - So you can find both @Qualifier and @Primary are telling Spring to use the specific bean when multiple candidates are qualified to autowire. But @Qualifier is more specific and has high priority. So when both @Qualifier and @Primary are found, @Primary will be ignored.

## AOP
- Aspect-oriented programming 
    - add additional behavior to existing code,
    - execute extra methods during the invocation of specific methods
    - solution for cross-cutting concerns
        - Cross-cutting concerns such as Security, Cache, Transaction Management, Logging, Audit, Exception handling, Timer, Retry and Validation.
- uses Proxy design pattern
- not easy to read
### terms
#### Aspect
An aspect is a modularization of a concern that cuts across multiple classes. 

The combination of the pointcut and the advice.
#### Joinpoint
A Joinpoint is a point during the execution of a program, such as the execution of a method or the handling of an exception.

PointCut defines many methods, this is the one among them during runtime
#### Pointcut
A Pointcut is a predicate that helps match an Advice to be applied by an Aspect at a particular JoinPoint.
- A pointcut expression starts with a pointcut designator (PCD), which is a keyword telling Spring AOP what to match. 
    - Using method signature
        - execution(primary)
            - `@Pointcut("execution(* com.baeldung.pointcutadvice.dao.FooDao.*(..))")` using wildcards
        - within
            - `@Pointcut("within(com.baeldung.pointcutadvice.dao.FooDao)")`
        - this and target
            - this limits matching to join points where the bean reference is an instance of the given type
            - target limits matching to join points where the target object is an instance of the given type.
            - The former works when Spring AOP creates a CGLIB-based proxy, and the latter is used when a JDK-based proxy is created.
    - Using annotation
        - This PCD limits matching to join points where the subject of the join point has the given annotation. For example we may create a @Loggable annotation:`@Pointcut("@annotation(com.baeldung.pointcutadvice.annotations.Loggable)")
public void loggableMethods() {}`

We often associate the Advice with a Pointcut expression, and it runs at any Joinpoint matched by the Pointcut.

#### Advice
An Advice is an action taken by an aspect at a particular Joinpoint. 
- Before, Around, After, AfterThrowing, AfterReturning

## Spring vs. Spring Boot vs. Spring MVC
### Spring vs. Spring Boot
- Spring: Spring Framework is the most popular application development framework of Java. The main feature of the Spring Framework is dependency Injection or Inversion of Control (IoC). With the help of Spring Framework, we can develop a loosely coupled application. It is better to use if application type or characteristics are **purely defined**.
- Spring Boot: Spring Boot is a module of Spring Framework. It allows us to build a stand-alone application with minimal or zero configurations. It is better to use if we want to develop a **simple** Spring-based application or RESTful services.

| Spring | Spring Boot |
| --- | --- |
| Spring Framework is a widely used Java EE framework for building applications. | Spring Boot Framework is widely used to develop REST APIs. |
| It aims to simplify Java EE development that makes developers more productive. | It aims to shorten the code length and provide the easiest way to develop Web Applications. |
| The primary feature of the Spring Framework is dependency injection. | The primary feature of Spring Boot is Autoconfiguration. It automatically configures the classes based on the requirement. |
| It helps to make things simpler by allowing us to develop loosely coupled applications. | It helps to create a stand-alone application with less configuration. |
| The developer writes a lot of code (boilerplate code) to do the minimal task. | It reduces boilerplate code. |
| To test the Spring project, we need to set up the sever explicitly. | Spring Boot offers embedded server such as Jetty and Tomcat, etc. |
| It does not provide support for an in-memory database. | It offers several plugins for working with an embedded and in-memory database such as H2. |
| Developers manually define dependencies for the Spring project in pom.xml. | Spring Boot comes with the concept of starter in pom.xml file that internally takes care of downloading the dependencies JARs based on Spring Boot Requirement. |

### Spring Boot vs. Spring MVC
- Spring MVC: Spring MVC is a Web MVC Framework for building web applications. It contains a lot of configuration files for various capabilities. It is an HTTP oriented web application development framework.

 









    