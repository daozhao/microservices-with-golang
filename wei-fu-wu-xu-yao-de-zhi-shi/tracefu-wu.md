# trace服务

trace服务主要用于调试性能和调试程序使用。传统的服务端调试都是已打印log为主，分布系统打印log这个方法已经没有办法满足了需求，当中还需要包括网络的性能监控。所以必须有一个新的方式进行跟踪调试。

关于这个分布跟踪系统有一篇比较著名的论坛《Dapper，大规模分布式系统的跟踪系统》 http://bigbully.github.io/Dapper-translation/   英文原版地址：https://research.google.com/pubs/pub36356.html



目前trace这部分功能有一个很好的标准和开源实践－－ http://opentracing.io/。

trace 服务器的搭建建议使用https://github.com/jaegertracing/jaeger。这个是uber开源的Opentracing的服务端软件，包括web图形界面。

教程  

https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941



https://zipkin.io/

