# flink

## flink  概念和部署

### flink概念

#### 窗口

- 窗口划分基于Time，Count，Session，Data-Driven

###  部署模式

- Standalone cluster （集群模式）

  > - Flink 是matster-slave 分布式处理架构
  > - master对应jobmanager
  > - slave对应taskmanager

- Flink On Yarn

  > - Hadoop Yarn 是Hadoop 2.x 提出的统一资源管理器
  > - Flink 应用提交到Yarn上目前支持两种模式：
  >   - Yarn Session Model
  >     1. 向Hadoop Yarn申请足够多的资源，并在Yarn上启动长时间运行的Flink Session集群
  >     2. 用户可以通过RestApi 或者Web页面将Flink任务提交到Flink Session集群上运行
  >   - Single Job Model
  >     1. 每个Flink任务单独向Yarn 提交一个Application
  >     2. 每个任务都有自己的JobManager和TaskManager
  >     3. 任务结束后对应的组件也会随任务释放

- Flink On Kubernetes

  - 通过Docker镜像的方式向K8s集群中提交独立的flink任务

  - 需要启动jobmanager，taskmanager，jobmanager-svc三个服务

    

  

