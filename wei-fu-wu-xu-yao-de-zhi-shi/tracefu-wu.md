# trace服务

trace服务主要用于调试性能和调试程序使用。传统的服务端调试都是已打印log为主，分布系统打印log这个方法已经没有办法满足了需求，当中还需要包括网络的性能监控。所以必须有一个新的方式进行跟踪调试。

关于这个分布跟踪系统有一篇比较著名的论文《Dapper，大规模分布式系统的跟踪系统》 [http://bigbully.github.io/Dapper-translation/](http://bigbully.github.io/Dapper-translation/)   英文原版地址：[https://research.google.com/pubs/pub36356.html](https://research.google.com/pubs/pub36356.html)

目前trace这部分功能有一个很好的标准开源实践－－ [http://opentracing.io/。](http://opentracing.io/。)它目前支持9个语言，包括golang，java，python，php等常用服务端使用的语言。

Opentracing并没有实现服务端搜集数据和方便查看数据的界面，这里需要使用第三方的trace 服务器。这里建议使用uber开源的jaegertracing搭建建议使用。

[https://github.com/jaegertracing/jaeger。这个是uber开源的Opentracing的服务端软件，包括web图形界面。](https://github.com/jaegertracing/jaeger。这个是uber开源的Opentracing的服务端软件，包括web图形界面。)

教程

[https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941](https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941)

其他Opentracing服务端

[https://zipkin.io/](https://zipkin.io/)



trace服务：

Opentracing[http://opentracing.io/](http://opentracing.io/)标准

chrome中进行追踪的一个工具（chrome://tracing/）



[https://uber.github.io/jaeger/](https://uber.github.io/jaeger/) Jaeger OpenTracing compatible distributed tracing system

  


**Take OpenTracing for a HotROD ride**

[https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941](https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941)

uber关于[**jaeger**](https://github.com/jaegertracing/jaeger)的demo介绍文章。

[https://www.katacoda.com/opentracing/scenarios/golang-hotrod-demo](https://www.katacoda.com/opentracing/scenarios/golang-hotrod-demo) jaeger的demo运行环境，不过有问题。

[https://lightstep.com/](https://lightstep.com/) trace系统这个好像是商业

[https://github.com/lightstep/lightstep-tracer-go](https://github.com/lightstep/lightstep-tracer-go)

**Appdash is an application tracing system for Go, based on **[**Google's Dapper**](http://research.google.com/pubs/pub36356.html)** and**[**Twitter's Zipkin**](http://twitter.github.io/zipkin/)**.**

[https://github.com/sourcegraph/appdash](https://github.com/sourcegraph/appdash)

[**https://zipkin.io/**](https://zipkin.io/)** Zipkin is a distributed tracing system. **

  
Dapper, a Large-Scale Distributed Systems Tracing Infrastructure 

[https://research.google.com/pubs/pub36356.html](https://research.google.com/pubs/pub36356.html)

google一编关于分布式跟踪系统论文  
[https://medium.com/opentracing](https://medium.com/opentracing)这里有关于open tracing的blog文章。

[https://github.com/yurishkuro/opentracing-tutorial/tree/master/go](https://github.com/yurishkuro/opentracing-tutorial/tree/master/go)[**opentracing-tutorial**](https://github.com/yurishkuro/opentracing-tutorial)

**open tracing中文文档 **[https://wu-sheng.gitbooks.io/opentracing-io/content/](https://wu-sheng.gitbooks.io/opentracing-io/content/)

open trace 简明教程 [https://github.com/yurishkuro/opentracing-tutorial](https://github.com/yurishkuro/opentracing-tutorial)

