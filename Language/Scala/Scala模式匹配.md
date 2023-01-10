模式匹配是检查某个值（value）是否匹配某一个模式的机制，一个成功的匹配同时会将匹配值解构为其组成部分。

它是Java中的`switch`语句的升级版，同样可以用于替代一系列的 if/else 语句。

## 语法

---

一个模式匹配语句包括一个待匹配的值，`match`关键字，以及至少一个`case`语句。

## 模式匹配的一般用法

---

```scala
import scala.util.Random

val x: Int = Random.nextInt(10)

x match {
  case 0 => "zero"
  case 1 => "one"
  case 2 => "two"
  case _ => "other"
}
```

上述代码中的`val x`是一个0到10之间的随机整数，将它放在`match`运算符的左侧对其进行模式匹配，`match`的右侧是包含4条`case`的表达式，其中最后一个`case _`表示匹配其余所有情况，在这里就是其他可能的整型值。

`match`表达式具有一个结果值

## 案例类中的模式匹配

---

```scala
abstract class Animal
case class Dog(hobbit: String = "run", speed: String = "slow") extends Animal {
  val age = 10
}
case class Cat(hobbit: String = "sleep", speed: String = "fast") extends Animal

// 根据部分值进行匹配
val cat = Cat()
cat match {
  case Cat("sleep", _) => println("This cat likes sleeping.")
  case Cat(_, "fast") => println("This cat run fast.")
}

// 仅根据类型进行匹配
def printHobbit(animal: Animal): Unit = animal match {
  case d: Dog => println("run")
	case c: Cat => println("sleep")
	case _ => println("nothing")
}

// 模式守卫 （为了让匹配更加具体，可以使用模式守卫，也就是在模式后面加上if语句）
val dog = Dog()
dog match {
  case Dog("sleep", _) if dog.age > 10 => println("This dog is old and it likes sleeping.")
  case Dog(_, "fast") if dog.age > 10 => println("This dog is old but still run fast.")
}
```

## 密封类

---

特质（trait）和类（class）可以用`sealed`标记为密封的，这意味着其所有子类都必须与之定义在相同文件中，从而保证所有子类型都是已知的。

```scala
sealed abstract class Furniture
case class Couch() extends Furniture
case class Chair() extends Furniture

def findPlaceToSit(piece: Furniture): String = piece match {
  case a: Couch => "Lie on the couch"
  case b: Chair => "Sit on the chair"
}
```

这对于模式匹配很有用，因为我们不再需要一个匹配其他任意情况的`case`

## 利用提取器对象的unapply方法来定义非案例类的模式匹配

```scala
import scala.util.Random

object CustomerID {

  def apply(name: String) = s"$name--${Random.nextLong}"

  def unapply(customerID: String): Option[String] = {
    val stringArray: Array[String] = customerID.split("--")
    if (stringArray.tail.nonEmpty) Some(stringArray.head) else None
  }
}

val customer1ID = CustomerID("Sukyoung")  // Sukyoung--23098234908
customer1ID match {
  case CustomerID(name) => println(name)  // prints Sukyoung
  case _ => println("Could not extract a CustomerID")
}
```