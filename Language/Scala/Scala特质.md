

特质 (Traits) 用于在类 (Class)之间共享程序接口 (Interface)和字段 (Fields)。 它们类似于Java 8的接口。

-   类和对象 (Objects)可以扩展特质，但是特质不能被实例化，因此特质没有参数。
-   在Scala中，当一个类从trait继承时，它实现trait的接口，并继承trait中包含的所有代码。
-   在Scala中，traits可以继承类。
-   当一个类继承一个trait作为其父类时，也使用关键字extends。
-   即使当类使用with关键字在其他traits中混合时，也使用关键字extends。
-   此外，当一个trait是另一个trait或类的子对象时使用extends。

## 定义一个特质


```scala
trait running {
  def run(): Unit = println("running")
}

// 使用 extends 关键字来扩展特质
class Dog extends running {

}
```

## 带泛型的特质

---

特质作为泛型类型和抽象方法非常有用：

```scala
trait Iterator[A] {
  def hasNext: Boolean
  def next(): A
}
```

## 类继承特质

---

```scala
class IntIterator(to: Int) extends Iterator[Int] {
  private var current = 0

  // 使用 override 关键字来实现trait里面的任何抽象成员
  override def hasNext: Boolean = current < to
  override def next(): Int =  {
    if (hasNext) {
      val t = current
      current += 1
      t
    } else 0
  }
}
```

## 类混入特质

---

当某个特质被用于组合类时，被称为混入，使用关键词with实现混入。

```scala
trait A
trait B
class C
// 类D继承类C混入特质A
class D extends C with A
// 类F继承类C混入特质A和特质B
class F extends C with A with B
// 类E继承特质B混入特质A
class E extends B with A
```

---

## 特质继承特质

```scala
trait A
trait B
trait C extends A
trait D extends B
```

## 特质混入特质

---

```scala
trait A
trait B
trait C extends A
trait D extends B
// 特质E继承特质A混入特质B
trait E extends A with B
class F 
// 特质G继承类F混入特质A和特质B
trait G extends F with A with B
```

## 子类型

---

凡是需要特质的地方，都可以由该特质的子类型来替换（class ClassA extends TraitB，则可认为ClassA为TraitB的子类）

```scala
import scala.collection.mutable.ArrayBuffer

trait Pet {
  val name: String
}

class Cat(val name: String) extends Pet
class Dog(val name: String) extends Pet

val dog = new Dog("Harry")
val cat = new Cat("Sally")

val animals = ArrayBuffer.empty[Pet]
animals.append(dog)
animals.append(cat)
animals.foreach(pet => println(pet.name))
```

在这里 `trait Pet` 有一个抽象字段 `name` ，`name` 由Cat和Dog的构造函数中实现。

最后一行，我们能调用`pet.name`的前提是它必须在特质Pet的子类型中得到了实现。