# 第3章 数组相关操作

##### 

##### 3.1 定长数组

构造一个长度不变的数组，使用Scala中的`Array`。

```scala
//    10个整数的数组，元素被初始化为0
val nums = new Array[Int](10)
//    10个字符串数组，元素被初始化为null
val a = new Array[String](10)
//    长度为2的Array[String]，类型是推断出来的，注意没有new
val s = Array("Hello", "World")
//    使用()而不是[]来访问数组
s(0) = "Goodbye"
```

---

##### 3.2 变长数组：数组缓冲

对于长度需要变化的数组，Scala使用`ArrayBuffer`，类似于Java中的`ArrayList`。

```scala
//    初始化一个数组缓冲
val b = ArrayBuffer[Int]()
//    追加元素
b += 1
//    追加多个元素
b += (1, 2, 3, 5)
//    用++=操作符追加任何集合
b ++= Array(8, 13, 21)
//    移除最后5个元素
b.trimEnd(5)
```

在数组缓冲的末端追加或删除都是高效的操作，但在中间插入和删除则需要平移之后的元素。

除此之外，`ArrayBuffer`还提供了许多方便的操作。

```scala
//    在下标2之前插入，变为ArrayBuffer(1, 1, 6, 2)
b.insert(2, 6)
//    在下标2之前插入，变为ArrayBuffer(1, 1, 7, 8, 9, 6, 2)
b.insert(2, 7, 8, 9)
//    移除下标为2的元素，变为ArrayBuffer(1, 1, 8, 9, 6, 2)
b.remove(2)
//    移除下标为2开始的3个元素，变为ArrayBuffer(1, 1, 2)
b.remove(2, 3)
```

如果要将`ArrayBuffer`转为`Array`，可以使用`b.toArray`。

---

##### 3.3 遍历数组和数组缓冲

for循环遍历数组或者数组缓冲：

```scala
for (i <- 0 until a.length) {
  println(a(i))
}
```

如果想跳着取元素：

```scala
  for (i <- 0 until(a.length, 2)) {
    println(a(i))
  }
```

如果想要倒着取元素：

```scala
  for (i <- (0 until a.length).reverse) {
    println(a(i))
  }
```

如果不需要用到下标，可以直接访问数组元素：

```scala
  for (elem <- a) {
    println(elem)
  }
```

---

##### 3.4 数组转换

`for...yield`循环可以创建一个类型与原始集合相同的新集合，例如希望对数组中的偶数翻倍并去掉奇数：

```scala
val a = Array(2, 3, 5, 7, 11)
val result = for (elem <- a if elem % 2 == 0) yield 2 * elem
```

但其实更加符合Scala程序员做法的是以下形式：

`a.filter(_ % 2 == 0).map(2 * _)`

---

##### 3.5 常用算法

在程序中，最常用的运算是求和与排序，Scala有内建的函数来处理这些任务。

`Array(1, 7, 2, 9).sum`对数组或数组缓冲进行求和。要使用`sum`算法，元素类型必须是数值类型，包括整型，浮点型和`BigInteger/BigDecimal`。

`min`与`max`输出数组或数组缓冲中的最小/最大值。

`sorted`方法将数组或数组缓冲排序，并返回新的集合。

```scala
val b = ArrayBuffer(1, 7, 2, 9)
val bSorted = b.sorted(_ < _)
```

也可以直接对数组排序，但不能的对数组缓冲进行排序：

```scala
val a = Array(1, 7, 2, 9)
//    a被修改
scala.util.Sorting.quickSort(a)
```

如果想要显示数组或数组缓冲的内容，使用`mkString`法方法。

```scala
//    指定拼接符
a.mkString(" and ")
//    指定前后缀以及拼接符
a.mkString("<", ",", ">")
```

`Array.toString`打印的是Java对象，`ArrayBuffer.toString`打印的是便于调试的显示值。

---

##### 3.6 解读Scaladoc

对`Array`进行操作时，数组被转换成`ArrayOps`对象，该对象有许多有用的方法，在此省略。

---

##### 3.7 多维数组

与Java一样，多维数组是通过数组的数组来实现的，例如：`Double`类型的二维数组为`Array[Array[Double]]`，要构造这样的数组，可以使用`ofDim`方法：

`val matrix = Array.ofDim[Double](3, 4)`

要访问其中的对象，使用两对括号：

`matrix(row)(column) = 42`

---

##### 3.8 与Java的互操作

使用Scala的隐式转换，你可以使用Scala的Buffer类型，在调用Java方法时，自动转换成Java的List。

Scala调用Java：

```scala
import scala.collection.JavaConversions.bufferAsJavaList
import scala.collection.mutable.ArrayBuffer

val command = ArrayBuffer("ls", "-al", "/home/cay")
//    Scala到Java的转换
val pb = new ProcessBuilder(command)
```

Java调用Scala：

```scala
import scala.collection.JavaConversions.asScalaBuffer
import scala.collection.mutable.Buffer
//    不能使用ArrayBuffer，仅能保证是个Buffer
val cmd: Buffer[String] = pb.command()
```



