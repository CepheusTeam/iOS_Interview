# OC 基础





## #import 和 #include 的区别， @class 有什么用？

`@class` 一般用于头文件中需要声明该类的某个实例变量的时候用到，在`.m`文件中还是需要使用`#import`

`#improt` 比起 `#imclude`的好处在于**不会一起交叉编译**





## #include\<filename> 和 #include"filename"的区别

＃include\<filename>直接在库文件目录中搜索所包含的文件；

＃include”filename”在当前目录下搜索所包含的文件，如果没有的话再到库文件目录搜索。







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





## 简述self.name = nil 的机制，以及与[name release]的区别？

 

 self.name =nil;   //使用nil参数调用setName:方法

[name release］生成的访问器将自动释放以前的 name 对象





## 数组与指针的区别



1. 数组可以申请在栈区和数据区；指针可以指向任意类型的内存块
2. sizeof作用于数组时，得到的是数组所占的内存大小；作用于指针时，得到的都是4个字节的大小
3. 数组名表示数组首地址，值可以不变，不可以将++ 作用于数组名上，普通指针的值可以改变，可以将++ 作用于指针上
4. 用字符串初始化字符数组是将字符串的内容拷贝到字符数组中；用字符串初始化字符指针是将字符串的首地址赋给指针，也就是指针指向了该数组。



## static的作用



1. 函数体内 static 变量的作用范围为该函数体，不同与 auto 变量，该变量的内存只被分配一次，因此该变量的值在下次调用的时候仍然维持上次的值；
2. 在模块内的 static 全局变量可以被该模块内的其他函数访问，但是不能被模块外的其他函数访问；
3. 在模块内的 static 函数只可以被这一模块内的其他函数调用，这个函数的使用范围被限制在声明他的模块内。
4. 在类的 static 成员变量属于整个类所拥有，对类的所有对象只有一份拷贝；
5. 在类中的 static 成员变量属于整个类所拥有，这个函数不接收 this 指针，因为智能访问类的 static 成员变量





## 简述内存分区的情况



1. 代码区：存放函数二进制代码
2. 数据区：系统运行时申请内存并初始化，系统推出时由系统释放。存放全局变量、静态变量、常量。
3. 堆区：通过 malloc 等函数或者 new 等操作符动态申请得到，需程序员手动申请和释放。
4. 栈区：函数模块内申请，函数结束时由系统自动释放。存放局部变量、函数参数。



## OC的优点和缺点

优点：

1. Category
2. posing
3. 动态识别
4. 指标计算
5. 弹性讯息传递
6. 不是一个过度复杂的 C 衍生语言
7. OC 可以和 Cpp 混合编程

确定

1. 不支持命名空间
2. 不支持运算符重载
3. 不支持多重继承
4. 使用动态运行时类型，所有的方法都是函数调用，所以很多编译时优化方法都用不到。（如内联函数等），性能低劣。




## OC中加号方法和减号方法的区别？

加号方法是类方法，属于静态方法

减号方法是实例方法，必须由类的实例来调用








## 队列和栈的区别



队列和栈是两种不同的数据容器。从数据结构的角度看，它们都是线性结构，即数据元素之间的关系相同



队列是先进先出的数据结构，他在两端进行操作，一端进行入队列操作，一端进行出队列操作。



栈是一种先进后出的数据结构，它只能在栈顶进行操作，入栈和出栈都在栈顶操作。





## 类别的作用？继承和类别分别在实现中有什么区别？



category 可以在不获悉，不改变原来代码的情况下往里面添加新的方法，只能添加不能删除和修改。并且如果类别和原来类中的方法产生名称冲突，则类别奖覆盖原来的方法，因为类别具有更高的优先级。类别主要有3个作用：

1. 将类的实现分散到多个不同文件或者多个不同的框架中
2. 创建对私有方法的向前引用
3. 向对象添加非正式协议，继承可以增加修改方法，并且可以增加属性。





## id 声明的对象有什么特性？



id 是一个很重要的类型，是一个可以指向任何类型的指针或者可以理解为指向任何未知类型的指针。





## 自动释放池跟GC有什么区别？iPhone 上有 GC 吗？[poor release] 和 [pool drain]有什么区别?



iPhone 上没有GC 。 iPhone 在开发的时候没有垃圾回收机制。在垃圾回收环境中， release 是一个空操作。因此 NSAutoreleasePrrl 提供了 drain 方法。在引用计数环境中，改方法的作用等同于调用 release 。但在垃圾回收环境中，他会触发垃圾回收(如果自上次垃圾回收以来分配的内存大于当前的阀值)。因此，在通常情况下，应该是用 drain 来销毁自动释放池。





## OC的类可以多重继承么？可以实现多个接口么？重写一个类的方式用继承好还是分类好？为什么？



OC 只支持单继承，如果要实现多继承的话，可以通过类别和协议的方法来实现，Cocoa 中所有的类都是 NSObject 的字类，多继承在这里是用 protocol 委托代理来实现的。



## 线程与进程的区别和联系？



线程和进程都是由操作系统所体会的程序的基本单元，系统利用该基本单元实现系统对应的并发行。进程和线程的主要差别在于它们是不同的操作系统资源管理方式。进程有独立的地址空间，一个进程崩溃后，在保护模式下，不会对其他进程产生影响，而线程是一个进程的不同执行路径。线程有自己的堆栈和局部变量，但线程之间没有单独的地址空间，一个线程死掉就等于整个进程死掉，所以多进程的持续要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些。但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。



## OC 有私有方法吗？ 私有变量呢？



OC类里面的方法只有两种，静态方法和实例方法。这似乎就不是完整的面向对象了，按照OO的原则就是一个对象只暴露有用的东西。如果没有私有方法的话，对于一些小范围的代码重用就不那么顺手了，在类里面声明一个私有方法

```objective-c
@interface Controller : NSObject { 
  NSString *something; 
}

+ (void)thisIsAStaticMethod;
- (void)thisIsAnInstanceMethod;
@end
  
@interface Controller (private) 
  
- (void)thisIsAPrivateMethod;
@end

```



`@private`可以用来修饰私有变量

在OC中，所有实例变量默认都是私有的，所有实例方法默认都是公有的。



## HTTP 协议中 POST 和 GET 的区别？



1. **GET方法**
   1. GET方法提交的数据不安全，数据置于请求行，客户端地址栏可见。
   2. GET方法提交的数据大小有限
   3. GET方法不可以设置书签
2. **POST方法**
   1. POST方法提交的数据安全，数据置于消息主体内，客户端不可见
   2. POST方法提交的数据大小没有限制
   3. POST方法可以设置书签




## 用预处理指令 #define 声明一个常数，用以表示一年有多少秒，忽略闰年问题。



```objective-c
#define SECONDS_PER_YEAR (60*60*24*365)UL
```



注意点：

1. `#define` 的语法基本知识；  不能以分号结束，括号的使用等
2. 懂得预处理器将为你计算常数表达式的值，因此，直接写出你是如何计算一年中有多少秒而不是计算出实际的值，是更清晰而没有代价的。
3. 意识到这个表达式将使一个16位机的整型数溢出-因此要用到长整型符号L,告诉编译器这个常数是的长整型数。





## 写一个标准宏MIN ，这个宏输入两个参数并返回较小的一个



```objective-c
#define MIN(A,B) ((A) < (B) ? (A) : (B))
```



注意点：

1. 标识 `#define`在宏中应用的基本知识。这是很重要的，因为直到嵌入操作符变为标准C的一部分，宏是方便产生嵌入代码的唯一方法，对于嵌入式系统来说，为了达到性能要求，迁入代码经常是必须的方法。

2. 三重条件操作符的知识。这个操作符存在C语言中的原因是它使得编译器能产生比if else 更优化的代码。

3. 懂得在宏中小心的把参数用括号括起来。

   ```c
   //例如：当你写下面的代码时会发生什么事？  
   least = MIN(*p++,b);

   //结果是：

   ((p++) <= (b) ? (p++) :(*p++))

   //这个表达式会产生副作用，指针p会作三次++自增操作。 

   ```

   ​



### 简述ARC机制？



ARC,自动引用计数。简单的说就是代码中自动加入了 retain release 相关代码，原先需要手动添加的涌来处理内存管理的引用计数代码可以自动的由编译器完成了。



使用ARC的好处：

1. ARC之后OC的代码更容易写了。因为我们不需要担心内存管理这样的问题了
2. 代码的总量变少了，节省了很多的劳动力
3. 代码高速话。由于使用编译器管理引用计数，减少了低效代码的可能性。



不好的地方：

1. ARC学习成本
2. 一些旧的代码，或者MRC三方代码，使用起来比较麻烦。





## 自动释放池是什么，如何工作？



当你向一个对象发送一个autorelease 消息时，Cocoa就会将该对象的一个引用放入到最新的自动释放池。它仍然是个正当的对象，因此自动释放池定义的作用域内的其它对象可以向它发送消息。当程序执行到作用域结束的位置时，自动释放池就会被释放，池中的所有对象也就被释放。

1. OC 是 通过一种”referring counting”(引用计数)的方式来管理内存的, 对象在开始分配内存(alloc)的时候引用计数为一,以后每当碰到有copy,retain的时候引用计数都会加一, 每当碰到release和autorelease的时候引用计数就会减一,如果此对象的计数变为了0, 就会被系统销毁.
2. NSAutoreleasePool 就是用来做引用计数的管理工作的,这个东西一般不用你管的.
3. autorelease和release没什么区别,只是引用计数减一的时机不同而已,autorelease会在对象的使用真正结束的时候才做引用计数减一.



## MVC的理解

MVC模式考虑三种对象：模型对象、视图对象和控制器对象。 模型对象负责应用程序的数据和定义操作数据的逻辑； 视图对象知道如何显示应用程序的模型数据； 控制器对象是M与V之间的协调者。



## 浅复制和深复制的区别？//浅拷贝和深拷贝



浅层复制（copy）：只复制指向对象的指针，而不复制引用对象本身。//通过对象的指针来访问这个对象

深层复制（mutableCopy）：复制引用对象本身意思就是有个A对象，复制一份后得到A_copy对象后，对于浅复制来说，A和A_copy指向的是同一个内存资源，复制的只不过是是一个指针，对象本身资源 还是只有一份，那如果我们对A_copy执行了修改操作,那么发现A引用的对象同样被修改，这其实违背了我们复制拷贝的一个思想。深复制就好理解了,内存中存在了 两份独立对象本身。//当修改A时，A copy不变。



## iOS 的系统架构？



iOS的系统架构分为

1. 核心操作层 Core OS layer
2. 核心服务层 Core Service layer
3. 媒体层  Media layer
4. Cocoa 界面服务层 Cocoa Touch Layer


## 



## iOS主要提供了几种播放音频的方法



SystemSound Services

AVAudioPlayer

Audio Queue Services

OpenAL



## 使用 AVAudioPlayer 累调用哪个框架，使用步骤？



ACFoundation Framework

步骤：

配置 AVAudioPlayer对象；

实现 AVAudioPlayer 类的委托方法；

控制 AVAudioPlayer 类的对象；

监控音量水平；

回放进度和拖拽播放





## Core Foundation 中提供了哪几种操作 Socket 的方法



CFNetwork、 CFSocket 、 BSD Socket



## CFSocket 使用有几个步骤

创建 Socket 的上下文

创建 Socket

配置要访问的服务器学习

封装服务器学习

连接服务器



## 单件实例是什么？



Foundation 和 Application Kit 框架中的一些类只允许创建单个对象，即这些类在当前进程中的唯一实例。举例来说，NSFileManager 和 NSWorkspace 类在使用的时候都是基于进程进行单件对象的实例话。当向这些类请求实例的时候，他们会像我们传递一个单一实例的引用，如果该实例还不存在，则首先进行实例的分配和初始化。单件对象充当控制中心的角色，复制指引或者协调类的各种服务。如果类在概念上只有一个实例（如 NSWorkspace）就应该产生一个单件实例，而不是多个实例；如果将来某一天可能有多个实例，您可以使用单件实例机制，而不是工厂方法或函数。





## 获取项目根路径，并在其下创建一个`userData` 的目录



**获取根路径**

```objective-c
NSArray *path = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory,NSUserDomainMask,YES);
NSString *documentDirectory = [paths objectAtIndex：0];
```

**创建文件系统管理器**

```objective-c
NSFileManager *fileManager = [[NSFileManager alloc] init];
```

**判断 userData 目录是否存在**

```objective-c
if(![fileManager fileExistAtPath:[NSString stringWithFormat@"%@/userData",documentDirectory]]) {
  //不存在，创建一个
  [fileManager createDirectoryAtPath:[NSStringstringWithFormat:@"%@/userData",documentsDirectory] withIntermediateDirectories:falseattributes:nilerror:nil];
}
```



## OC 中的数字对象都有哪些，简述它们与基本数据类型的区别是什么？



在 OC 中 NSNumber 是数字对象，可以进行拆装箱操作！

// 将 int 转为 NSNumber

NSNumber *num = [NSNumber numberWithInt:123];

// 得到一个 int

int testNum = [num intValue];



## 找出一下代码的问题？



```objective-c
@implementation Person  
- (void)setAge:(int)newAge {  
self.age = newAge;  
}
@end
```

 死循环。



## 截取字符串`**20 ****｜****http://www.621life.com**`中`|`字符串前面以及后面的数据，分别输出它们



```objective-c
NSString *str = “20|http://www.621life.com”;
NSRange range = [strrangeOfString:@"|"];
int location = range.location;
NSString *str1 = [strsubstringToIndex:location];
NSString *str2 = [str substringFromIndex:location+1];

```

