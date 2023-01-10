Scala支持单继承，而不是多重继承。

子类可以只有一个父类。

Scala类层次结构的根是Any，没有父类。

```
class Vehicle (speed : Int){
    val mph :Int = speed
    def race() = println("Racing")
}

```

Vehicle类采用一个参数，即车辆的速度。

创建类Vehicle的实例时，必须传递此参数，如下所示：

```
new Vehicle(100)

```

该类包含一个方法，称为`race`。

## 扩展类

在Scala中扩展基类类似于在Java中扩展，除了两个限制：

-   方法覆盖需要`override`关键字，
-   只有主构造函数可以将参数传递给基础构造函数。

可以覆盖从Scala中的超类继承的方法，如下所示：

```
class Car (speed : Int) extends Vehicle(speed) {
    override val mph: Int= speed
    override def race() = println("Racing Car")
}

```

类 `Car` 使用关键字 `extends` 扩展 `Vehicle` 类。

字段mph和方法种族需要使用关键字覆盖来覆盖。

## 注意

以下代码显示了另一个类`Bike`扩展`Vehicle`。

```
class Vehicle (speed : Int){
    val mph :Int = speed
    def race() = println("Racing")
}

class Car (speed : Int) extends Vehicle(speed) {
    override val mph: Int= speed
    override def race() = println("Racing Car")

}
class Bike(speed : Int) extends Vehicle(speed) {
    override val mph: Int = speed
    override def race() = println("Racing Bike")
}
object Main extends App {
    val vehicle1 = new Car(200)
    println(vehicle1.mph )
    vehicle1.race()
    val vehicle2 = new Bike(100)
    println(vehicle2.mph )

}

```