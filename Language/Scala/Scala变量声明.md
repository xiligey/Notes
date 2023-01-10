Scala允许您在声明它时确定变量是不可变的（只读的）还是不可变的（读写的）。

不可变的“变量"用关键字 `val` 声明:

```
val array: Array[String] = new Array(5)

```

## 例子

数组元素本身是可变的，因此可以修改元素:

```
object Main {
  def main(args: Array[String]) {

     val array: Array[String] = new Array(5)
     array = new Array(2)
     array(0) = "Hello"
     println(array )
  }
}

```

## 注意

在声明时必须初始化val。

## 可变变量

可变变量用关键字 `var` 声明，并且必须立即初始化。

```
object Main {
  def main(args: Array[String]) {

     var stockPrice: Double = 100.0
     stockPrice = 200.0
     println(stockPrice);
  }
}

```

## 例2

下面的代码定义了一个具有不可变的名字和姓氏，但是一个可变的年龄的Person类。

```
class Person(val name: String, var age: Int)

object Main {
  def main(args: Array[String]) {

     val p = new Person("Dean Wampler", 29)
     println(p.name)
     println(p.age )
     p.age = 30
     println(p.age )

  }
}

```