# iOS_Interview


## #import 和 #include 的区别， @class 有什么用？

`@class` 一般用于头文件中需要声明该类的某个实例变量的时候用到，在`.m`文件中还是需要使用`#import`

`#improt` 比起 `#imclude`的好处在于**不会一起交叉编译**



## readwirte、 readonly、assign、retain、copy、nonatomic 属性关键词的作用。

`@property`是一个属性访问声明，括号内支持一下几个属性关键词：

1. getter=getName，setter=setName， 设置属性存取方法的别名。
2. readwrite、readonly， 设置可供访问的级别。
3. assign，setter方法可以直接赋值，不进行 retain 操作，为了解决原类型与循环引用的问题。
4. retain，setter方法对参数进行 release 旧值，再 retain 新值，所有实现都是这个顺序。
5. copy, setter 方法进行 copy 操作，与 retain 处理流程一样，先旧值 release， 再 copy 出新的对象， retainCount 为1 。这是为了减少对上下文的依赖而引入的机制。
6. nonatomic，非原子性访问，不加同步，多线程并发访问会提高性能。注意，如果不加此属性，则默认是两个访问方法都为原子性访问。



## 在一个对象的方法里面： self.name = "obj"; 和 _name=“obj” 有什么区别？



使用点语法会调用setter方法赋值。









