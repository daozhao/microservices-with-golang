[https://segmentfault.com/a/1190000008672912](https://segmentfault.com/a/1190000008672912)



服务发现

consul [https://www.consul.io/](https://www.consul.io/)

[**etcd**](https://github.com/coreos/etcd)[https://github.com/coreos/etcd](https://github.com/coreos/etcd)

Raft算法可以通过这个[动画](http://thesecretlivesofdata.com/raft/)来学习下，非常直观

Zookeeper

Consul和ZooKeeper的区别[http://dockone.io/article/300](http://dockone.io/article/300)

**微服务框架-服务注册和发现**[**http://www.jianshu.com/p/3b206180086b**](http://www.jianshu.com/p/3b206180086b)

Jason Wilder的一篇[博客](http://jasonwilder.com/blog/2014/02/04/service-discovery-in-the-cloud/)对分别对常见的服务发现开源项目Zookeeper、Doozer、etcd进行了总结介绍：

Zookeeper是一个用户维护配置信息、命名、分布式同步以及分组服务的集中式服务框架，它使用Java语言编写，通过[Zab](http://www.stanford.edu/class/cs347/reading/zab.pdf)协议来保证节点的一致性。因为Zookeeper是一个CP型系统，所以当[网络分区](http://wiki.apache.org/hadoop/ZooKeeper/FailureScenarios)问题发生时，系统就不能注册或查找服务。

[Doozer](https://github.com/ha/doozerd)是一个一致性的、分布式存储系统，使用Go语言编写，通过[Paxos](http://research.microsoft.com/en-us/um/people/lamport/pubs/lamport-paxos.pdf)来保证强一致性，Doozer项目目前已经停止更新并有将近160个分支。和Zookeeper一样，Doozer也是一个CP型系统，在网络分区问题发生时，会有同样的问题。

etcd是一个用于共享配置和服务发现的高可用的键值存储系统，使用Go语言编写，通过Raft来保证一致性，有基于HTTP+JSON的API接口。etcd也是一个强一致性系统，但是etcd[似乎支持](https://github.com/coreos/etcd/blob/master/server/v2/get_handler.go#L25)从non-leaders中读取数据以提高可用性；另外，写操作仍然需要leader的支持，所以在网络分区时，写操作仍可能失败。



