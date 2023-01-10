Scala中的if表达式的结果始终为Unit。

if/else的结果基于表达式的每个部分的类型。

## 例子

以下代码说明了Scala中的表达式。

```scala
if (exp) println("yes")

```

如果exp是true，上面的代码打印“是”。

像Java一样，if表达式可能有一个多行代码块。

```scala
if (exp) {
    println("Line one")
    println("Line two")
}
```

Scala中的if/else在Java中的行为类似于三元运算符：

```
val i: Int = if (exp) 1 else 3

```

并且表达式的任一（或两者）部分可以具有如下面代码中所示的多行代码块。

```
val i: Int = if (exp)
                1
             else {
                val j = System.currentTimeMillis
                (j % 100L).toInt
             }

```