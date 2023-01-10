### 1 scala介绍一下

Scala 是一种多范式语言，它一方面吸收继承了多种语言中的优秀特性，一方面又没有抛弃 Java 这个强大的平台，它运行在 Java 虚拟机 (Java Virtual Machine) 之上，轻松实现和丰富的 Java 类库互联互通。它既支持面向对象的编程方式，又支持[函数式编程](https://www.zhihu.com/search?q=%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)。它写出的程序像动态语言一样简洁，但事实上它确是严格意义上的[静态语言](https://www.zhihu.com/search?q=%E9%9D%99%E6%80%81%E8%AF%AD%E8%A8%80&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)，相对于Java而言，Scala的代码更为精简（减低犯错），而且功能更为广泛（Scala其实是Scalable Language 的简称，意为可扩展的语言），许多Scala的特性和语法都是针对Java的不足和弱点来设计的。

### 2 关于scala，你有什么想说的吗？scala可以用在哪些方面呢？

Scala的特点是有很多函数程式语言的特性（例如ML，Miranda, Scheme，Haskell），譬如惰性求值，list comprehension, type inference, anonymous function, pattern matching 等等，同时也包含 Object-Oriented 的特性（OO 能与 FP 混合使用是 Scala 的亮点）。此外，许多相似于高级编程语言的语法也渗入其中（例如 Python），不仅提高了 Scala 代码的可读性，维护、修改起来也较为省时省力。

[scala语言](https://www.zhihu.com/search?q=scala%E8%AF%AD%E8%A8%80&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)主要在于Spark开发中进行使用，代码编写简洁方便，并且执行效率很高，相比较Java语言来说，代码可以减少几倍，还很灵活。

### 3 scala懒加载问题怎么处理？

使用Lazy关键字进行懒加载操作

在一些情况中我们经常希望某些变量的初始化要延迟，并且表达式不会被重复计算。就像我们用Java实现一个懒汉式的单例。如：

```
打开一个数据库连接。这对于程序来说，执行该操作，代价式昂贵的，所以我们一般希望只有在使用其的引用时才初始化。（当然实际开发中用的是连接池技术）
为了缩短模块启动时间，可以将当前不需要的某些工作推迟执行。
保证对象中其他字段的初始化能优先执行。
```

### 4 Scala有break吗，Case class了解吗，哪里用到过？

Scala没有break操作，但是可以实现break原理，需要创建Breaks对象实现内部的break方法就可以像java一样跳出语句，但是在模式匹配过程中不需要跳出匹配模式，因为模式匹配只能匹配其中一个结果值。

case class代表样例类，它和class类比较来说，可以不需要序列化，而class需要序列化操作，和object很类似，但是不同的是object不能传入参数，而case class可以带入参数，一般在做转换操作传参使用，比如DataSet操作的时候，转换RDD或者DataFream操作时候，可以使用case class进行参数的传递。

### 5 元组

1.  元组的创建

```
val tuple1 = (1, 2, 3, "heiheihei")

println(tuple1)
```

1.  元组数据的访问，注意元组元素的访问有下划线，并且访问下标从1开始，而不是0

```
val value1 = tuple1._4

println(value1)
```

1.  元组的遍历

```
方式1：
for (elem <- tuple1.productIterator  ) {
   print(elem)
}
方式2：
tuple1.productIterator.foreach(i => println(i))
tuple1.produIterator.foreach(print(_))
```

### 6 隐式转换

隐式转换函数是以implicit关键字声明的带有单个参数的函数。这种函数将会自动应用，将值从一种类型转换为另一种类型。

```
implicit def a(d: Double) = d.toInt
// 当执行这句代码的时候，内部会自动调用我们自己编写好的隐式转换方法
val i1: Int = 3.5
println(i1)
```

### 7 隐式转换应用场景

在scala语言中，隐式转换一般用于类型的隐式调用，亦或者是某个方法内的局部变量，想要让另一个方法进行直接调用，那么需要导入implicit关键字，进行隐式的转换操作，同时，在Spark Sql中，这种隐式转换大量的应用到了我们的DSL风格语法中，并且在Spark2.0版本以后，DataSet里面如果进行转换RDD或者DF的时候，那么都需要导入必要的隐式转换操作。

### 8 什么叫闭包

一个函数把外部的那些不属于自己的对象也包含(闭合)进来。

通俗的来说就是[局部变量](https://www.zhihu.com/search?q=%E5%B1%80%E9%83%A8%E5%8F%98%E9%87%8F&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)当全局变量来使用！！！

```
案例1：

def minusxy(x: Int) = (y: Int) => x - y

这就是一个闭包：

1) 匿名函数(y: Int) => x -y嵌套在minusxy函数中。

2) 匿名函数(y: Int) => x -y使用了该匿名函数之外的变量x

3) 函数minusxy返回了引用了局部变量的匿名函数

案例2

def minusxy(x: Int) = (y: Int) => x - y

val f1 = minusxy(10)

val f2 = minusxy(10)

println(f1(3) + f2(3))

此处f1,f2这两个函数就叫闭包。
```

### 9 解释一下Scala内的Option类型

在Scala语言中，Option类型是一个特殊的类型，它是代表有值和无值的体现，内部有两个对象，一个是Some一个是None，Some代表有返回值，内部有值，而None恰恰相反，表示无值，比如，我们使用Map集合进行取值操作的时候，当我们通过get取值，返回的类型就是Option类型，而不是具体的值。

### 10 解释一下什么叫偏函数

偏函数表示用{}包含用case进行类型匹配的操作，这种操作一般用于匹配唯一的属性值，在Spark中的算子内经常会遇到，例

```
val rdd = sc.textFile(路径)
rdd.map{
    case (参数)=>{返回结果}
}
```

### 11 手写Scala单例模式

单例模式是一种常用的软件设计模式。在它的核心结构中只包含一个被称为单例的特殊类。通过单例模式可以保证系统中一个类只有一个实例。

```
/
  * scala中关于单例的模拟
  * object中的属性和方法都可以当做类似java中的静态成员，都可以通过
  * object.成员来进行调用
  */
object SingletonOps {
  def main(args: Array[String]): Unit = {
    val singleton1 = Singleton.getInstance
    val singleton2 = Singleton.getInstance
    println(singleton1 == singleton2)
    singleton1.index = 5
    println("singleton1.index： " + singleton1.index)
    println("singleton2.index： " + singleton2.index)
  }
}

object Singleton {
  private val singleton = Singleton;
  def getInstance = singleton
  var index = 1
}
```

定义：柯里化指的是将原来接受两个参数的函数变成新的接受一个参数的函数的过程。新的函数返回一个以原有的第二个参数作为参数的函数

例如：

```
def mul(x:Int,y:Int) = x * y  //该函数接受两个参数
def mulOneAtTime(x:Int) = (y:Int) => x * y  //该函数接受一个参数生成另外一个接受单个参数的函数
这样的话，如果需要计算两个数的乘积的话只需要调用：
mulOneAtTime(5)(4)
这就是函数的柯里化
```

### 13 Scala中的模式匹配和Java的匹配模式的区别

scala的模式匹配包括了一系列的备选项，每个替代项以关键字大小写为单位，每个替代方案包括一个模式或多个表达式，如果匹配将会进行计算，箭头符号=>将模式与表达式分离

例如:

```
obj match{
　　　　　　case 1 => "one"
　　　　　　case 2 => "two"
　　　　　　case 3 => "three"
　　　　　　case _ => default
　　　　}

```

而Java的匹配模式是switch case匹配方式，它内部匹配的类型有局限性，并且需要用Break跳出匹配模式，而Scala中只会匹配其中一个结果，同时匹配类型居多，如String、Array、List、Class等..

### 14 Scala中的伴生类和伴生对象是怎么一回事

在scala中，[单例对象](https://www.zhihu.com/search?q=%E5%8D%95%E4%BE%8B%E5%AF%B9%E8%B1%A1&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)与类同名时，该对象被称为该类的伴生对象，该类被称为该对象的伴生类。

伴生类和伴生对象要处在同一个源文件中

伴生对象和伴生类可以互相访问其私有成员

不与伴生类同名的对象称之为孤立对象

### 15 谈谈Scala的尾递归

正常得递归，每一次递归步骤，需要保存信息到堆栈中去，当递归步骤很多的时候，就会导致内存溢出

而尾递归，就是为了解决上述的问题，在尾递归中所有的计算都是在递归之前调用，编译器可以利用这个属性避免堆栈错误，尾递归的调用可以使信息不插入堆栈，从而优化尾递归

例如:

```
5 + sum(4) // 暂停计算 => 需要添加信息到堆栈
5 + (4 + sum(3))
5 + (4 + (3 + sum(2)))
5 + (4 + (3 + (2 + sum(1))))
5 + (4 + (3 + (2 + 1)))
15
tailSum(4, 5) // 不需要暂停计算
tailSum(3, 9)
tailSum(2, 12)
tailSum(1, 14)
tailSum(0, 15)
15
```

### 16 函数中 Unit是什么意思？

Scala中的Unit类型类似于java中的void，无返回值。主要的不同是在Scala中可以有一个Unit类型值，也就是（），然而java中是没有void类型的值的。除了这一点，Unit和void是等效的。一般来说每一个返回void的java方法对应一个返回Unit的Scala方法。

### 17 Scala中的to和until 有什么区别？

例如1to10，它会返回Range（1,2,3,4,5,6,7,8,9,10），而1until 10 ，它会返回Range（1,2,3,4,5,6,7,8,9）

也就是说to包头包尾，而until 包头不包尾！

### 18 var，val和def三个关键字之间的区别？

var是变量声明关键字，类似于Java中的变量，[变量值](https://www.zhihu.com/search?q=%E5%8F%98%E9%87%8F%E5%80%BC&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)可以更改，但是变量类型不能更改。 val常量声明关键字。 def 关键字用于创建方法（注意方法和函数的区别） 还有一个lazy val（[惰性val](https://www.zhihu.com/search?q=%E6%83%B0%E6%80%A7val&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)）声明，意思是当需要计算时才使用，避免重复计算

```
代码示例：
var x = 3 //  x是Int类型
x = 4      //
x = "error" // 类型变化，编译器报错'error: type mismatch'
val y = 3
y = 4        //常量值不可更改，报错 'error: reassignment to val'
def fun(name: String) = "Hey! My name is: " + name
fun("Scala") // "Hey! My name is: Scala"
//注意scala中函数式编程一切都是表达式
lazy val x = {
  println("computing x")
  3
}
val y = {
  println("computing y")
  10
}
x+x  //
y+y  // x 没有计算, 打印结果"computing y"

```

### 19 trait（特质）和abstract class（抽象类）的区别？

（1）一个类只能集成一个抽象类，但是可以通过with关键字继承多个特质；

（2）抽象类有带参数的构造函数，特质不行（如 trait t（i：Int）{} ，这种声明是错误的）

### 20 unapply 和apply方法的区别， 以及各自使用场景？

先讲一个概念——提取器，它实现了构造器相反的效果，构造器从给定的参数创建一个对象，然而提取器却从对象中提取出构造该对象的参数，scala标准库预定义了一些提取器，如上面提到的样本类中，会自动创建一个伴生对象（包含apply和unapply方法）。 为了成为一个提取器，[unapply方法](https://www.zhihu.com/search?q=unapply%E6%96%B9%E6%B3%95&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A129809632%7D)需要被伴生对象。 apply方法是为了自动实现样本类的对象，无需new关键字。

Null是一个trait（特质），是所以引用类型AnyRef的一个子类型，null是Null唯一的实例。

Nothing也是一个trait（特质），是所有类型Any（包括值类型和引用类型）的子类型，它不在有子类型，它也没有实例，实际上为了一个方法抛出异常，通常会设置一个默认返回类型。

Nil代表一个List空类型，等同List[Nothing]

None是Option monad的空标识

### 22 call-by-value和call-by-name求值策略的区别？

（1）call-by-value是在调用函数之前计算；

（2） call-by-name是在需要时计算

```
示例代码
//声明第一个函数
def func(): Int = {
  println("computing stuff....")
  42 // return something
}
//声明第二个函数，scala默认的求值就是call-by-value
def callByValue(x: Int) = {
  println("1st x: " + x)
  println("2nd x: " + x)
}
//声明第三个函数，用=>表示call-by-name求值
def callByName(x: => Int) = {
  println("1st x: " + x)
  println("2nd x: " + x)
}
//开始调用
//call-by-value求值
callByValue(func())
//输出结果
//computing stuff....
//1st x: 42
//2nd x: 42
//call-by-name求值
callByName(func())
//输出结果
//computing stuff....
//1st x: 42
//computing stuff....
//2nd x: 42
```

### 23 yield如何工作？comprehension（推导式）的语法糖是什么操作？

yield用于循环迭代中生成新值，yield是comprehensions的一部分，是多个操作（foreach, map, flatMap, filter or withFilter）的composition语法糖。

comprehension（推导式）是若干个操作组成的替代语法。如果不用yield关键字，comprehension（推导式）可以被forech操作替代，或者被map/flatMap，filter代替。

```
示例代码：
// 三层循环嵌套
for {
  x <- c1
  y <- c2
  z <- c3 if z > 0
} yield {...}
//上面的可转换为
c1.flatMap(x => c2.flatMap(y => c3.withFilter(z => z > 0).map(z => {...})))
```

高阶函数指能接受或者返回其他函数的函数，scala中的filter map flatMap函数都能接受其他函数作为参数。

### 25 scala全排序过滤字段，求 1 to 4 的全排序， 2不能在第一位， 3,4不能在一起

```
  import util.control.Breaks._

  - 1 to 4 的全排序
  - 2不能在第一位
  - 3,4不能在一起
   object LocalSpark extends App{
      override def main(args: Array[String]): Unit = {
      List(1,2,3,4).permutations.filter(list=>list(0) != 2).map(list=>{
      var num =0
      breakable{
      for(x<- 0 to (list.size-1)){
      if(list(x)==3 && x<3 && list(x+1)==4) break
      if(list(x)==3 && x>0 && list(x-1)==4) break
      num +=1
      }
      }
      if(num <4){
      List()
      }else{
      list
      }
      }).filter(list=>list.size>3).foreach(println(_))
      }
      }

  结果
  List(1, 3, 2, 4)
  List(1, 4, 2, 3)
  List(3, 1, 2, 4)
  List(3, 1, 4, 2)
  List(3, 2, 1, 4)
  List(3, 2, 4, 1)
  List(4, 1, 2, 3)
  List(4, 1, 3, 2)
  List(4, 2, 1, 3)
  List(4, 2, 3, 1)
```