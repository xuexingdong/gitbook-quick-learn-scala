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

在Java中，我们不鼓励使用公有字段，而是通过`getter`和`setter`去读取或修改属性。在Scala中，我们只需要自己声明字段即可，Scala会自动生成`getter`与`setter`。假设有以下这样一个类：

```scala
class Person {
  var age = 0
}
```

对于`age`字段来说，生成的`getter`与`setter`方法分别叫`age`和`age_=`。

知道了命名规则以后，我们可以选择覆盖`getter`与`setter`：

```scala
class Person {
  private var privateAge = 0

  def age = privateAge

  def age_=(newValue: Int) {
    if (newValue > privateAge) privateAge = newValue
  }
}
```

总结一下，Scala的`getter`与`setter`具有以下规律：

* 如果字段是私有的，则`getter`与`setter`也是私有的。
* 如果字段是`val`，则只有`getter`被生成。
* 如果不需要任何`getter`或`setter`，可以将字段声明为`private[this]`。

---

##### 5.3 只带getter的属性

如果需要一个只读属性，可以使用`val`字段，这样对象在构建完成以后这个属性值就不会再被改变。

有时，我们不希望使用者随意更改某个值，但可以通过其他方式改变。如下：

```scala
class Counter {
  private var value = 0

  def increment() {
    value += 1
  }

  def current = value
}
```

`Counter`的`current`属性在调用`increment`时更新，但没有对应的`setter`。

总结一下，在实现属性时有四种情况：

1. `var foo`：Scala自动合成一个`getter`和`setter`。
2. `val foo`：Scala自动合成一个`getter`。
3. 自定义`foo`和`foo_=`方法。
4. 自定义`foo`方法。

> 可以看出，Scala不支持只有`setter`而没有`getter`的属性。

---

##### 5.4 对象私有字段

在Scala中，方法可以访问一个类的所有对象的私有字段，如：

```scala
class Counter {
  private var value = 0

  def increment() {
    value += 1
  }

  def current = value

  def isLess(other: Counter) = value < other.value
}
```

other也是Counter对象，所以可以被访问到，如果想制定更严格的访问控制，可以采用如下语句：

`private[this] var value = 0`的，

这样一来，Counter类的对象只能访问当前对象的value字段，这样的访问被称为**对象私有**。

---

##### 5.5 Bean属性



