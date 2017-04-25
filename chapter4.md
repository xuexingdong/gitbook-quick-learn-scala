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

---

##### 4.3 更新映射中的值

只有可变的映射可以进行值的更新。

`scores("Bob") = 10`



