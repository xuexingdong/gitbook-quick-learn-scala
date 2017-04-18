# 

# 第1章 基础

##### 

##### 1.1 REPL

全称Read-Eval-Print-Loop，是一种交互式解释器环境，Node.js、Python、Scala等语言都具有这个方便的特性。

##### 

##### 1.2 声明值和变量

```scala
    val x, y = 100
    var greeting, message: String = null
```

##### 

##### 1.3 常用类型

Byte、Char、Short、Int、Long、Float、Double、Boolean，与Java不同的是，这些类型是类。

Scala不可以区分基本类型和引用类，可以自直接对数字执行方法，比如1.toString\(\)。

Scala的编译器会自动转换基本类型与包装类。

##### 

##### 1.4 算术和操作符重载

Scala在进行+-\*/%等操作符的时候，实际上在调用一个方法，例如`a+b`实际上是`a.+(b)。`事实上，Scala的方法几乎可以是任何符号，并且都可以缩写成`a 方法 b`的形式。



