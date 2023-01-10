while循环执行一个代码块，只要条件为真。

以下代码每天打印一次投诉，直到13日的下个星期五到达：

```
object Main {
  def main(args: Array[String]) {
     import java.util.Calendar

     def isFridayThirteen(cal: Calendar): Boolean = {
       val dayOfWeek = cal.get(Calendar.DAY_OF_WEEK)
       val dayOfMonth = cal.get(Calendar.DAY_OF_MONTH)
       (dayOfWeek == Calendar.FRIDAY) && (dayOfMonth == 13)
     }
     while (!isFridayThirteen(Calendar.getInstance())) {
       println("Today isn"t Friday the 13th. Lame.")
       Thread.sleep(86400000)
     }
  }
}

```

## Scala do-while循环

do-while循环在条件表达式为真时执行一些代码。

也就是说，do-while检查在运行块之后条件是否为真。

要计数到10，我们可以这样写：

```
object Main {
  def main(args: Array[String]) {
     var count = 0

     do {
       count += 1
       println(count)
     } while (count < 10)

  }
}

```