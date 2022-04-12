#### lambda表达式

> 在kotlin 中并没有block这个概念，只是我们习惯称之为block 函数，其本质是lambda 表达式
>
> 具名后，其在kotlin包中体现为，Function类表达。

lambda 表达式，其实在java8时就很常用到了

```java
view.setOnClickListener(v->{
		//onclick event
})
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
view.setOnClickListener(view){

}
//如果函数仅有一个参数则 （）也可以省略
view.setOnClickListener{
  
}
```

可以观察下区别。区别在于参数不在{}外，而在{} 内。

以上我们可知 由java 接口回调 转 kotlin lambda 表达式的过程。在熟悉kotlin后，就不会再去写接口了，而是直接用lambda 表达式替代

#### 万能接口

在不考虑回调类型的情况下 在java 中实现万能回调接口

```java
public interface Callback{
	Object invoke(Object...obj);
}
```

而kotlin中已经帮我们实现 kotlin.jvm.functions

```kotlin
/** A function that takes 0 arguments. */
public interface Function0<out R> : Function<R> {
    /** Invokes the function. */
    public operator fun invoke(): R
}
/** A function that takes 1 argument. */
public interface Function1<in P1, out R> : Function<R> {
    /** Invokes the function with the specified argument. */
    public operator fun invoke(p1: P1): R
}

//....一直到23个参数
/** A function that takes 22 arguments. */
public interface Function22<in P1, in P2, in P3, in P4, in P5, in P6, in P7, in P8, in P9, in P10, in P11, in P12, in P13, in P14, in P15, in P16, in P17, in P18, in P19, in P20, in P21, in P22, out R> : Function<R> {
    /** Invokes the function with the specified arguments. */
    public operator fun invoke(p1: P1, p2: P2, p3: P3, p4: P4, p5: P5, p6: P6, p7: P7, p8: P8, p9: P9, p10: P10, p11: P11, p12: P12, p13: P13, p14: P14, p15: P15, p16: P16, p17: P17, p18: P18, p19: P19, p20: P20, p21: P21, p22: P22): R
}
```



#### 什么样的接口能用lambda替代

* 代码提示

* Java 接口 && 单一方法 任意参数 任意返回值

* functions 接口

* kotlin中的书写的typealias 其本质就是 functions

  

  例一：

  Java

  ```java
  public interface Callback{
  	void onCallback(String s);
  }
  ```

  在kotlin中调用

  ```kotlin
  fun test(callback:Callback){
  		callback.onCallback("sdfsdf")
  }
  
  
  //调用
  test{  //默认参数it
  	
  }
  ```

  例二：

  

  ```kotlin
  fun test(block:Function1<String,Any>){
  		block.invoke("sdfsdf")
  }
  
  
  //调用
  test{  //默认参数it
  	
  }
  ```

  

  例三：

  

  ```kotlin
  fun test(block:(String)->Unit){
  		block.invoke("sdfsdf")
  }
  
  //调用
  test{  //默认参数it
  	
  }
  ```

  





