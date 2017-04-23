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



