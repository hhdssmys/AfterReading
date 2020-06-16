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
