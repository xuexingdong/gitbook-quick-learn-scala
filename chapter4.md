# 第4章 映射和元组



##### 4.1 构造映射

可以这样构造一个映射：

`val scores = Map("Alice" -> 10, "Bob" -> 3, "Cindy" -> 8)`

这样构造出来的Map是不可变的，如果需要一个可变的映射，可以使用：

`val scores = scala.collection.mutable.Map("Alice" -> 10, "Bob" -> 3, "Cindy" -> 8)`

如果想构造一个空的映射，则需要指定参数类型：

`val scores = new scala.collection.mutable.HashMap[String, Int]`

事实上，`"Alice" -> 10`操作符等同于\`\("Alice", 10\)，但前者显然看起来更加直观，更加的Scala。

---

##### 4.2 获取映射中的值

获取映射的时候，使用圆括号：

`val bobScore = scores("Bob")`

但有时候判断映射中是否有指定的键，使用`contains`方法：

`val bobScore = if (scores.contains("Bob")) scores("Bob") else 0`

其实，还有更Scala的写法：

`val bobScore = scores.getOrElse("Bob", 0)`

注意，映射的`get`方法返回的是`Option`对象，在14章中会详细介绍。

---

##### 4.3 更新映射中的值

只有可变的映射可以进行值的更新。

`scores("Bob") = 10`

或者可以使用`+=`操作符来添加多个关系：

`scores += ("Bob" -> 10, "Fred" -> 7)`

要移除某个键和对应的值，使用`-=`操作符：

`scores -= "Alice"`

上述的`+=`与`-=`操作符都是针对可变映射而言的，对于不可变的映射，可以新建一个映射：

`val newScores = score + ("Bob" -> 10, "Fred" -> 7)`

或者使用`var`来声明集合：

```scala
var scores = ...
scores = scores + ("Bob" -> 10, "Fred" -> 7)
scores = scores - "Alice"
```

实际上，这样不停的创建新映射的效率并不会很低，老的映射与新的映射共享大部分结构。

---

##### 4.4 迭代映射

可以通过`for ((k, v) <- 映射)`来遍历映射。

如果只需要访问键或值，可以使用`scores.keySet`或`scores.values`。

反转映射的快速方法：`for ((k, v) <- 映射) yield (v, k)`

---

##### 4.5 已排序映射

Scala的映射实现方式有2种---哈希表与平衡树，默认是哈希表。Scala没有可变的树形映射，如果需要按一定顺序访问所有的键，可以使用`SortedMap`。

`val scores = scala.collection.immutable.SortedMap("Alice" -> 10, "Fred" -> 7, "Bob" -> 3, "Cindy" -> 8)`

如果你需要可变的树形映射，建议使用Java的`TreeMap`。

如果想要按照插入顺序来访问所有键，使用`LinkedHashMap`：

`val scores = scala.collection.immutable.LinkedHashMap("January" -> 1, "February" -> 2, "March" -> 3, ...)`

---

##### 4.6 与Java的互操作

通过隐式转换，可以实现Java与Scala的映射转换。

Java转Scala映射：

```scala
import scala.collection.JavaConversions.mapAsScalaMap

val scores: scala.collection.mutable.Map[String, Int] = new util.TreeMap[String, Int]()
```

Scala转Java映射：

```scala
import scala.collection.JavaConversions.mapAsJavaMap
import java.awt.font.TextAttribute._

val attrs = Map(FAMILY -> "Serif", SIZE -> 12)
val font = new Font(attrs)
```

##### 4.7 元组

元组是不同类型集的聚集，如：

`(1, 3.14, "Fred")`是一个类型为`Tuple3[Int, Double, java.lang.String]`的元组。

通过`_1`、`_2`、`_3`访问元组的组元（注意组元从1开始索引，而不是0）。

可以使用模式匹配来获取元组的组员，如果有不需要的成员，用`_`来代替。

`val (first, second, _) = t`

元组可以用于函数需要返回值不止一个的情况。

##### 4.8 拉链操作

元组可以把多个值绑在一起，通常可以用`zip`方法来完成，举例来说：

```scala
val symbols = Array("<", "-", ">")
val counts = Array(2, 10, 2)
val pairs = symbols.zip(counts)
```

返回的结果是`Array(("<", 2), ("-", 10), (">", 2))`。

用`toMap`方法可以将对偶（二元组）的集合转换成映射：`keys.zip(values).toMap`。

