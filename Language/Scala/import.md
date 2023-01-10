要在包中使用声明，我们必须导入它们，就像在Java中一样。

Scala提供了其他选项，如下面导入Java类型的示例所示：

包是一个命名的代码模块。

Java和Scala惯例规定程序包名称是代码所有者的反向域名。

源文件中的第一个非注释行：

```
package com.java2s.stuff

```

可以导入Scala包，以便可以在当前编译范围中引用它们。

以下语句导入scala.xml软件包的内容：

```
import scala.xml._

```

以下语句导入scala.xml软件包的内容：

```
import transform._

```

我们可以从scala.collection.mutable包中导入单个类和对象，例如HashMap：

```
import scala.collection.mutable.HashMap

```

我们可以从单个包中导入多个类或对象，例如，从scala.collection.immutable包中导入TreeMap和TreeSet：

```
import scala.collection.immutable.{TreeMap, TreeSet}
```

## 例子

```
     import java.awt._
     import java.io.File
     import java.io.File._
     import java.util.{Map, HashMap}

```

我们可以在包中使用下划线 `_` 作为通配符导入所有类型。

我们还可以导入单个Scala或Java类型，如第二行所示。

Java使用“星号"字符 `*` 作为导入的通配符。

在Scala中，此字符被允许作为方法名称，因此使用 `_` 来避免歧义。

第三行导入java.io.File中的所有静态方法和字段。

等效的Java导入语句将是import static java.io.File。*;

最后，我们可以导入一个类或对象并重命名它。例如，您可以从scala.util.parsing.json包中导入JSON类/对象，并将其重命名为JsonParser：

```
import scala.util.parsing.json.{JSON=> JsonParser}

```

import可以在任何代码块内部使用，导入将仅在该代码块的范围内有效。

例如，我们可以在类体中导入一些东西，如下面的代码所示：

```
class Frog {
    import scala.xml._
    //
}

```

例如，我们可以在类体中导入一些东西，如下面的代码所示：

这很像Java的静态导入。

组合局部范围导入和导入对象允许我们微调导入对象及其关联方法的位置。

## 注意

Scala没有导入静态构造，因为它像其他类型一样对待对象类型。

我们可以将import语句几乎放在任何地方，以将它们的可见性限制在需要它们的地方。

我们可以在导入时重命名类型，我们可以禁止不需要的类型的可见性：

```
     def stuffWithBigInteger() = {

       import java.math.BigInteger.{
         ONE => _,
         TEN,
         ZERO => JAVAZERO }

       println( "TEN: "+TEN )
       println( "ZERO: "+JAVAZERO )
     }

```

## 导入是相对的

Scala导入是相对的。

请注意以下导入的注释：

```
     import scala.collection.mutable._
     import collection.immutable._              // Since "scala" is already imported
     import _root_.scala.collection.parallel._  // full path from real "root"

```