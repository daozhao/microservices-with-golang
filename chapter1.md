# 什么是微服务架构

微服务是一种架构风格，一个大型复杂软件应用由一个或多个微服务组成。系统中的各个微服务可被独立部署，各个微服务之间是松耦合的。每个微服务仅关注于完成一件任务并很好地完成该任务。在所有情况下，每个任务代表着一个小的业务能力。

微服务的概念源于2014年3月Martin Fowler所写的一篇文章“Microservices”\([http://martinfowler.com/articles/microservices.html\)。](http://martinfowler.com/articles/microservices.html%29。)

尽管“微服务”这种架构风格没有精确的定义，但其具有一些共同的特性，如围绕业务能力组织服务、自动化部署、智能端点、对语言及数据的“去集中化”控制等等。

**用一个通俗的说法：**

**微服务架构\(Microservices Architecture\)**并不是什么新鲜事物，只是将原有的**单一服务架构\(Monolithic Architecture \)**的各个模块独立出来，每一个模块作为一个服务。服务与服务之间使用网络进行通信。对比原有的单一结构，在性能上应该下降了。但是为什么依然受到追捧尼？因为现在的系统讲求的不是单机性能，而是整个集群的性能。

## 微服务架构的优点：

* 每个微服务都相对较小，开发人员更容易理解，应用程序启动速度更快，这使开发人员的工作效率更高，并加快了部署速度

* 每项服务都可以独立于其他服务进行部署，更易于频繁部署新版本的服务

* 更容易扩大发展。它使您能够围绕多个团队组织开发工作。每个团队都拥有并负责一项或多项单一服务。每个团队都可以独立于所有其他团队开发，部署和扩展服务。

* 改进了故障隔离。例如，如果一个服务中有内存泄漏，那么只有该服务会受到影响。其他服务将继续处理请求。相比之下，单一架构中的一个行为不当的组件可能会导致整个系统崩溃。

* 每项服务都可以独立开发和部署

* 消除了对技术堆栈的长期承诺。开发新服务时，您可以选择新的技术堆栈。同样，在对现有服务进行重大更改时，您可以使用新的技术堆栈重写它。

## 缺点：

* 开发人员必须处理创建分布式系统的额外复杂性。测试更困难，开发者必须实现服务间通信机制。在不使用分布式事务的情况下实现跨多个服务的用例是很困难的，实现跨多个服务的用例需要团队之间的仔细协调

* 在生产中，部署和管理由许多不同服务类型组成的系统也存在操作复杂性。

* 增加内存消耗。 微服务体系结构用NxM服务实例替换N个单体应用程序实例。

## 适用场景及团队

有人说如果是小团队小项目不适用微服务架构。本人认为微服务可以适用绝大多数的团队和项目。除非你的项目设计目标本了就很少，根本不打算扩展的就另当别论。  
项目初期的规模可能都很少，做微服务可能感觉增加复杂度。但是这些复杂度增加非常有限，但是微服务对于将来扩展业务有着非常多的优势。所以新开发的系统我都推荐上微服务架构。对于旧有系统都可以考虑部分新业务转移到微服务。逐步推进整个服务微服务化。  
微服务

微服务需要比较强的DevOps团队。只要你的团队不是太差，花点时间增加知识就可以了。对于编程的复杂度增加是有限的，不过对于部署的难度增加相对较大的。不过项目初期，用户量不多的时候可以使用一些简易的部署方式，降低部署的难度。



GitBook allows you to organize your book into chapters, each chapter is stored in a separate file like this one.

[http://www.roncoo.com/article/detail/130121](http://www.roncoo.com/article/detail/130121)  什么是微服务架构？

[http://microservices.io/patterns/microservices.html](http://microservices.io/patterns/microservices.html)  Pattern: Microservice Architecture

[https://www.ibm.com/developerworks/community/blogs/3302cc3b-074e-44da-90b1-5055f1dc0d9c/entry/解析微服务架构\_一\_什么是微服务?lang=en](https://www.ibm.com/developerworks/community/blogs/3302cc3b-074e-44da-90b1-5055f1dc0d9c/entry/解析微服务架构_一_什么是微服务?lang=en)  解析微服务架构\(一\)：什么是微服务

[http://www.infoq.com/cn/news/2013/12/micro-service-architecture](http://www.infoq.com/cn/news/2013/12/micro-service-architecture)  微服务架构解析

[http://www.cnblogs.com/devinzhang/p/6728317.html](http://www.cnblogs.com/devinzhang/p/6728317.html)  [微服务架构介绍和RPC框架对比](http://www.cnblogs.com/devinzhang/p/6728317.html)

[http://www.infoq.com/cn/articles/basis-frameworkto-implement-micro-service](http://www.infoq.com/cn/articles/basis-frameworkto-implement-micro-service)  实施微服务，我们需要哪些基础框架？

基于微服务的软件架构模式 [https://www.jianshu.com/p/546ef242b6a3](https://www.jianshu.com/p/546ef242b6a3)

[https://martinfowler.com/articles/microservices.html](https://martinfowler.com/articles/microservices.html)  Microservices a definition of this new architectural term

