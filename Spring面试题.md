# Spring面试题

#### 介绍一下Spring
- spring目的是用于简化企业应用程序的开发，它使得开发者只需要关心业务需求，是一个轻量级的ioc和aop的容器框架。
- 常见的配置方式有三种：**基于XML的配置、基于注解的配置、基于Java的配置**。
- 主要由以下几个模块组成：<br>
Spring Core：核心类库，提供IOC服务；<br>
Spring Context：提供框架式的Bean访问方式，以及企业级功能（JNDI、定时任务等）；<br>
Spring AOP：AOP服务；<br>
Spring DAO：对JDBC的抽象，简化了数据访问异常的处理；<br>
Spring ORM：对现有的ORM框架的支持；<br>
Spring Web：提供了基本的面向Web的综合特性，例如多方文件上传；<br>
Spring MVC：提供面向Web应用的Model-View-Controller实现。

#### Spring 的优点？
（1）spring属于低侵入式设计，代码的污染极低；<br>
（2）spring的DI机制将对象之间的依赖关系交由框架处理，减低组件的耦合性；<br>
（3）Spring提供了AOP技术，支持将一些通用任务，如安全、事务、日志、权限等进行集中式管理，从而提供更好的复用。<br>
（4）spring对于主流的应用框架提供了集成支持。<br>

## IOC控制反转

#### 解释一下IOC
- IOC是控制反转，我们以往创建对象使用new的形式来创建，现在将创建对象的权利交给spring容器类实现，需要使用的时候再进行依赖注入，目的是为了**解耦**。

## AOP面向切面编程

#### 解释一下AOP
- AOP是面向切面编程，AOP技术将那些与核心业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块间的耦合度，如**记录日志、事务管理、权限验证**等。

## DI依赖注入

#### 解释一下DI
- DI是依赖注入（DI,DependencyInjection），也叫控制反转（IoC,inversion of control）是Spring框架的核心机制。Spring通过DI实现IOC。

#### Spring中常用的注入方式
- 常用的注入方式有三种 ： **构造器注入、setter注入、基于注解注入**。

## Spring Bean

#### 解释一下Spirng Bean
- Spring Bean ：是基于用户提供的配置创建的，构成了应用程序主干的对象，由 Spring IoC 容器实例化、装配和管理。

#### Bean的作用域（scope）
- **Singleton** - 每个 Spring IoC 容器仅有一个单实例。
- **Prototype** - 每次请求都会产生一个新的实例。
- **Request** - 每次请求都会创建一个实例。
- **Session** - 在一个会话周期内只有一个实例。
- Global-session - 类似于标准的 HTTP Session 作用域，5.0版本后已不再使用。
- **Appilcation** - 在一个 ServletContext 中只有一个实例。
- **Websocket** - 在一个 Websocket 只有一个实例。

#### Bean的生命周期
- **（1）实例化Bean** <br>
 对于BeanFactory容器，当客户向容器请求一个尚未初始化的bean时，或初始化bean的时候需要注入另一个尚未初始化的依赖时，容器就会调用createBean进行实例化。对于ApplicationContext容器，当容器启动结束后，通过获取BeanDefinition对象中的信息，实例化所有的bean。
- **（2）设置对象属性（依赖注入）** <br>
  实例化后的对象被封装在BeanWrapper对象中，紧接着，Spring根据BeanDefinition中的信息 以及 通过BeanWrapper提供的设置属性的接口完成依赖注入。
- **（3）处理Aware接口**   <br>
接着，Spring会检测该对象是否实现了xxxAware接口，并将相关的xxxAware实例注入给Bean：    <br>
①如果这个Bean已经实现了BeanNameAware接口，会调用它实现的setBeanName(String beanId)方法，此处传递的就是Spring配置文件中Bean的id值；<br>
②如果这个Bean已经实现了BeanFactoryAware接口，会调用它实现的setBeanFactory()方法，传递的是Spring工厂自身。  <br>
③如果这个Bean已经实现了ApplicationContextAware接口，会调用setApplicationContext(ApplicationContext)方法，传入Spring上下文；
- **（4）BeanPostProcessor** <br>
如果想对Bean进行一些自定义的处理，那么可以让Bean实现了BeanPostProcessor接口，那将会调用postProcessBeforeInitialization(Object obj, String s)方法。
- **（5）InitializingBean 与 init-method** <br>
如果Bean在Spring配置文件中配置了 init-method 属性，则会自动调用其配置的初始化方法。
-（6）如果这个Bean实现了BeanPostProcessor接口，将会调用postProcessAfterInitialization(Object obj, String s)方法；由于这个方法是在Bean初始化结束时调用的，所以可以被应用于内存或缓存技术；
- #### 以上几个步骤完成后，Bean就已经被正确创建了，之后就可以使用这个Bean了。
- **（7）DisposableBean** <br>
当Bean不再需要时，会经过清理阶段，如果Bean实现了DisposableBean这个接口，会调用其实现的destroy()方法；
- **（8）destroy-method** <br>
最后，如果这个Bean的Spring配置中配置了destroy-method属性，会自动调用其配置的销毁方法。
