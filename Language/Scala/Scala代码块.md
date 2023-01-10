方法和变量定义可以是如下的单行：

```
def meth() = "Hello World"

```

方法和变量也可以在用大括号{}表示的代码块中定义。

代码块可以嵌套。

代码块的结果是在代码块中计算的最后一行，如以下示例所示。

```
object Main {
    def meth1():String = {"hi"}
    def meth2():String = {
        val d = new java.util.Date()
        d.toString()
    }

  def main(args: Array[String]) {
    println(meth1 )
    println(meth2 )
  }
}

```

变量定义也可以是代码块。

```
val x3:String= {
    val d = new java.util.Date()
    d.toString()
}

```