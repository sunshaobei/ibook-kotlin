> Kotlin提供了类似于C语言的typedef 的功能：可以为已有的类型指定另一个可读性更强的名字。Kotlin提供了typealias来定义类型别名。

typealias语句的语法格式为：

> typealise 类型别名 = 已有类型

如果类型名称太长，你可以另外引入较短的名称，并使用新的名称替代原类型名。

- 它有助于缩短较长的泛型类型。 例如，通常缩减集合类型是很有吸引力的：



```dart
// 为Set<Network.Node> 指定更短的别名NodeSet 
typealias NodeSet = Set<Network.Node>
// 为MutableMap<K, MutableList<File>> 指定更短的别名FileTable<K>
typealias FileTable<K> = MutableMap<K, MutableList<File>>

// 使用
var set : NodeSet 
var table : FileTable<String> 
```

- 你可以为函数类型提供另外的别名：



```kotlin
typealias MyHandler = (Int, String, Any) -> Unit
typealias Predicate<T> = (T) -> Boolean
```

- 你可以为内部类和嵌套类创建新名称（很多时候，我们也可以通过定义别名为内部类起一个更短的名字）：



```kotlin
class A {
    inner class Inner
}
class B {
    inner class Inner
}
//为A.Inner内部类知道别名
typealias AInner = A.Inner
//为B.Inner内部类知道别名
typealias BInner = B.Inner

fun typealiasTest(){
    // 使用AInner 定义变量、调用对象
    var a : AInner = A().AInner()
    // 使用BInner 定义变量、调用对象
    var b = B().BInner()
}
```

## 二、Kotlin自身使用的别名功能

Kotlin自身大量利用别名这个功能。比如Kotlin利用别名建立了Kotlin类和Java类之间的关系。
 如下代码是Kotlin集合体系中定义的别名。



```kotlin
// IntelliJ API Decompiler stub source generated from a class file
// Implementation of methods is not available
package kotlin.collections
@kotlin.SinceKotlin public typealias ArrayList<E> = java.util.ArrayList<E>
@kotlin.SinceKotlin public typealias HashMap<K, V> = java.util.HashMap<K, V>
@kotlin.SinceKotlin public typealias HashSet<E> = java.util.HashSet<E>
@kotlin.SinceKotlin public typealias LinkedHashMap<K, V> = java.util.LinkedHashMap<K, V>
@kotlin.SinceKotlin public typealias LinkedHashSet<E> = java.util.LinkedHashSet<E>
@kotlin.SinceKotlin public typealias RandomAccess = java.util.RandomAccess
```

## 三、Lambda表达式别名

与Java相比，Kotlin的Lambda表达式是一个差异性比较大的特色功能：

> **`Java的Lambda表达式的类型是函数式接口，而Kotlin的Lambda表达式的类型之间就是函数类型。`**

因此Kotlin也允许为Lambda表达式的类型指定别名。如下代码所示：

```kotlin
//为 (T) -> Boolean 类型指定别名  Predicate<T>
typealias Predicate<T> = (T) -> Boolean

fun foo(p: Predicate<Int>) = p(42)

fun main() {
    val f: (Int) -> Boolean = { it > 0 }
    println(foo(f)) // 输出 "true"
    
    //使用 Predicate<Int> 定义变量，该变量的值是一个Lambda表达式
    val p: Predicate<Int> = { it > 0 }
    // 为filter() 方法传入p参数，只保留大于0的数字
    println(listOf(1, -2, 4, 5, 6, 7 ).filter(p)) // 输出 "[1, 4, 5, 6, 7]"
    
    //使用 Predicate<String> 定义变量，该变量的值是一个Lambda表达式
    val p2: Predicate<String> = { it.length > 4 }
    // 为filter() 方法传入p参数，只保留长度大于4的字符串
    println(arrayOf("Java", "Kotlin", "Python", "C", "C++","OuyangPeng").filter(p2))   
}
```

