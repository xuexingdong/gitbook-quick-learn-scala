# 第5章 类

##### 5.1 简单类和无参方法

Scala中声明一个类与Java很相似：

```scala
class Counter {
  private var value = 0 // 必须初始化字段
  def increment() { value += 1 } // 方法默认为public
  def current() = value
}
```

类并不声明为`public`，一个Scala源文件可以包含多个类，这些类都具有公有可见性。

实例化类的时候，同样的采用`val myCounter = new Counter()`的形式。

调用无参方法时，`()`可以省略，即`myCounter.current`等同于`myCounter.current()`。

Scala建议的编码吗风格是：对于**改值器**方法，使用`()`；对于**取值器**方法，不使用`()`。

也可以在声明时直接不添加`()`来强制在调用时不能添加`()`，即采用`def current = value`的形式进行声明。

---

##### 5.2 带getter和setter的属性

在Java中，我们不鼓励使用公有字段，而通过`getter`和`setter`去



