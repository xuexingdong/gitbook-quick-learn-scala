# 第1章 基础

##### 1.1 REPL

全称Read-Eval-Print-Loop，是一种交互式解释器环境，Node.js、Python、Scala等语言的安装包中都附带此种工具。

---

##### 1.2 声明值和变量

在Scala中，`val`关键字用来声明常量，`var`关键字用来声明变量。

可以同时声明多个变量。

可以不指定变量的类型。

```scala
// 不指定类型
val x, y = 100
// 指定类型
var greeting, message: String = null
```

---

##### 1.3 常用类型

Scala有八种基本类型：`Byte`、`Char`、`Short`、`Int`、`Long`、`Float`、`Double`、`Boolean`。

与Java不同的是，这些类型是类。

Scala不刻意区分基本类型和引用类，可以直接对数字执行方法，比如`1.toString()`。

Scala的编译器会自动转换基本类型与包装类。

---

##### 1.4 算术和操作符重载

Scala在进行+-\*/%等操作符的时候，实际上在调用一个方法，例如`a+b`实际上是`a.+(b)。`

事实上，Scala的方法几乎可以是任何符号，并且可以缩写成`a 方法 b`的形式。

---

##### 1.5 调用函数和方法

* `import math._`Scala中的下划线等同于Java的\*，在导入的时候做通配符用。

* 在使用以scala开头的包时，可以忽略scala前缀，无论是import时还是在使用时。

* 不带参数的Scala方法通常不使用圆括号，更一般的说，没有参数且不改变当前对象的方法不带圆括号。

> 在这里补充一下自己对**方法**和**函数**的理解。这两者的区别表现在面向对象的编程中，方法与对象相关，方法中的数据是隐式传递的，可以操作类内部的数据，比如`person.eat()`就是一个方法；而函数与对象无关，类似于`min`、`max`这种通用的函数。通俗点说，在Java中，它们就是普通方法与静态方法的区别。

---

##### 1.6 apply方法

在Scala中，`"Hello"(4)`将产出o，但实际上是调用了`StringOps`的`apply`方法，即等同于`"Hello".apply(4)。`

同样的，`BigInt("123456789")`可以不使用new关键字就创建一个`BigInt`对象，像这样使用伴生对象的`apply`方法来构建对象是Scala的常用手法。

---

##### 1.7 Scaladoc

可以前往`http://www.scala-lang.org/api/current/`浏览Scala的在线API文档。

