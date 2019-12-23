#### head_first_设计模式  

##### OO (面向对象)基础特性  
抽象，封装，继承，多态  

##### OO 准则  
1. 封装变化，与不变的相隔离  
2. 多用组合，少用继承  
3. 针对接口编程，不针对实现编程（eg. 对象通过接口相互依赖，可以实现低耦合） 
4. 为交互对象间的松耦合设计而努力  
5. 对扩展开放，对修改关闭  
6. 依赖倒转原则（1.高层模块不应该依赖低层模块，两者都应该依赖其抽象 2.抽象不应该依赖细节 3.细节应该依赖抽象）  

##### OO 设计模式  
1. 策略模式  
2. 观察者模式  
 &emsp;经典实现：Java 事件 （Observe 观察者 与 Observable 可观察者，即主题 subject ）  
 &emsp;注意：（观察者持有主题的依赖，可以实现数据拉取）
3. 装饰者模式：动态的将责任附加到对象上。扩展对象功能的，完全符合开闭原则  
 &emsp;经典实现：Java IO  
 &emsp;优点：  
 &emsp;&emsp; 1) 装饰与被装饰者有相同的超类型   
 &emsp;&emsp; 2) 因 1 凡是需要原始对象的地方都可以使用装饰对象（面向接口编程）  
 &emsp;&emsp; 3) 装饰者可以在委托前后加上自己的行为  
 &emsp;缺点：  
 &emsp;&emsp; 1) 具体组件，或者具体装饰都容易过多，表现出类爆炸的现象  
 &emsp;&emsp; 2) 装饰者需要持有一个组件，但是组件的构造较为麻烦  
4. 工厂模式  
5. 单例模式（确保一个类只有一个实例，并提供全局访问点）  
 &emsp;&emsp; 1) 一个实例：构造器私有，只能类内成员访问  
 &emsp;&emsp; 1) 静态方法 构造 实例     
 ```
 public MyClass {
   private static MyClass instance;
   private MyClass(){}
   public static MyClass getInstance(){
     //延迟实例化
     if(instance==null){
       instance = new MyClass();
     }
     return instance;
   }
 }
 //延迟实例化存在多线程问题，解决方案：
 1）public static synchronized MyClass getInstance(){ ... }
 2) 急切实例化 private static MyClass instance = new MyClass();
 3）双重检查加锁 
   if(instance==null){
     synchronized(MyClass.class){
       if(instance==null){
         instance = new MyClass();
       }
     }
   }
 ```
