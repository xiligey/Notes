Scala方法声明具有 `def` 关键字，方法名称，参数，可选返回类型，= 关键字，方法body.myMethod不带参数并返回String:

```
def myMethod():String = "www.w3cschool.cn"

```

`myOtherMethod` 不带参数并返回一个String，但是返回类型没有被显式声明，因为编译器推断返回类型。

```
def myOtherMethod() = "Moof"

```

我们在方法声明的括号内声明参数。参数名称后面必须是参数的类型：

```
def foo(a: Int):String = a.toString

```

我们可以声明多个参数：

```
def f2(a: Int, b:Boolean):String= if (b)a.toString else"false"

```

我们可以传递参数的类型或返回类型作为参数。

下面的代码取一个参数p和类型参数 `T` ，并返回一个`T` 的 `List` 。

因此，如果你传递一个`Int`，你会得到一个`List[Int]`，如果你传递一个`String`，你会得到一个`List[String]`。

```
deflist[T](p:T):List[T] = p :: Nil
list(1)
list("Hello")

```

并且列表中的最后一个参数可以是可变长度参数。

如果最后一个参数是可变长度参数，则它是可变长度参数类型的`Seq`，因此在这种情况下as参数是 `Seq[Int]`：

```
def largest(as: Int*): Int = as.reduceLeft((a, b)=> a max b)

```

可变长度参数方法可以被称为如下：

```
largest(1)
largest(2,3,99)
largest(3,22,33,22)

```

我们可以混合类型参数和可变长度参数：

```
def mkString[T](as: T*):String = as.foldLeft("")(_ + _.toString)

```

我们可以把类型参数的边界。在这种情况下，传入的类型必须是Number或Number的子类：

```
def sum[T <:Number](as:T*): Double = as.foldLeft(0d)(_ + _.doubleValue)

```

方法可以在任何代码范围内声明，除了在顶层，其中声明了类，traits和对象。

方法可以引用它们范围中的任何变量，如下面的代码所示。

```
def readLines(br: BufferedReader) = {
    var ret: List[String] = Nil
    def readAll():Unit= br.readLinematch {
        case null =>
        case s => ret ::= s ; readAll()
    }
    readAll()
    ret.reverse
}
```

覆盖已声明方法的方法必须包含override修饰符。

覆盖抽象方法的方法可以包括覆盖修饰符。

```
abstract class Base {
    def thing: String
}
class One extends Base {
    def thing= "Moof"
}
```

不使用参数和变量的方法可以以同样的方式访问，val可以覆盖超类中的def，如下面的代码所示。

```
class Two extends One{
override val thing= (new java.util.Date).toString
}
class Three extends One{
override lazy val thing= super.thing + (new java.util.Date).toString
}

```

## Call-by-Name

在Scala中，我们可以将参数传递给方法和函数：call-by-name，它将代码块传递给被调用者。

每次被叫方访问参数时，将执行代码块并计算该值。

## 方法调用

Scala为调用方法提供了许多句法变体。

有标准的Java点符号：

```
instance.method()

```

但是如果一个方法不带任何参数，尾括号是可选的：

```
instance.method

```

这允许没有参数方法的方法在目标实例上显示为属性或字段。

采用单个参数的方法可以像Java中一样被调用：

```
instance.method(param)

```

但是可以调用带有单个参数的方法，而不使用圆点或括号：

```
instance.method param

```

因为Scala允许方法名称包含符号，如+， - ，*和？，Scala的点少方法记法创建一个句法中立的方法调用方法，这是Java中的硬编码运算符。

```
object Main {
  def main(args: Array[String]) {
     println(2.1.*(4.3))
     println(2.1* 4.3)
  }
}

```

最后，我们在Java中调用多参数方法：

```
instance.method(p1, p2)

```

如果Scala方法接受一个类型参数，wecan也显式地传递类型参数：

```
instance.method[TypeParam](p1,p2)

```