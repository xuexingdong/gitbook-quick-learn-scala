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





