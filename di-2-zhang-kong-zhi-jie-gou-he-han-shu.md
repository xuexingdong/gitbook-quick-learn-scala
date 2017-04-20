# 第2章 控制结构和函数

##### 

##### 1.1 条件表达式

Scala的每个表达式都有值，比如`val s = if (x > 0) 1 else -1`，值是1或-1.

Scala的每个表达式都有一个类型，该类型是各个分支的公共超类型，比如`val s = if (x > 0) "positive" else -1`，String和Int的公共超类型就是Any。

如果else部分缺失了，会用一个Unit类来表示else的分支，写作\(\)。即`val s = if (x > 0) 1`等同于`val s = if (x > 0) 1 else ()`。可以把Unit当做void来使用，但从技术上讲，void表示无值，Unit表示一个“无值”的值。

