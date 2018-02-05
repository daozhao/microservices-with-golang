# 日志

日志在传统的后台程序通常是有单一一个日志，非常方便进行查找，遍历，统计等操作。当时由于微服务架构，不同的服务有不同的日志，而且不同的服务可能分别运行在不同的机器上边。这样增加了日志管理的难度。所以我们需要把日志统一搜集到一个统一的地方。方便查找，遍历，统计等。不过比较幸运的是。这些工作我们都不必通过编程而获得。只需使用相关开源的系统实现就可以了。我们的日志只需要按照原有的方式打印到stdout或者日志文件中就可以了。

## 日志处理系统ELK

ELK由ElasticSearch、Logstash和Kiabana三个开源工具组成。官方网站：[https://www.elastic.co/products](https://www.elastic.co/products)



利用docker只需5步搭建ELK日志分析系统 https://www.kancloud.cn/hanxt/elk/158871



