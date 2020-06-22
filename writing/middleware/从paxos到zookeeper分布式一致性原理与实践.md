#### zookeeper知识点：  
选举机制：过半原则，影响因素：1）选举周期 2）事务id 3）服务器id
部署方式：单机模式，集群模式（奇数即可，偶数浪费）  
集群角色： Leader |  Follower   
最小的集群机器数： 3 台   
zookeeper服务器使用端口： 监听客户端端口 2181 ， 选举端口3888 ， L-F 通信端口 2888  
#### zookeeper 集群的特点： 
1. 一个Leader，多个Follower  
2. 集群只要有半数以上（不包括恰好一半）节点存活，就能提供服务  
3. 全局数据一致（伪强一致：可以过半响应确认写入）：每个server保存一份数据副本
4. 写请求，都会转发给 Leader ，来自同一个 client 的写请求 按照其发送顺序依次进行  
5. 数据更新原子性：一次数据更新要么成功，要么失败  
6. 实时性：基于内存存储，一定短暂的时间范围内，client 不论连接哪个服务器，都可以读到最新的数据  
#### 配置信息 zoo.cfg 
1. clientPort 客户端连接端口  
2. dataDir 数据文件目录+ 数据持久化路径  
3. trickTime 心跳时间间隔 ms 
4. initLimit L-F 初始化连接时，最大超时时间，是心跳间隔额倍数值  
5. syncLimit L-F 同步通信时 ，最大超时时间，是心跳间隔额倍数值  
6. server.[serverId]=IP:通信port:选举port 集群信息，多个   
7. 集群模式下，要在 dataDir 目录下 新建文件 myid ，内容为 serverId，是个整数值  
#### 写数据流程  
1. 客户端向 server 发送数据，写请求  
2. 判断该server是否是Leader，如果不是，则转发请求给Leader  
3. Leader 将该写请求广播给所有server，过半响应成功，则写成功  
4. Leader 告知原接收请求的server，写成功
5. server 通知客户端 写成功，写操作结束  

#### 命令
1. create path data  创建节点，必须有数据    
2. delete  path  删除节点  
3. set  path data 修改内容  
4. get  path 查看
5. ls 查看路径 ls2 查看详情  
6. exist 
7. 监听
> 1) get path watch 监听节点数据内容变化  
> 2) ls path watch 监听子节点增减变化  
#### 数据存储  
节点数据 + stat 状态信息  

<hr />

#### 《从paxos到zookeeper分布式一致性原理与实践》  
&emsp;&emsp;阅读本书还是很有难度的，至今对zookeeper没有一个基本的认知，但是本书依旧是本好书，要慎读paxos协议等部分  
#### 我的认知：
&emsp;&emsp;zookeeper是基于内存的，类似文件系统的<B>树形存储</B>，其节点包含两种特性（临时，顺序），另一个功能特点是（watch回调）  
##### 以下是章节：
+ 分布式架构  
> 1. 分布式架构：从ACID到CAP/BASE (概念讲的很好)  
+ 一致性协议与应用: 主指 PAXOS
> 2. 一致性协议：2PC 3PC PAXOS（过半机制）  
> 3. PAXOS的实践： Chubby HyperTable  
+ zookeeper
> 4. zookeeper的paxos实现：ZAB协议
> 5. 使用zookeeper：开发API（<B>重要</B>）  
> 6. 应用场景（<B>重要</B>）  
> 7. 技术内幕（<B>重要</B>）
> 8. 运维  
