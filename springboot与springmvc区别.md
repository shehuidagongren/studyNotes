# springboot与springmvc区别梳理

一.springmvc：

在早些时候，javaweb的开发中，统一把显示层，控制层，数据层的操作全部交给JSP或者javaBean处理，我们可以称之为Model1：

![img](https://img-blog.csdnimg.cn/img_convert/2a671302fe8d42e54fb112d67a517e98.png)

出现的弊端：

JSP和JavaBean之间严重耦合，Java代码和Html代码也耦合在了一起
要求开发者不仅要掌握Java，还要掌握一定的前端水准
前端和后端相互依赖，前端需要等待后端完成，后端也依赖前端完成，才能进行有效的测试
代码复用性差
正是因为上面的这些弊端，所以很快这种方式就被Servlet+JSP+JavaBean所替代了，早期的MVC模型是Model2

![img](https://img-blog.csdnimg.cn/img_convert/928806ca90b072cbb6971fe52b4a854a.png)

首先用户的请求会到达Servlet，然后根据请求调用响应的JavaBean，并把所有的显示结果交给JSP完成，这样的模式我们就成为MVC模式

M代表的模型 Model

模型就是数据，就是dao，bean

V代表的试图 View

C代表的控制器 COntroller

控制器就是把不同的数据Model显示在不同的试图View上，Servlet就是扮演这样的角色。

（后面会介绍如何搭建一个SpringMVC项目）

二.SpringBoot

springBoot就是让你的项目尽快跑起来的spring应用程序并且尽可能减少你的配置文件

设计目的：

用来简化新Spring应用的初始搭建以及开发过程

从最根本上来说，SpringBoot就是一些库的集合，他能够被人以项目的构建系统所使用，他使用习惯由于配置（项目中存在大量的配置，西外还内置一个习惯性的配置）的理念，让你的向项目快速运行起来，用大佬的话理解，就是SpringBoot其实不是什么新的框架，他默认配置了很多框架的使用方式，就想maven整合了所有的jar包，springboot整合所有框架，总结一下及几点：

为所有Spring开发提供了一个更快广泛的入门体验
零配置，无冗余代码生成和xml强制配置，遵循约定大于配置
集成了大量常用的第三方库的配置，Springboot医用未这些第三方库提供了几乎可以零配置的开箱即用的能力
提供一系列大型项目常用的非功能性特征，嵌入式服务器，安全性，度量，运行状况检查，外部化配置等
SpringBoot不是Spring替代者，Spring框架是通过IOC机制来管理Bean的，SpringBoot依赖Spring框架来管理对象的依赖，Springboot并不是Spring的精简版本，而是使用Spring做好各种产品级准备
SpringBoot在应用中的角色

springBoot是基于SpringFramework来构建的，SpringFramework是一种J2EE的框架

SpringBoot是一种快速搭建Spring应用

SrpingCloud是构建SpringBoot分布式环境，也就是常说的云应用

SpringBoot中流砥柱，承上启下



三.SpringMvc与SpringBoot区别

springBoot只是一个配置工具，整合工具，辅助工具
springmvc是框架，项目中实际运行的代码
Spring框架就像一个大家族，有众多衍生出的产品例如Boot，security，jpa等等，但他们的基础都是SpringIOC和AOP，ioc提供依赖注入的容器，aop解决了面向横切面的编程，然后再次两者的基础上实现了其他延伸产品的高级功能
SpringMVC提供了一种轻度耦合的方式来开发web应用，他是Spring中的一个模块，是一个Web框架，通过DispatcherServlet，ModelAndView，和ViewResolver，开发Web应用变得很容易
SpringBoot实现了自动配置，降低了项目的搭建难度
对使用者来说，换用SpringBoot以后，项目的初始方法变了，配置文件变了。另外就是不需要单独安装Tomcat这类容器服务器，maven打出jar包直接拍起来就是个网站，但是你最核心的业务逻辑实现与业务流程实现没有任何变化。
总结：

Spring最初利用“工程模式”（DI）和“代理模式”（AOP）解耦应用组件，大家觉得挺好用，于是按照这种模式搞了一个MVC框架（一些Spring的解耦组件），用于开发Web应用（SpringMVC）,然后发现每次开发都写了很多样板代码，为了简化工作流程，于是开发出了一些懒人整合包，这套就是SpringBoot

所有，用最简练的语言概括就是：

- **Spring是一个引擎；**
- **SpringMVC是基于Spring的一个MVC框架；**

- **SpringBoot是基于Spring4的条件注册的一套快速开发整合包**

 

但是面试官提问这些并非需要这些答案！

SpringMVC从两个方面看

1.Spring的核心中IOC与AOP。IOC就是控制翻转（就是将原本由程序代码直接操作的对象的调用权交给容器）。目的是为了减低计算机代码的耦合度，所谓的耦合度就是代码中的逻辑关系不要太紧密，避免后面改的人会因为不懂业务逻辑导致改错代码，除此以外也避免我们每次创建心得对象，减少对应的代码量。我们实际代码过程中最常见的方式是依赖注入（DIDependencyInjection），所谓依赖注入就是通过构造函数注入或者set进行注入。依赖查找（DL Dependency Lookup）这是通过名称和类型查找bean，AOP分为五部门：

Aspect（切面）：通常是一个类，里面可以定义切入点和通知
JoinPoint（连接点）：程序执行中明确的点，一般是方法的调用
Advice（通知）AOP在特定的切入点做出的增强处理有before，after，afterRunning，afterThrowing，around；
Pointcut（切入点）：就是带有通知的连接点，在程序中主要体现未书写切入点表达式
AOP代理：AOP框架创建的对象，代理就是目标对象的加强，Spring的AOP可以使用JDK代理，也可以使用CGLIB代理，前者基于接口，后者基于子类
区别

springboot是约定大于配置，可以简化spring的配置流程，springmvc是基于servlet的mvc框架，个人感觉少了model中的映射。
以前web应用要使用到tomcat服务器启动，而springboot内置服务器容器，通过@SpringApplication中注解类中main函数启动即可
Spring的三大核心IOC（控制反转）和DI(依赖注入)和AOP（面向切面编程）

控制反转是将原先在代码中创建对象的工作交由Spring容器管理，依赖注入采用动态代理的方式进行注入，注入方式可以通过构造函数、set方法、@Autowired注解注入。spring的IOC和DI都是为了解除代码之间的耦合度，便于日后的项目扩展。举个例子：在未使用spring之前，创建对象是通过在代码中new进行实例化的，假设我这里有一个Demo类，Demo类中有一个方法叫做getInfo（），A,B,C,D类中都有调用Demo类中的getInfo（），有一天小王不小心把getInfo（）方法改动了，结果导致所有调用Demo类的getInfo（）的类都报错了，直接项目跑步起来，通过上面可想而知为什么我们需要解除程序耦合，而spring的SpringIOC和DI就是为了解决这个问题的。另外就是对象生命周期的问题，以往大量创建的示例对象在代码进行，如果对象资源不解释释放销毁很容易出现内存溢出异常



# SpringMVC与SpringBoot的区别

1、含义不同

- springboot：SpringBoot是一个自动化配置的工具。
- springmvc：SpringMVC是一个web框架。


2、配置不同

- springboot：SpringBoot采用约定大于配置的方式，通过其自动配置功能自动处理配置，同时内置服务器tomcat，打开就可以直接用。
- springmvc：此框架需要大量配置，例如 DispatcherServlet 配置和 View Resolver 配置。需要手动配置xml文件，同时需要配置Tomcat服务器。


3、依赖项不同

- springboot：springboot具有启动器的概念，一旦将其添加到类路径中，它将带来开发Web应用程序所需的所有依赖项。
- springmvc：需要单独指定每个依赖项才能运行功能。


4、开发时间不同

- springboot：Spring Boot有助于减少开发时间，因为所有与依赖关系相关的任务都会得到处理。
- springmvc：与Spring Boot相比，开发所需的时间更多，因为开发人员需要花时间添加所需的依赖项。


5、生产力不同

- springboot：由于开发时间更短，生产力提高。
- springmvc：生产力降低，因为需要了解依赖性附加组件。


6、实现JAR打包功能的方式不同

- springboot：Spring Boot 允许嵌入式服务器以独立的方式运行该功能。
- springmvc：Spring MVC需要大量手动配置才能实现JAR打包的功能。


7、是否提供批处理功能

- springboot：它提供强大的批处理。
- springmvc：它不提供强大的批处理。


8、作用不同

- springboot：Spring Boot也允许构建不同类型的应用程序。
- springmvc：Spring MVC仅用于开发动态网页和RESTful网络服务。


9、社区和文档支持不同

Spring MVC的社区和文档比Spring boot要好得多。

10、是否需要部署描述符

- springboot：不需要部署描述符。
- springmvc：需要部署描述符。
