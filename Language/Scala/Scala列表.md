在Scala列表中，所有元素都具有类似数组的类型，但与数组不同，列表的元素不能通过赋值进行更改。

具有类型T的元素的列表被写为List [T]。

有两种方法来创建列表：

-   以与创建数组类似的方式创建列表
-   use :: cons运算符。

## 例子

首先我们将展示更传统的方法。以下代码显示了如何创建空列表。

```scala
val empty: List[Nothing] = List()
```

注意，列表的类型是Nothing。

我们可以创建如下列代码所示的书籍列表：

```scala
val books: List[String] = List("Scala", "Groovy", "Java")
```

这两个列表可以使用tail`Nil`和`::`定义。

Nil也表示空列表。

可以使用Nil定义空列表。

```scala
val empty = Nil
```

书籍列表可以使用尾部Nil和::定义，如下面的代码所示。

```scala
val books = "Scala" :: ("Groovy" :: ("Java" :: Nil))
```

列表上的操作可以用head和tail方法表示，其中head返回列表的第一个元素，tail返回一个由除第一个元素之外的所有元素组成的列表。