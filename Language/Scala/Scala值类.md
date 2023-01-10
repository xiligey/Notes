使用值类，Scala允许扩展 `AnyVal` 的用户定义的值类。

Scala 值类使我们能够在Scala类型层次结构的AnyVal一侧编写类。

Scala中的值类不分配运行时对象。

值类允许我们将扩展方法添加到类型，而不需要创建实例的运行时开销。

这是通过定义新的AnyVal子类来实现的。

## 例子

下面说明了一个值类定义：

```
class SomeClass(val underlying: Int) extends AnyVal

```

前面的SomeClass类有一个单一的公共val参数，它是基础运行时表示。

编译时的类型是`SomeClass`，但在运行时，表示是一个`Int`。

值类可以定义defs，但不能定义vals，vars或嵌套的traits类或对象。

以下代码说明了值类 `SomeClass` 中的 `def` 。

值类只能扩展一个通用特征。

```
class SomeClass(val i: Int) extends AnyVal {
    def twice() = i*2
}

```

这里SomeClass是一个用户定义的值类，它包装Int参数并封装两次方法。

要调用两次方法，请按如下所示创建SomeClass类的实例：

```
val v = new SomeClass(9)
v.twice()

```