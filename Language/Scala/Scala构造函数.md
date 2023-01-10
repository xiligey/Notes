类由类成员（如字段和方法）组成。

字段保存对象的状态，并使用 `val` 或 `var` 定义。

方法完成对象的计算任务，并使用定义关键字 `def` 。

在Scala中，类的整个主体是构造函数。

如果构造函数采用零参数，则可以省略参数列表。

Scala区分用val字段，var字段，private val或private var声明的构造函数和没有varor val的字段。

## 参数声明为val

如果构造函数参数声明为val，Scala只为它生成一个getter方法。

让我们声明一个字段为val，如下所示：

```
class Book( val title:String)

```

因为构造函数字段被定义为一个val，所以该字段的值是不可变的。因此，Scala只生成getter方法，没有setter方法。

```
object Main {
  def main(args: Array[String]) {
    class Book( val title:String)
    val book = new Book("Scala")

    println(book);
    println(book.title )
    //book.title = "new title"  //Error
  }
}

```

在Scala中，如果构造函数或方法采用零参数，则可以省略参数列表。

## 参数声明为var

如果构造函数参数声明为var，Scala将生成访问器和mutator方法。

```
class Book( var title:String)

```

所以当你设置字段时，像这样

```
book.title("new title")

```

我们可以改变Book对象的字段，因为它是用关键字var声明的。

```
object Main {
  def main(args: Array[String]) {
    class Book( var title:String)
    val book = new Book("Beginning Scala")
    book.title = "new title"
    println(book.title )
  }
}

```

## 参数声明为私有val或var

您可以将 `private` 关键字添加到 `val` 或 `var` 字段，以防止getter和setter方法生成。

在这种情况下，字段只能从类的成员内访问：

```
class Book(private var title: String) {
    def printTitle {
       println(title)
    }
}

val book = new Book("Beginning Scala")
println(book.printTitle )

```

## 参数声明没有val或var

当在构造函数参数上未指定val和var时，Scala不生成getter或setter。

正如你在这里可以看到的，你不能访问书的字段标题。

```
class Book(title: String)
val book = new Book("Beginning Scala")
//book.title //Error

```

## 例子

这里是`Book`类，一个名为title的构造函数参数，默认值为“Scala”。

因为参数使用默认值定义，您可以调用构造函数而不指定标题值：

```
class Book (val title: String = "Scala")
val book = new Book
book.title

```

您还可以在创建新图书时指定所选的标题值：

```
val book = new Book("new title")
book.title

```

您还可以选择提供命名参数，如以下代码所示：

```
val book = new Book(title="Beginning Scala")
book.title

```

## 辅助构造函数

我们可以为类定义一个或多个辅助构造函数，以提供创建对象的不同方法。

辅助构造函数通过创建名为this的方法来定义。

我们可以定义多个辅助构造函数，但它们必须有不同的签名。

每个辅助构造函数必须以对先前定义的构造函数的调用开始。

以下代码说明了一个主构造函数和两个辅助构造函数。

```
class Book (var title :String, var ISBN: Int) {
    def this(title: String) {
        this(title, 2222)
    }
    def this() {
        this("CSS")
        this.ISBN = 1111
    }
    override def toString = s"$title ISBN- $ISBN"
}

```

给定这些构造函数，可以通过以下方式创建同一本书：

```
val book1 = new Book
val book2 = new Book("Clojure")
val book3 = new Book("Scala", 3333)

```

辅助构造函数只需要调用先前定义的构造函数之一。