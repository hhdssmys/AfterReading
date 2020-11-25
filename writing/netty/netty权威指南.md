#### 初读《Netty权威指南》
本书分已下章节：  
>1. Java NIO 主要介绍了几种 NIO 模型 
>2. Netty NIO 开发  主要讲了 TCP 拆包，粘包的原因，以及解决方案，及案例 
>3. Netty 编码介绍，介绍了几种编码的优缺点及 netty 中的实现，推荐 protobuf
>4. netty 自定义协议开发案例 
>5. netty 源码，讲的不细致，但是学习结构可以借鉴  
>6. netty 架构介绍补充  

本书都还可以，可能4没有太多的复习价值  

#### BIO NIO 区别：
系统读，分两个阶段：1）内核准备好数据 2）拷贝至用户空间  
#### NIO 其他概念：
>1. linux 万物皆文件，文件读写看做是文件描述符 fd，描述符是一个数字，指向一个结构体，包含文件路径，<B>数据区</B>等属性
>2. select / poll ，遍历所有的 fd 集合，因此不能持有太多的fd，空循也费时间，
>3. epoll 基于事件驱动，性能更高，不受 fd 数量限制  
#### TCP 拆包粘包：
>1. 原因：下层协议对上层协议未知，不处理，TCP等会分片传输，上层协议需自行解决多个小片拼完整的问题
>2. 解决：1）定长 2）分隔符 3）header中的长度字段
#### 比较编码的因素
>1. 编码的性能，谁快
>2. 编码的体积，谁小
#### 源码学习
>1. byteBuf 
>2. channel 与 unsafe，unsfae 提供外部调用
>3. channelPipeline 与 channelHandle 责任链，调用容器，遍历list
>4. eventLoop 与 group，boss 指的是 acceptor ，work指的是 IO 线程， IO线程做3部分，1)select，pipeline 2）系统任务 3）定时任务
>5. Futrue 和 Promise
