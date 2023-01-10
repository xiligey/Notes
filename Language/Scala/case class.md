## 什么是案例类

---

Scala案例类似于常规类，但它**适合于对不可变数据进行建模**。它在模式匹配中也很有用，这样的类有一个默认的apply()方法来处理对象构造。scala case类也有所有的val属性，这意味着它们是不可变的。

## 案例类的特点

---

-   不仅提供了普通类相同的功能，还自带copy等方法
-   有一个默认的apply()方法来处理对象构造，实例化一个案例类的时候 不需要用new语句
-   案例类的构造函数中的所有参数都是案例类的属性（默认属性都是public val类型，可手动改为var）
-   案例类支持模式匹配功能
-   案例类非常适用于不可变的数据
-   案例类在比较的时候是按值比较而非按引用比较

## 示例

---

### 创建案例类Student（属性都是public val类型）

```scala
case class Student(name: String, age: Int)
// 实例化Student 不需要使用new
val s1 = Student("Jack", 12)
// 构造函数的参数都是属性
println(s1.name, s1.age)
```

### 创建案例类Job（手动将属性改为var类型）

```scala
case class Job(var title: String, var salary: Double)
val j1 = Job("coding farmer", 5)
j1.title = "IT" // 修改属性的值
j1.salary *= 1.2
```

### 创建案例类Car（手动将属性改为private）

```scala
case class Car(private val color: String, private var price: Double)
```

### 案例类用于模式匹配

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

### 比较两个案例类

```scala
case class logger(logLevel: String)
val l1 = logger("info")
val l2 = logger("info")

println(l1 == l2) // tru
```

### 拷贝一个案例类，同时指定部分构造参数做一些改变

```scala
case class logger(var logLevel: String, var logIds: Seq[Int])
var x = Seq(1,2,3)
val l1 = logger("info", x)
val l2 = l1.copy(logLevel = "warn")
```