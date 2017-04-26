# 第2章 控制结构和函数

##### 

##### 2.1 条件表达式

Scala的每个表达式都有值，比如`val s = if (x > 0) 1 else -1`，s的值是1或-1。

Scala的每个表达式都有一个类型，该类型是各个分支的公共超类型，比如`val s = if (x > 0) "positive" else -1`，`String`和`Int`的公共超类型就是`Any`。

如果else部分缺失了，会用一个`Unit`类来表示else的分支，写作`()`。即`val s = if (x > 0) 1`等同于`val s = if (x > 0) 1 else ()`。可以把`Unit`当做`void`来使用，但从技术上讲，`void`表示无值，`Unit`表示一个“无值”的值。

---

##### 2.2 语句终止

Scala不需要分号，除非在同一行内有多段代码。

当代码很长时，比较好的一个建议是在操作符之后进行换行，这样解释器会知道这不是一个语句的结尾。

---

##### 2.3 块表达式和赋值

在Scala中，{}块包含一系列表达式，其结果也是一个表达式，块中最后一个表达式的值就是块的值。这种特性在一个val值初始化需要很多步骤的时候很有效。

要注意的是，赋值语句是没有值的---其实是一个`Unit`值。所以`x = y = 1`这样的表达式在Scala中是行不通的，x的值是`()`而不是你所期望的1。

---

##### 2.4 输入和输出

Scala有3种输出形式：

* print\("Answer: "\)
* println\(42\)
* C风格的格式化字符串`printlf("Hello, %s! You are %d years old.\n", "Fred", 42)`

Scala有9种输入形式：

* readLine：可带一个参数，作为提示字符串，用来读入一行字符串。
* readInt, readFloat...：共8种，命名均为read+数据类型的形式，用来读入其他数据类型。

---

##### 2.5 循环

Scala的while循环方式与其他语言基本一样。

Scala没有类似Java的for循环（初始化变量;变量是否满足条件;更新变量），只有`for (i <- 表达式)`这种结构，如：

```scala
for (i <- 1 to n) {
  r = r * i
}
```

`1 to n`会返回一个1到n的`Range`（包含1与n），循环会遍历这个集合中的每一个值，如果使用`1 until n`则不会包含上限n。

在这里，并没有对i进行var或val的指定，该变量的类型是集合的元素类型。

Scala没有`break`与`continue`。

---

##### 2.6 高级for循环与推导式

可以用**变量&lt;-表达式**的形式生成多个生成器，用分号隔开。如：

`for (i <- 1 to 3; j <- 1 to 3) print((10 * i + j) + " ")`

每个生成器都可以带一个**守卫**，以if开头的Boolean表达式：

`for (i <- 1 to 3; j <- 1 to 3 if i != j) print((10 * i + j) + " ")`

注意if之前没有分号。

可以使用任意多的定义，引入可以在循环中使用的变量。

`for (i <- 1 to 3; from = 4 - i; j <- from to 3) print((10 * i + j) + " ")`

有时，for语句中的表达式太多，你可以使用{}代替\(\)，并将这些表达式换行：

```scala
for {i <- 1 to 3
     from = 4 - i
     j <- from to 3} {
  print((10 * i + j) + " ")
}
```

如果for循环的循环体以`yield`开始，则该循环会构造出一个集合，每次迭代生成集合中的一个值。

`for (i <- 1 to 10) yield i % 3`

这类循环叫做for推导式，它生成的集合与它的第一个生成器是类型兼容的。

---

##### 2.7 函数

函数由函数名称、参数、函数体构成，必须给出所有的参数类型。

`def abs(x: Double) = if (x >= 0) x else -x`

函数不需要指定返回类型，这是由于语句块具有返回值，Scala可以自己推断函数的返回类型，但递归函数必须指定返回类型。

在学习Scala时，你最好养成函数不写`return`的习惯。

---

##### 2.8 默认参数和带名参数

在Scala中，一个含有默认参数的函数是这样的：

`def decorate(str: String, left: String = "[", right: String = "]") = left + str + right`

如果参数数量不够，默认参数会**从后往前**的被对应（这一点与其他编程语言很不一样）。

和Python一样，你也可以在提供参数的时候指定参数名，带名参数可以是任意的顺序。

`decorate(left = "<<<", str = "Hello", right = ">>>")`

---

##### 2.9 变长参数

类似于Java中的`...`与Python中的`*args`，Scala的函数也可以接收一个变长参数。

```scala
def sum(args: Int*) = {
  var result = 0
  for (arg <- args) result += arg
  result
}
```

调用的方法如下：

`sum(1, 2, 3, 4, 5)`

你可能想传入一个范围的值，但事实上是错误的。

`sum(1 to 5)`

在接收单个参数时，会把参数当做`Int`处理，正确的做法是，追加`_*`符号，让编译器知道该参数是一个参数序列：

`sum(1 to 5: _*)`

---

##### 2.10 过程

对于没有返回值的函数，Scala称之为过程，在表达上，仅仅是略去了函数体之前的=号。

```scala
def addAndPrint(a: Int, b: Int) {
  print(a + b)
}
```

如果执行`val a = addAndPrint(1, 2)`并打印， 你会发现`a`是一个`Unit`值，打印的结果是`()`。

---

##### 2.11 懒值

当val被声明为`lazy`时，它的初始化将被推迟，直到我们首次对它取值（类似于Python中generator的效果）。

`lazy val words = scala.io.Source.fromFile("/usr/share/dict/words").mkString`

如果程序从不访问`words`，那么文件也不会被打开，这个特性对于一些开销大的初始化语句很有用。

---

##### 2.12 异常

Scala没有受检异常。

`throw`表达式有特殊的类型`Nothing`，在if/else表达式中，如果一个分支的类型是Nothing，那么表达式的类型就是另一个分支的类型。

捕获错误采用**模式匹配**的语法：

```scala
try {
  process(new URL("http://horstmann.com/fred-tiny.gif"))
} catch {
  case _: MalformedURLException => println("Bad URL: " + url)
  case ex: IOException => ex.printStackTrace()
}
```

如果你不需要使用捕获的异常对象，可以使用`_`来代替变量名。

