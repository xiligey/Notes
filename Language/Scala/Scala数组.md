## 什么是数组

数组是由相同类型的元素的集合组成的数据结构。

元素与索引相关联，索引通常为整数，用于访问或替换特定元素。

有两种方法来定义数组：指定元素的总数，然后将值分配给元素，或者我们可以一次指定所有值。

## 例子

以下代码显示了如何创建一个可以包含三个元素的字符串数组。

```
var books:Array[String] = new Array[String](3)
```

这里书籍被声明为一个可以容纳三个元素的字符串数组。我们可以简化声明如下。

```
var books = new Array[String](3)
```

我们可以定义books数组并赋值如下。

```
var books = Array("Scala", "Java", "Groovy")

```

我们可以使用如下所示的命令为各个元素赋值或访问各个元素：

```
object Main {
  def main(args: Array[String]) {
    var books = new Array[String](3)
    books(0) = "Scala";
    books(1) = "Java";
    books(2) = "Groovy"
    println(books(0))

  }
}

```

数组的第一个元素的索引是数字0，最后一个元素的索引是元素的总数减去1。