#### 函数式编程与 Lambda 表达式
函数式编程： 行为参数化  
函数接口：只定义一个抽象方法（多余的继承方法存在也不行） 
lambda 表达式： 匿名函数的简化，没有名称，但是由参数，函数体，返回   
lambda 表达式：直接内连于方法参数，为函数式接口的抽象方法提供实现    
类型推断：根据被调用的函数接口的目标类型，进行类型推断，检查 lambda表达式      
类型推断可以省略参数列表的参数类型   
方法引用：调用特定方法的 lambda 表达的特定写法，其基本含义是lambda仅仅调用该方法，那最后用名称描述，而不是描述如何调用；目标引用`::`方法名，分隔符`::`    
> 1. 静态方法  
> 2. 任意类型的实例方法，该类型对象其实是lambda的参数     
> 3. 现有对象的实例方，该对象是一个外部已经存在的对象，不属于lambda     
> 4. 构造函数方法引用： className::new  
复合lambda 
```
  函数式接口         描述符           抽象方法       作用
 Predicate<T>       T -> boolean     test()         判断  
 Consumer<T>        T -> void        accept()       访问调用  
 Function<T,R>      T -> R           apply()        接收T，返回R，做数据加工转换  
 Supplier<T>        ()->T                           提供对象 T 
 BinaryOperator<T>  (T,T)->T                        两个值产生 一个新值
 BiFunction<T,U,R>  (T,U)->R 
```
#### Stream 流 与 并行 与 函数式接口  
1. 声明性的--易读，复合性的---灵活，可并行---性能更好   
2. 流只能消费一次，不可逆，不能重复消费同一个流，流是内部迭代   
3. 流操作：1）中间操作：多个操作连接在一起形成复合查询链  2）终端操作：触发流处理，forEach，count，collect   
```
流操作       是否是终端操作     接收参数                             作用       
###### 筛选与切片
filter                        一个返回 boolean的函数                谓词筛选
distinct                       无                                  去重
limit                          整数n                               截短前n个元素  
skip                           整数n                               跳过n个元素
####### 映射
map                                                               转换映射
flatMap                                                           转换映射，多个流合并为一个流Arrays::Stream接收数组产生一个流     
######## 查找与匹配，此处用到了短路，不必遍历处理所有元素
anyMatch      终端            谓词 boolean                         至少一个匹配
allMatch      终端             谓词 boolean 
noneMatch     终端             谓词 boolean   
findAny       终端             无                                  返回流中的任意一个，返回值是Option<T>
findFirst     终端             无
#######  规约，反复结合流中的元素，产生一个计算值
reduce                        初始值，BinaryOperator<T>  (T,T)->T   规约计算，返回值是Option<T>        

```

<hr />

#### Java 8 实战  
本书的函数式思想与流处理都是之前没有接触过得，具有研习的价值。书中也介绍了一些演化至 Java 8 时添加的新接口体系，如（Executor,LocalDtae等）  
如果只是想了解java 8 的新特性（主要是lambda与Stream），看完第二部分即可  
如果可能的话 14 部分以前的都可以看看，并发与并行，option 对null的处理，新的时间接口  
#### 章节：  
 1. 1-3 函数式编程思想（行为参数化）与 lambda 表达式  
 2. 4-7 java 8 流接口体系介绍
 3. 8-12  默认方法，Option 取代 Null，CompletableFuture,新的时间api  
 4. 13-16，其中15 16 目前的价值不高，只读13，14 即可
