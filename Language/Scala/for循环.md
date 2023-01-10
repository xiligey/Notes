A For Comprehension是一个非常强大的Scala语言的控制结构。

它提供了迭代集合的能力，它还提供过滤选项和生成新集合的能力。

让我们从表达式的基本开始：

```scala
object Main {
	def main(args: Array[String]) {
		val dogBreeds = List("A", "B", "C", "D", "E", "F")
		for (breed <- dogBreeds) println(breed)
	}
}
```

Expression的Basic是`for`表达式的一个非常基本的特性。

首先，我们需要一个用于表达式将迭代的集合。我们创建一个书籍列表，如下面的代码所示：

```scala
val books = List("Scala", "Groovy", "Java", "SQL", "CSS")
```

现在我们可以写一个非常基本的表达式来遍历图书列表。

```scala
object Main {
  def main(args: Array[String]) {
    val books = List("Scala", "Groovy", "Java", "SQL", "CSS")
    for (book<-books)
       println(book)
  }
}
```

在上面的代码中`for`表达式为列表书中的每个元素创建一个名为book的临时变量以及该元素的相应值。

左箭头操作符称为生成器，因为它从表达式中使用的集合生成相应的值。

## 生成器表达式

表达式`breed <- dogBreeds`称为生成器表达式，因此命名是因为它从集合中生成单个值。

左箭头运算符（< - ）用于遍历一个集合，例如List。

我们还可以使用它与范围来写一个更传统的寻找循环：

```scala
object Main {
  def main(args: Array[String]) {
     for (i <- 1 to 10) println(i)
  }
}
```

## 约束: 过滤值

我们可以添加`if`表达式来过滤我们想要保留的元素。

这些表达式称为约束。

要找到我们的狗品种列表中的所有D，我们修改前面的例子如下：

```
object Main {
  def main(args: Array[String]) {
     val dogBreeds = List("D", "Y", "D", "S", "G", "P")
     for (breed <- dogBreeds
       if breed.contains("D")
     ) println(breed)
  }
}
```

您可以有多个约束：

```
object Main {
  def main(args: Array[String]) {
     val dogBreeds = List("D", "Y", "D", "S", "G", "P")

     for (breed <- dogBreeds
       if breed.contains("D")
       if  !breed.startsWith("Y")
     ) println(breed)

     for (breed <- dogBreeds
       if breed.contains("D") &&  !breed.startsWith("Y")
     ) println(breed)

  }
}
```

过滤器是for表达式中的if子句，用于过滤集合，当我们不想遍历整个集合时。

以下代码显示如何在我们的书籍列表中查找所有Scala图书。

```
object Main {
  def main(args: Array[String]) {
    val books = List("Scala", "Groovy", "Java", "SQL", "CSS")
    for(book<-books
        if book.contains("Scala")
    ) println(book)
  }
}
```

## 可变绑定

我们可以为表达式定义变量。

然后我们可以在你的for表达式的正文中重用这些变量。

```
object Main {
  def main(args: Array[String]) {
    val books = List("Scala", "Groovy", "Java", "SQL", "CSS")
    for {
        book <- books
        bookVal = book.toUpperCase()
    } println(bookVal)
  }
}
```

`bookVal`没有声明为val，但是你仍然可以重用它。

## Yielding

在Scala的for表达式中，我们可以使用yield关键字来生成新的集合。

从for表达式生成的集合的类型从迭代的集合的类型推断。

要在for循环中将值赋给我们的程序的另一部分，请使用`yield`关键字为表达式生成新的集合。

```scala
object Main {
  def main(args: Array[String]) {
     val dogBreeds = List("D", "Y", "D", "S", "G", "P")
     val filteredBreeds = for {
       breed <- dogBreeds
       if breed.contains("T") &&  !breed.startsWith("Y")
     } yield breed
  }
}
```

以下代码显示如何对集合使用yield。

```
object Main {
  def main(args: Array[String]) {
    val books = List("Scala", "Groovy", "Java", "SQL", "CSS")
    var scalabooks = for{
        book <-books
        if book.contains("Scala")
    }yield book

    println(scalabooks);
  }
}
```

过滤的结果作为名为`book`的值生成。

这个结果是在for循环中每次运行时累积的，因此累积的集合被分配给值scalabooks。

scalabook是List [String]类型，因为它是图书列表的一个子集，也是List [String]类型。

## 扩展范围和值定义

用于解释的Scala可以在`for`表达式的第一部分中定义可用于后面表达式的值，如下例所示：

```
object Main {
  def main(args: Array[String]) {
     val dogBreeds = List("D", "Y", "D", "S", "G", "P")
     for {
       breed <- dogBreeds
       upcasedBreed = breed.toUpperCase()
     } println(upcasedBreed)
  }
}
```