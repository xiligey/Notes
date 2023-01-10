在 Scala 中，元组是一个可以容纳不同类型元素的类。

-   元组是不可变的。
-   与列表和数组不同，没有办法迭代元组中的元素，它的目的只是作为一个多个值的容器
-   元组在需要组合离散元素并提供结构化数据的通用方法时非常有用

## 创建元组

```scala
val t1 = ("1.1", 1.2)
val t2: Tuple2[String, Double] = ("1.1", 1.2)
val t3: (String, Double) = ("1.1", 1.2)
val t4 = ("1.1", 1.2): (String, Double) 
val t5 = "1.1" -> 1.2
```

## 访问元素

---

元组的元素访问从1开始计（tuple._i, i=1,2,3,...）

```scala
val t6 = (1, 2, 3, 4, 5, 6, 7)
println(t6._1) // 1
println(t6._6) // 6
```

## 元组解构

---

元组解构用于批量赋值：

```scala
val t7 = ("chenxilin", "XinYu")
val (name, city) = t7
```

<aside> ⚠️ 注意：如果 写成了 `val name, city = t7`, 则name和city都会被赋值为("chenxilin", "XinYu")

</aside>

元组解构用于模式匹配：

```scala
val distances = List(("Mercury", 57.9), ("Venus", 108.2), ("Earth", 149.6), ("Mars", 227.9), ("Jupiter", 778.3))
distances.foreach {
  tuple => {
    tuple match {
      case ("Mercury", 57.9) => println("1")
      case p if (p._2 > 500) => println("2")
      case p if (p._2 > 300) => println("3")
      case _ => println("4")
    }
  }
}
```