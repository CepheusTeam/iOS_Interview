# UI 基础





## 简要说明`viewDidLoad`和`viewDidUnload`何时调用?



viewDidLoad 在view从nib文件初始化的时候调用，

loadView 在 controller 的 view 属性为 nil 的时候调用

此法在编程实现view 的时候调用，view的控制器默认会注册 `memory warning notification`



当controller的人和view都没有用的时候 viewDidUnload 方法会被调用，在这里实现将 retain 的 view release， 如果是IBOutlet 的view 则不在这里release ，这类 View 的释放有 XIB 控制。





## 控件响应的事件



基于触摸事件、基于值的事件 和 基于编辑的事件。





## XIB 文件的构成分为哪三个图标？ 都具有什么功能？



File's Owner 是所有 nib 文件中的每个图标，它表示从磁盘加载 nib 文件的对象；

First Responder 就是用户当前正在交互的对象；

View 显示用户界面，完成用户交互，是UIView及其子类；



## 简述视图控件的生命周期



1. loadview 尽管我们不直接调用这个方法，如果手动创建自己的视图，那么应该覆盖这个方法，并将它们赋值给视图控制器的 View 属性。
2. viewDidLoad 只有在视图控制器将其视图载入到内存之后才调用该方法，这是执行任何其他初始化操作的入口。
3. viewDidUnload 当视图控制器从内存释放自己的方法的时候调用，用于清除那些可能以及在视图控制器中创建的对象
4. viewWillAppear 当视图将要添加到窗口中并且还不可见的时候或者上层视图移除图层后本视图变成顶级视图时调用该方法，用于执行诸如改变视图方向等的操作。
5. viewDidAppear 当视图添加到窗口中以后或者上层视图移出图层后本视图变成顶级视图时调用，用于放置那些需要在视图显示后执行的代码。
6. viewWillDisappear
7. viewDidDisappear





## UIView 和 CALayer 有什么区别？

1. UIVIew 是 iOS 系统中界面元素的基础，所有的界面元素都继承自它。它本身完全是由 CoreAnimation 来实现的。它真正的绘图部分，是由一个 CALayer 类来管理。 UIView 本身更像是一个 CALayer 的管理器，访问他的跟绘图和坐标有关的属性。
2. UIView 有个一个重要的属性 layer，可以返回它的主 CALayer 实例。
3. UIView 的 CALayer 类似 UIVIew 的子 View 树形结构，也可以像他的 layer 上添加子 layer， 来完成某些特殊的表示。 即 CALayer 层是可以嵌套的。
4. UIview 的 layer 树形实在系统内部，被维护着三份 copy。 分别是：
   1. 逻辑树，这里是代码可以操纵的。
   2. 动画树，这是一个中间层，系统就在这一层上更改属性，进行各种渲染操作。
   3. 显示树，其内容就是当前正在被显示在屏幕上的内容。
5. 动画的运作：
   * 对 UIView 的 subLayer（非主 Layer）属性进行更改，系统将自动进行动画生成，动画持续时间的缺省值大概是0.5秒。
6. 坐标系统：
   * CALayer 的坐标系统比 UIView 多了一个 anchorPoint 属性，使用 CGPoint 结构表示，值域是0-1，是一个比例值。这个点是各种图形变换的坐标原点，同时会更改 layer 的 position 的位置，它的缺省值是{0,5,0,5}即layer的中央
7. 渲染: 当更新层，改变不能立即显示在屏幕上。当所有的层都准备好时，可以调用 setNeedsDisplay 方法来重绘显示。
8. 变换：要在一个层中添加一个3D 或者仿射变换，可以分别设置层的 transform 或 affineTransform 属性
9. 变形：QuartzCore 的渲染能力，使二维图像可以被自由的操纵，就好像是三维的。图像可以在一个三维坐标系中以任意角度被旋转，缩放，和倾斜。CATransform3D 的一套方法提供了一些魔术般的变换效果。





## CocoaTouch 提供了哪几种 CoreAnimation 过渡类型



交叉淡化、推挤、显示、覆盖





## frame 和 bounds 的区别



frame 指的是：该 view 在父 view 坐标系统中的位置和大小。（参照点是父亲的坐标系统）//frame:框架、结构

bounds指的是：该 view 在本身坐标系统中的位置和大小。（参照点是本身坐标系统）//bounds:界限 



## Quatrz2D的绘图功能的三个核心概念是什么并简述其作用



上下文： 主要用于描述图形写入哪里；

路径：是在图层上绘制的内容

状态：用于保存配置变换的值、填充和轮廓，alpha值等。



## 有那几种手势通知方法



```objective-c
-(void)touchesBegan:(NSSet)touchedwithEvent:(UIEvent)event;

-(void)touchesMoved:(NSSet)touched withEvent:(UIEvent)event;

-(void)touchesEnded:(NSSet)touchedwithEvent:(UIEvent)event;

-(void)touchesCanceled:(NSSet)touchedwithEvent:(UIEvent)event;
```



