# 服务发现

服务与发现。微服务架构都是分布式架构。由于使用了K8s这些服务编排系统，所以运行的服务在那个服务器或者说那个ip，并不确定。而且一个服务可能会有多个副本在运行。所以每运行一个任务需要进行注册，当调用一个服务需要查找发现这个服务。

## 服务与发现的方案

### 集中式LB方案

![](/assets/集中式lb.png)

服务消费者和服务提供者之间有一个独立的LB，LB通常是专门的硬件设备如F5，或者基于软件如LVS，HAproxy等实现。LB上有所有服务的地址映射表，通常由运维配置注册，当服务消费方调用某个目标服务时，它向LB发起请求，由LB以某种策略（比如Round-Robin）做负载均衡后将请求转发到目标服务。LB一般具备健康检查能力，能自动摘除不健康的服务实例。服务消费方如何发现LB呢？通常的做法是通过DNS，运维人员为服务配置一个DNS域名，这个域名指向LB。

集中式LB方案实现简单，在LB上也容易做集中式的访问控制，这一方案目前还是业界主流。集中式LB的主要问题是单点问题，所有服务调用流量都经过LB，当服务数量和调用量大的时候，LB容易成为瓶颈，且一旦LB发生故障对整个系统的影响是灾难性的。另外，LB在服务消费方和服务提供方之间增加了一跳\(hop\)，有一定性能开销。

### 进程内LB方案

![](/assets/进程内的lb.png)

针对集中式LB的不足，进程内LB方案将LB的功能以库的形式集成到服务消费方进程里头，该方案也被称为软负载\(Soft Load Balancing\)或者客户端负载方案，下图Fig 2展示了这种方案的工作原理。这一方案需要一个服务注册表\(Service Registry\)配合支持服务自注册和自发现，服务提供方启动时，首先将服务地址注册到服务注册表（同时定期报心跳到服务注册表以表明服务的存活状态，相当于健康检查），服务消费方要访问某个服务时，它通过内置的LB组件向服务注册表查询（同时缓存并定期刷新）目标服务地址列表，然后以某种负载均衡策略选择一个目标服务地址，最后向目标服务发起请求。这一方案对服务注册表的可用性\(Availability\)要求很高，一般采用能满足高可用分布式一致的组件（例如Zookeeper， Consul， Etcd等）来实现。

进程内LB方案是一种分布式方案，LB和服务发现能力被分散到每一个服务消费者的进程内部，同时服务消费方和服务提供方之间是直接调用，没有额外开销，性能比较好。但是，该方案以客户库\(Client Library\)的方式集成到服务调用方进程里头，如果企业内有多种不同的语言栈，就要配合开发多种不同的客户端，有一定的研发和维护成本。另外，一旦客户端跟随服务调用方发布到生产环境中，后续如果要对客户库进行升级，势必要求服务调用方修改代码并重新发布，所以该方案的升级推广有不小的阻力。

进程内LB的案例是Netflix的开源服务框架，对应的组件分别是：Eureka服务注册表，Karyon服务端框架支持服务自注册和健康检查，Ribbon客户端框架支持服务自发现和软路由。另外，阿里开源的服务框架Dubbo也是采用类似机制。

### 独立LB进程方案

![](/assets/独立主机的lb.png)

该方案是针对第二种方案的不足而提出的一种折中方案，原理和第二种方案基本类似，不同之处是，他将LB和服务发现功能从进程内移出来，变成主机上的一个独立进程，主机上的一个或者多个服务要访问目标服务时，他们都通过同一主机上的独立LB进程做服务发现和负载均衡，

该方案也是一种分布式方案，没有单点问题，一个LB进程挂了只影响该主机上的服务调用方，服务调用方和LB之间是进程内调用，性能好，同时，该方案还简化了服务调用方，不需要为不同语言开发客户库，LB的升级不需要服务调用方改代码。该方案的不足是部署较复杂，环节多，出错调试排查问题不方便。

该方案的典型案例是Airbnb的SmartStack服务发现框架，对应组件分别是：Zookeeper作为服务注册表，Nerve独立进程负责服务注册和健康检查，Synapse/HAproxy独立进程负责服务发现和负载均衡。Google最新推出的基于容器的PaaS平台Kubernetes，其内部服务发现采用类似的机制。

### 方案总结

集中式方案一般应用与客户软件与服务器之间的交互。例如手机app调用远端服务端口，web的前端javascript请求服务端数据的时候使用。

进程内LB方案和独立进程LB方案一般用与微服务各个服务之间的相互调用。现在们研究微服务的服务与发现，一般就用这两种方案。

## 服务与发现的常用框架

1. [consul](https://www.consul.io/)在一个单一的数据中心内部使用服务节点。在每个数据中心中，为了Consule能够运行，并且保持强一致性，Consul服务端需要仲裁。然而，Consul原生支持多数据中心，就像一个丰富gossip系统连接服务器节点和客户端一样。

2. [Zookeeper](https://zookeeper.apache.org/)是一个用户维护配置信息、命名、分布式同步以及分组服务的集中式服务框架，它使用Java语言编写，通过[Zab](http://www.stanford.edu/class/cs347/reading/zab.pdf)协议来保证节点的一致性。因为Zookeeper是一个CP型系统，所以当[网络分区](http://wiki.apache.org/hadoop/ZooKeeper/FailureScenarios)问题发生时，系统就不能注册或查找服务。

3. [Doozer](https://github.com/ha/doozerd)是一个一致性的、分布式存储系统，使用Go语言编写，通过[Paxos](http://research.microsoft.com/en-us/um/people/lamport/pubs/lamport-paxos.pdf)来保证强一致性，Doozer项目目前已经停止更新并有将近160个分支。和Zookeeper一样，Doozer也是一个CP型系统，在网络分区问题发生时，会有同样的问题。

4. [etcd](https://github.com/coreos/etcd)是一个用于共享配置和服务发现的高可用的键值存储系统，使用Go语言编写，通过Raft来保证一致性，有基于HTTP+JSON的API接口。etcd也是一个强一致性系统，但是etcd[似乎支持](https://github.com/coreos/etcd/blob/master/server/v2/get_handler.go#L25)从non-leaders中读取数据以提高可用性；另外，写操作仍然需要leader的支持，所以在网络分区时，写操作仍可能失败。

另外附一个consul对比Zookeeper表格

|  | consul | Zookeeper |
| :--- | :--- | :--- |
| 软件类型 | 专门做服务注册和发现可 | 可以用来做服务注册和发现 |
| 方案 | 独立的进程方案进 | 进程内的服务 |
| UI | 漂亮的UI来做服务监控和节点监控 | 没有UI，你需要DIY |
|  | 支持Key/Value存储，可以用来做动态配置 | 支持节点数据，也可以用来做动态配置 |
| 多数据中心 | 支持多数据中心\(多机房数据备份\) | 不支持 |

## 

## 参考链接：

Jason Wilder的一篇[博客 http://jasonwilder.com/blog/2014/02/04/service-discovery-in-the-cloud/](http://jasonwilder.com/blog/2014/02/04/service-discovery-in-the-cloud/)对分别对常见的服务发现开源项目Zookeeper、Doozer、etcd进行了总结介绍：

[https://segmentfault.com/a/1190000008672912](https://segmentfault.com/a/1190000008672912) 服务发现

微服务框架-服务注册和发现 [https://www.jianshu.com/p/3b206180086b](https://www.jianshu.com/p/3b206180086b)

实施微服务，我们需要哪些基础框架？[http://www.infoq.com/cn/articles/basis-frameworkto-implement-micro-service](http://www.infoq.com/cn/articles/basis-frameworkto-implement-micro-service)

Consul和ZooKeeper的区别[http://dockone.io/article/300](http://dockone.io/article/300)

Raft算法可以通过这个[动画 http://thesecretlivesofdata.com/raft/](http://thesecretlivesofdata.com/raft/)来学习下，非常直观

Consul 简介和快速入门 [https://www.gitbook.com/book/vincentmi/consul-guide/details](https://www.gitbook.com/book/vincentmi/consul-guide/details)





