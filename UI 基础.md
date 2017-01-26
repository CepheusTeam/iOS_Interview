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

1. ​