**Kotlin的高阶函数**  

高阶函数就是以另一个函数作为参数或者返回值的函数。

1 当函数的参数是参数时，java只能使用接口，把函数包起来。例如：View.setOnclickLinstener()。  
2 一个声明好的函数，不管是你要把它作为参数传递给函数，还是要把它赋值给变量，都得在函数名的左边加上双冒号才行。   
```java
fun a(funParam: Fun): String {
    return funParam(1);
}
fun b(param: Int): String {
    return param.toString()
}
a(::b)
val d = ::b
```  
3 ::b 是一个对象，一个函数类型的对象。::b(1) 实际调用 (::b).invoke(1)  
4 匿名函数也是一个对象  
5 如果 Lambda 是函数的最后一个参数，你可以把 Lambda 写在括号的外面：
```java
view.setOnClickListener(fun (v: View) -> Unit {
    switchToNextPage()
})
view.setOnClickListener() { v: View ->
  switchToNextPage()
}
如果Lambda 是函数的唯一参数 可以省略（）
view.setOnClickListener { v: View ->
  switchToNextPage()
}
如果这个 Lambda 是单参数的，它的这个参数也省略掉不写,对于省略的唯一参数有默认的名字：it
view.setOnClickListener { 
  switchToNextPage()
}
```
6 Kotlin 的 Lambda 跟 Java 8 的 Lambda 是不一样的，Java 8 的 Lambda 只是一种便捷写法，本质上并没有功能上的突破，而 Kotlin 的 Lambda 是实实在在的对象。


**总结：**
> 1 在 Kotlin 里，有一类 Java 中不存在的类型，叫做「函数类型」，这一类类型的对象在可以当函数来用的同时，还能作为函数的参数、函数的返回值以及赋值给变量；  
> 2 创建一个函数类型的对象有三种方式：双冒号加函数名、匿名函数和 Lambda；  
> 3 一定要记住：双冒号加函数名、匿名函数和 Lambda 本质上都是函数类型的对象。在 Kotlin 里，匿名函数不是函数，Lambda 也不是什么玄学的所谓「它只是个代码块，没法归类」，Kotlin 的 Lambda 可以归类，它属于函数类型的对象。

参考资料：扔物线  https://rengwuxian.com/kotlin-lambda/