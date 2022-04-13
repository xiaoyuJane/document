

#### IDEA 搭建flink程序

参见https://blog.csdn.net/xiaolegeaizy/article/details/109095981

- 启动IntelliJ IDEA，创建一个新的项目

- 选择Maven项目，并选择"Create from archetype"

- 因为默认没有Flink的archetype，所以需要自己添加

  ![1649745199948](C:\Users\z18081\AppData\Roaming\Typora\typora-user-images\1649745199948.png)

  这里版本号外其他不要变

- 指定项目的groupId、artifactId名称。这里我分别取以下名称：

  - groupId：com.xueai8
  - artifactId：FlinkScalaDemo

- 指定项目的Maven配置，默认就好。

- Maven会自动构建项目（前提是安装了maven，并且m2目录下有setting.xml并且配置了仓库，这里可以用阿里云的maven）



#### 窗口触发器



参见https://www.jianshu.com/p/b1b9a688162f

窗口的触发器定义了：

- 窗口是何时被触发

- 并同时决定触发行为（对窗口进行清理或者计算）。



触发器确定窗口(由窗口分配程序形成)何时准备由窗口函数处理。

每个WindowAssigner都带有一个默认触发器。
注意：窗口的触发在内部是设置定时器来实现的。







#### 动态更改时间窗



动态滚动时间窗的实现

官方的TumblingEventTimeWindows是通过一个静态方法of(Time size)或者构造函数TumblingEventTimeWindows(long size, long offset)来确定窗口大小.我改成了从assignWindows传入的元素中获取,所以需要在调用.window(DynamicTumblingWindowAssigner)之前就把窗口大小传入元素中.
————————————————
版权声明：本文为CSDN博主「fool_dawei」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/m0_37893932/article/details/109185202







#### keydeProcessFunction

本次实战的目标是学习KeyedProcessFunction，内容如下：

1. 监听本机9999端口，获取字符串；
2. 将每个字符串用空格分隔，转成Tuple2实例，f0是分隔后的单词，f1等于1；
3. 上述Tuple2实例用f0字段分区，得到KeyedStream；
4. KeyedSteam转入自定义KeyedProcessFunction处理；
5. 自定义KeyedProcessFunction的作用，是记录每个单词最新一次出现的时间，然后建一个十秒的定时器，十秒后如果发现这个单词没有再次出现，就把这个单词和它出现的总次数发送到下游算子；

https://cloud.tencent.com/developer/article/1632976





#### flink rest api

1.集群启动后 通过 /jars/upload 向集群提交可执行jar文件

2.通过 /jars/:jarid/run 来启动一个job

https://blog.csdn.net/CarloPan/article/details/117321521







#### flink之state状态编程

##### state分类

- **ValueState**
- **AppendingState**
- **MapState**
- **BroadcastState**



在flink中，状态始终与特定算子相关联，像reduce、sum等算子都是默认带状态的，而map、flatmap本身时不带状态的，

如果需要用到状态，可以自定义

