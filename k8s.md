

### k8s-集群中的三种ip

- Node IP：物理网卡的ip地址，也即node 节点的ip地址

  > 可以是物理机的ip，也可以是虚拟机的ip，每个service都会在node上开通一个端口，外部可以通过node ip：NodePort 访问

- Pod IP： docker 容器的ip地址，即pod的ip地址，此为虚拟ip地址

  > docker engine 根据docker 网桥的ip地址段进行分配的，通常是一个虚拟的二层网络

- Cluster IP： Service的ip地址，虚拟ip地址

  > service地址不配在pod或者主机上，外部访问时，先到node节点网络，再转到service网络，最后代理给pod网络
  >
  > service 的ip地址，外部网络无法ping通，只有k8s集群内部访问使用
  >
  > cluster ip无法被ping，只能结合service port 组成一个具体的通信端口





### k8s的service

通过创建service，可以为一组具有相同功能的容器应用提供一个统一的入口地址，并且将请求负载分发到后端的各个容器应用上。