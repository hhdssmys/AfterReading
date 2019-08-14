## 初读《Spring技术内幕：深入解析Spring架构与设计原理（第2版）》

本书目前只看了前两部分`核心实现`（IOC,AOP）与`组件实现`（mvc,数据库,事务,远端调用）等， 
其中 IOC 与 AOP 是一切的基础，书中对 spring 各部分整体架构与重点部分的代码实现做了详尽介绍， 
包括涉及的设计模式，比较难啃，却十分值得，虽然后面的 `应用实现篇` 尚未阅读且于 20190814 尚未接触， 
但是相信其值得期待。 
 
  
### 笔记 
+ IOC启动
1. BeanDefinition 资源 Resource 定位
2. BeanDefinition 加载与解析
3. BeanDefinition 在IOC容器(BeanFactory与ApplicationContext)中的注册
- 依赖注入
1. 一般是getBean() 方法触发，但是也有提前触发的时机
+ AOP动态代理的两方式
