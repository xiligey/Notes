Scala中的异常处理以不同的方式实现，但它的行为与Java完全相同，并与现有的Java库无缝协作。

Scala中的所有异常都未选中；没有检查异常的概念。

抛出异常在Scala和Java中是一样的。

```
throw new Exception("some exception...")

```

try/finally结构在Scala和Java中也是一样的，如下面的代码所示。

```
try {
    throw newException("some exception...")
} finally{
    println("This will always be printed")
}

```

try/catch在Scala是一个表达式，导致一个值。

Scala中的异常可以在catch块中进行模式匹配，而不是为每个不同的异常提供单独的catch子句。

因为Scala中的try/catch是一个表达式，所以可以在try / catch中包装调用，并在调用失败时分配默认值。

以下代码显示了具有模式匹配catch块的基本try/catch表达式。

```
try {
    file.write(stuff)
} catch{
    case e:java.io.IOException => // handle IO Exception
    case n:NullPointerException => // handle null pointer
}
```

## 例子

以下代码显示了通过调用Integer.parseIntand在try/catch中包装调用的示例，如果调用失败，则分配默认值。

```
try{
   Integer.parseInt("dog")
}catch{
   case_ => 0
}

```