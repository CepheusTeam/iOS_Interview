# UI 基础





## 简要说明`viewDidLoad`和`viewDidUnload`何时调用?



viewDidLoad 在view从nib文件初始化的时候调用，

loadView 在 controller 的 view 属性为 nil 的时候调用

此法在编程实现view 的时候调用，view的控制器默认会注册 `memory warning notification`



当controller的人和view都没有用的时候 viewDidUnload 方法会被调用，在这里实现将 retain 的 view release， 如果是IBOutlet 的view 则不在这里release ，这类 View 的释放有 XIB 控制。