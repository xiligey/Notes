
类是创建对象的蓝图，对象是类的具体实例。

类定义包括字段声明和方法定义。

字段用于存储对象的状态，方法可以提供对字段的访问，并更改对象的状态。

## 定义一个Scala类


1.  最简单的方式：
    
    ```scala
    class Book
    ```
    
    以上方式等价于以下Java代码（Scala修饰符和Java的基本一致，具体使用见 [Scala修饰符](https://www.notion.so/Scala-d76644fb9f2d4e579eb95d636624b6ee) ）
    
    ```java
    public class Book {
    
    }
    ```
    
2.  添加一些属性和方法
    
    ```scala
    class Book {
      var name: String = ""
      def changeName(newName: String): Unit = {
        this.name = newName
      }
    }
    ```
    

## 创建一个Scala对象

---

定义类后，您可以使用关键字new创建类中的对象。

```scala
// 以下二者等价
val book = new Book
val book2 = new Book()
```

调用方法：

```java
book.changeName("三国演义")
println(book.name)
```

## 构造器

---

### 默认构造器

```scala
class Student {

}
```

`Student` 类没有定义任何构造器，因此只有一个默认的不带任何参数的构造器。

### 自定义构造器

```scala
class Student(name: String, id: Int, city: String, country: String) {

}
```

### 带默认值的构造器

构造器可以通过提供一个默认值来拥有可选参数：

```scala
class Student(name: String, id: Int, city: String = "BeiJing", country: String = "China") {

}
```

创建对象时可以省略默认参数项：

```scala
val s1 = Student("张三", 1)
val s2 = Student("Jack", 2, "New York", "America")
val s3 = Student("陈二", 3, "ShangHai")
```

## 私有成员及其Getter/Setter方法

---

-   类中的成员默认是public(公有)的，外部可以访问（如job）
-   加上private即为私有成员（如sex、_hobby）
-   规范：私有成员命名时以_开头，好让别人一看就知道是私有成员（如_hobby）
-   私有成员也分常量（如sex）和变量（如_hobby），常量只可以有getter方法，而变量可以有getter和setter方法
-   不带`val`或`var`的参数是私有的，仅在类中可见（如name、id、city、country）

```scala
class Student(name: String, id: Int, city: String = "BeiJing", country: String = "China") {
  
	val job: String = "coding farmer"
  // 私有成员(不可变，只有getter方法，没有setter方法)
  private val sex: String = "male"
  // 私有成员(可变，有getter和setter方法)
  private var _hobby: String = "swim"

  // _hobby的get方法(不必和Java一致使用getHobby)
  def hobby = _hobby
  // _hobby的set方法(Scala语法：在get方法名后加上_=则为set方法)
  def hobby_= (newHobby: String) = {
    _hobby = newHobby
  }
}
```