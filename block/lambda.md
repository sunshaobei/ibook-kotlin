#### lambda表达式

> 在kotlin 中并没有block这个概念，只是我们习惯称之为block 函数，其本质是lambda 表达式
>
> 具名后，其在kotlin包中体现为，Function类表达。

lambda 表达式，其实在java8时就很常用到了

```java
view.setOnClickListener(v->{
		//onclick event
}
```

而在kotlin 中

```kotlin
view.setOnClickListener({
		//onclick event 其中 it表示view参数，
})

```

单个参数的lambda表达式，默认以 it表示其参数,也可以自定义其参数名称 ，

```kotlin
view.setOnClickListener({v->
		
})
```

如果匿名函数中有多个参数，则需具象化参数。(假设两个参数)

```kotlin
view.setXXListener({v，t->

})
```

如果函数的最后一个参数是lambda表达式,则lambda 表达式可以提到（）之外，如下：

```kotlin
view.setOnClickListener(){

}
//如果函数仅有一个参数则 （）也可以省略
view.setOnClickListener{
  
}
```

可以观察下区别。区别在于参数不在{}外，而在{} 内。

