# 部署：

部署就是把一件开发好的服务程序发布到生产机上，并运行。由于程序的开发环境与生产机的软件配置往往都不一样，也由于个个服务程序所依赖的环境也不一样。造成程序发布是一个艰难的过程，很多时候会出现软件在生产机上并不能顺利启动，或者出现这个那个的错误。后来出现了docker这个软件，docker可以为个个服务程序提供一个独立的运行环境，各个服务程序相互不影响。就很容易把这个问题解决了。可以很快速部署软件。只需把写好的软件放在docker中运行测试，测试通过后。就直接发布测试的镜像就可以了。

有了Docker对于微服务还是不够的，由于微服务的灵活多变，有时候需要编排不同的docker运行在不同的机器中，我们还需要一个docker编排服务。[Kubernetes](https://kubernetes.io/)\(k8s\)就一个目前比较流行的编排服务工具。基本上选择k8s是不会错的。安心选择他吧。

[https://kubernetes.io/](https://kubernetes.io/)

什么是Docker  [https://cloud.tencent.com/developer/article/1005172](https://cloud.tencent.com/developer/article/1005172)



Kubernetes中文指南/实践手册

[https://jimmysong.io/kubernetes-handbook](https://jimmysong.io/kubernetes-handbook)

[https://jimmysong.io/kubernetes-handbook](https://jimmysong.io/kubernetes-handbook)

