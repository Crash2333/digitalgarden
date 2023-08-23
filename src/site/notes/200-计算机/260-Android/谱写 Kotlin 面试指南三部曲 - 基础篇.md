---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/谱写 Kotlin 面试指南三部曲 - 基础篇/","tags":["koltin/面试"],"noteIcon":""}
---

## 转载
> 原文地址 [juejin.cn](https://juejin.cn/post/7213582722329952312#comment)

#### 前言

随着金三银四的到来，这段时间陆续开启了面试的热潮，目前 Kotlin 作为 Android 日常开发中的主要的语言基础，无疑成为 Android 面试中常考的一部分，为了检验自身巩固自己的语言基础掌握情况，所以笔者整理收集了当下网上 Kotlin 常见的一些问题，但由于篇幅内容过长所以分了三个部分 (基础篇，协程篇，Flow 篇)，以下是基础篇部分，笔者选取了其中比较经典的 25 个问题，有需要的小伙伴们可以自行拓展，然后进行查缺补漏

Kotlin 面试指南三部曲系列:

*   [谱写 Kotlin 面试指南三部曲 - 协程篇](https://juejin.cn/post/7220235452292137019 "https://juejin.cn/post/7220235452292137019")
*   [谱写 Kotlin 面试指南三部曲 - Flow 篇](https://juejin.cn/post/7222982459583152188 "https://juejin.cn/post/7222982459583152188")

#### Q1：Kotlin 相对于 Java 有什么优势？

其实对于这个问题，根据我们开发人员使用 Kotlin 的实际经验，答案自然有所差异，自己稍微总结一下就好了，一千人就有一千个哈姆雷特;

这里笔者对这个问题最直观的感受就是 Kotlin 写的代码更加简洁，相比 Java 编写相同代码花费的时间和思考更少。以下是本人喜欢 Kotlin 相对于 Java 的几个优点：

*   **数据类**：在 Java 中，必须为每个对象创建 getter 和 setter，并正确编写 hashCode（或让 IDE 去构建它，每次更新类时都必须这样做）、toString 和 equals；在 Kotlin 数据类的帮助下，我们不再需要处理 hashcode、getter 和 setter 等。
*   **扩展函数**：Java 中并不支持扩展函数，Kotlin 提供了扩展函数的支持，使得代码更加清晰和简洁。
*   **支持一个通用代码库**：可以提取一个通用代码库，使用 Kotlin 多平台框架同时针对所有这些代码库。
*   **支持 Null Safety**：Kotlin 内置了 null safety 支持，这是一个救命稻草，尤其是在充满旧 Java 风格 API 的 Android 上。
*   **容错率变高**：出错的空间更小，因为它比 Java 更简洁、更具表现力。

#### Q2: 区分 Kotlin 和 Java

这里使用一个表格来大致概括 Kotlin 和 Java 之间的不同，以便于我们更好的区分

<table><thead><tr><th>basic</th><th align="center">Kotlin</th><th>Java</th></tr></thead><tbody><tr><td>空安全</td><td align="center">默认情况下，Kotlin 中的各种变量都是不可空的（也就是说，我们不能将 null 分配给任何变量或对象）。如果我们尝试分配或返回空值，Kotlin 代码将无法构建。如果我们绝对想要一个变量的空值，我们可以这样声明它：value num: Int? = null</td><td>NullPointerExceptions 是 Java 开发人员的一大烦恼。用户可以将 null 分配给任何变量，但是，当访问具有 null 值的对象引用时，将抛出空指针异常，用户必须管理该异常。</td></tr><tr><td>协程支持</td><td align="center">我们可以在 Kotlin 的多个线程中执行长时间运行的昂贵任务，但我们也有协程支持，它会在给定时刻停止执行，而不会在执行长时间运行的高要求操作时阻塞线程。</td><td>每当我们启动长时间运行的网络 I/0 或 CPU 密集型任务时，Java 中的相应线程就会被阻塞。Android 默认是单线程操作系统。Java 允许您在后台创建和执行大量线程，但管理它们是一项困难的操作。</td></tr><tr><td>数据类</td><td align="center">如果我们需要在 Kotlin 中有数据保存类，我们可以在类声明中定义一个带有关键字 “data” 的类，编译器会处理所有事情，包括为各个字段构造构造函数、getter 和 setter 方法。</td><td>假设我们需要一个 Java 类，它只保存数据而没有其他内容。构造函数、存储数据的变量、getter 和 setter 方法、hashcode()、函数 toString() 和 equals() 函数都需要由开发人员显式编写。</td></tr><tr><td>函数式编程</td><td align="center">Kotlin 是过程式和函数式编程（我们旨在将所有内容绑定到函数单元中的一种编程范式）语言，它具有许多有用的功能，例如 lambda 表达式、运算符重载、高阶函数和惰性求值等。</td><td>Java 直到 Java 8 才允许函数式编程，但是在开发 Android 应用程序的时候，它已经支持 Java 8 功能的子集。</td></tr><tr><td>扩展功能</td><td align="center">Kotlin 使开发人员能够向现有类添加新功能。通过将类名作为新函数名的前缀，我们可以构建扩展函数。</td><td>在 Java 中，如果我们想增强现有类的功能，就必须创建一个新类并继承父类。因此，Java 没有任何扩展功能。</td></tr><tr><td>数据类型推断</td><td align="center">我们不必根据它将在 Kotlin 中处理的赋值来声明每个变量的类型。如果需要，我们可以明确指定。</td><td>在 Java 中声明变量时，我们必须显式地声明每个变量的类型。</td></tr><tr><td>智能转换</td><td align="center">Kotlin 中的智能转换将使用关键字 “is-checks” 处理这些转换检查，它检查不可变值并进行隐式转换。</td><td>我们必须检查 Java 中变量的类型，并为我们的操作适当地转换它们。</td></tr><tr><td>检查异常</td><td align="center">我们在 Kotlin 中没有检查异常。因此，开发人员无需声明或捕获异常，这既有利也有弊。</td><td>我们已经在 Java 中检查了异常支持，这使开发人员能够声明和捕获异常，从而产生更健壮的代码和更好的错误处理。</td></tr></tbody></table>

#### Q3: Kotlin 有哪些可用的数据类型？

原始数据类型是 Kotlin 中最基本的数据类型，其他都是数组、字符串等引用类型。Kotlin 包含所有数据类型作为对象。以下是 Kotlin 中可用的不同数据类型：

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/72c5af7e7aa14830a435629a62adfe1c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

*   **整数数据类型**
    
    <table><thead><tr><th>数据类型</th><th>需要空间</th></tr></thead><tbody><tr><td>byte</td><td>8 bits</td></tr><tr><td>short</td><td>16 bits</td></tr><tr><td>int</td><td>32 bits</td></tr><tr><td>long</td><td>64 bits</td></tr></tbody></table>
*   **浮点数据类型**
    
    <table><thead><tr><th>数据类型</th><th>需要空间</th></tr></thead><tbody><tr><td>float</td><td>32 bits</td></tr><tr><td>double</td><td>64 bits</td></tr></tbody></table>
*   **布尔数据类型**
    
    真或假是布尔数据类型所代表的唯一信息。在 Kotlin 中，布尔类型与 Java 中相同。
    
    <table><thead><tr><th>数据类型</th><th>需要空间</th></tr></thead><tbody><tr><td>boolean</td><td>1 bit</td></tr></tbody></table>
*   **字符数据类型**
    
    字符数据类型表示小写字母 (az)、大写字母 (AZ)、数字 (0-9) 和其他符号。
    
    <table><thead><tr><th>数据类型</th><th>需要空间</th></tr></thead><tbody><tr><td>char</td><td>8 bits</td></tr></tbody></table>
*   **字符串数据类型**
    
    字符串在 Kotlin 中由 String 类型表示，字符串值通常是用双引号 (") 括起来的字符序列，这种情况下所需的空间取决于字符串中的字符数。
    
*   **数组数据类型**
    
    **Kotlin 中的 Array 类**用于表示数组。它具有 get 和 set 函数，由于运算符重载约定，这些函数也可以用作 “[]”。数组所需的空间还取决于它拥有的元素数量。
    

#### Q4: Kotlin 中变量是如何声明的？Kotlin 中有哪些不同类型的变量？

Kotlin 中的每个变量都必须在使用前声明，如果尝试在不声明变量的情况下使用它会导致语法错误，有权放入内存地址的数据类型由变量类型声明决定，在局部变量的情况下，可以根据初始化值确定变量的类型

Kotlin 中有两种类型的变量，它们如下：

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/74297092402a4360a92a51e3d1a397ae~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

*   **不可变变量**——不可变变量也称为只读变量。它们是使用 val 关键字声明的。一旦声明了这些变量，我们就无法更改它们的值。
    
    语法如下:
    
    ```
    val variableName = value
    
    
    ```
    
    因为它可以用变量的值初始化，所以不可变变量不是常量。这意味着不可变变量的值不需要在编译时知道，并且如果它在多次调用的结构中定义，它可以在每次函数调用时采用不同的值。
    
*   **可变变量** - 在可变变量中，可以更改变量的值，我们使用关键字 “var” 来声明此类变量。
    
    语法如下：
    
    ```
    var variableName = value
    
    
    ```
    

#### Q5: Kotlin 中的数据类是什么？

Data 类是一个简单的类，它保存数据并提供典型的功能。要将类声明为数据类，请使用 data 关键字。

用法：

```
data class className ( list_of_parameters)


```

以下函数由编译器自动为数据类派生:

*   **equals()** : 如果两个对象具有相同的内容，则 _equals()_ 函数返回 true。它的操作类似于 “==”，尽管对于 _Float_ 和 _Double_ 值来说它的工作方式不同。
*   **hashCode()** : _hashCode()_ 函数返回对象的哈希码值。
*   **copy()** : _copy()_ 函数用于复制一个对象，只改变它的一些特征，而其余的保持不变。
*   **toString()** : 此函数返回包含所有数据类参数的字符串。

同时为了确保一致性，数据类必须要满足以下要求：

*   主构造函数至少需要一个参数。
*   val 或 var 必须用于所有主构造函数参数。
*   抽象、开放、密封或内部数据类是不可能的。
*   数据类只能实现接口。

#### Q6: 解释 Kotlin 中空安全的概念

Kotlin 旨在从代码中消除空引用。如果程序在运行时抛出 NullPointerExceptions，可能会导致应用程序故障或系统崩溃。如果 Kotlin 编译器发现空引用，它会抛出 NullPointerException。

Kotlin 可以区分可空应用（可以容纳 null 的引用）和非空引用（不可以容纳 null 的引用）。Null 不能存储在 String 变量中（此时是不可空 引用），如果我们尝试将 null 分配给变量，编译器则会报错

```
var a: String = "interview"
a = null //error


```

当然，我们希望上面的字符串也能够保存 null 值，我们可以使用 '?' 将其声明为 nullable 类型。String 关键字后的运算符如下：

```
var a: String? = "interview"
a = null // no compilation error


```

Kotlin 提供了 Safe Call (?.)、Elvis (?:) 和 Not Null Assertion (!!) 运算符，它们定义了遇到 null 时需要执行的操作。这使得代码更可靠，更不容易出错。因此，Kotlin 通过使用可为空、不可为空的类型变量和不同的运算符来解决空值问题，从而强制执行空值安全。

#### Q7 : 解释 Kotlin 中的 Safe call、Elvis 和 Not Null Assertion 运算符

*   **安全调用 (Safe call) 运算符(?.)**
    
    空值比较很简单，但嵌套的 if-else 表达式的数量可能会让人筋疲力尽，代码感官上也不太好。因此，在 Kotlin 中，有一个安全调用运算符 ?，它通过仅在指定引用包含非空值时执行操作来简化操作，它允许我们使用单个表达式来执行空检查和方法调用。
    
    ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/69335021913745a5b6f85ef6b1149639~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
*   **Elvis 运算符 (?:)**
    
    当原始变量为 null 时，Elvis 运算符用于返回非空值或默认值。换句话说，如果 elvis 运算符不为空，则返回左边的表达式，否则返回右边的表达式。只有当左侧表达式为 null 时，才会对右侧进行求值。
    
    ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b3f142d616f7454bbd46fbd257e626a2~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
*   **非空断言运算符 (!!)**
    
    如果值为空，则非空断言 (!!) 运算符将其更改为非空类型并引发异常，任何想要 NullPointerException 的开发者都可以使用此运算符显式请求它。
    
    ```
    fun main() {
        var sample : String?  = null
        println(str!!.length)
    }
    
    
    ```
    
    ```
    Exception in thread "main" kotlin.KotlinNullPointerException
    
    
    ```
    

#### Q8: 如何在 Kotlin 中连接两个字符串？

以下是我们可以在 Kotlin 中连接两个字符串的不同方法：

*   **使用字符串插值**
    
    使用字符串插值技术连接两个字符串。基本上，我们在第三个字符串的初始化中用字符串代替它们的占位符。
    
    ```
    val s1 = "Jacky"
    val s2 = "Tallow"
    val s3 = "$s1 $s2" // stores "Jacky Tallow"
    
    
    ```
    
*   **使用 + 或 plus() 运算符**
    
    我们使用 “+” 运算符连接两个字符串并将它们存储在第三个变量中。
    
    ```
    val s1 = "Jacky"
    val s2 = "Tallow"
    val s3 = s1 + s2 // stores "JackyTallow"
    val s4 = s1.plus(s2) // stores "JackyTallow"
    
    
    ```
    
*   **使用 StringBuilder**
    
    我们使用 StringBuilder 对象连接两个字符串。首先，我们附加第一个字符串，然后附加第二个字符串。
    
    ```
    val s1 = "Jacky"
    val s2 = "Tallow"
    val s3 =  StringBuilder()     
    s3.append(s1).append(s2)
    val s4 = s3.toString() // stores "JackyTallow"
    
    
    ```
    

#### Q9: Kotlin 中 List 和 Array 类型之间有什么区别？

*   它们之间的主要区别在于 _Array_ 是固定大小的内存区域，_List_ 的内部实现会进行数组的扩容和缩容操作
*   _Array_ 是可变的（可以通过对其的任何引用进行更改），但是 _List_ 没有修改方法（它是只读视图 _MutableList_ 或不可变列表实现）
*   总的来说，Array 适用于固定长度的场景，List 适用于动态长度的场景，如果需要频繁添加和删除元素时，可以优先考虑使用 List

#### Q10: **可以在 Kotlin 中互换使用`IntArray`和`Array<Int>`吗？**

显然我们要知道，Kotlin 中 _Array _是属于_ Integer[] _引用下的，而_ IntArray() _是_ Int[]_;

这也就意味着将一组数字放入 _Array _中，它将始终被装箱（特别是通过`Integer.valueOf()`调用）；而放入到_ IntArray_ 中，它不会发生装箱，因为已经转换成了 Java 原始数组; 所以得出结论，**我们不能互相使用它们**。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4a7191e323364c84829a748349778f9d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

#### Q11: 如何理解 Kotlin 中的 Companion Object？

首先我们要知道在 Java 中 _static_ 关键字用于声明类成员并在不创建对象的情况下使用它们，即通过类名简单地调用它们，而在 Kotlin 中，没有所谓的 “static” 关键字。所以，如果我们要实现静态成员函数的功能，就要用到伴生对象，这也称为对象扩展。

值得注意的是，我们必须在对象定义前使用 **Companion** 关键字来构造伴随对象

```
class CompanionClass {

    companion object CompanionObjectName {
      // code
    }
}
val obj = CompanionClass.CompanionObjectName


```

我们也可以去掉 CompanionObject 的名字，换成 companion 这个词，这样 companion 对象的默认名字就是 Companion，如下：

```
class CompanionClass {
   companion object {
     // code
   }
}
val obj = CompanionClass.Companion


```

这样以来，所有必需的静态成员函数和成员变量都可以保存在创建的伴生对象中

```
class Sample {
   companion object Test {
       var a: Int = 1
       fun testFunction() = println("Test Kotlin")
   }
}
fun main() {
   println(Sample.a)
   Sample.testFunction()
}


```

#### Q12: 区分 Kotlin 中的 open 和 public 关键字

*   一方面，open 关键字表示为扩展开放。使用 open 关键字，任何其他类都可以从该类继承，但一般默认情况下，类不能在 Kotlin 中被继承。
    
*   另一方面，public 关键字是访问修饰符，它是 Kotlin 中的默认访问修饰符，如果没有指定可见性修饰符，则默认使用 public，这意味着我们的声明在程序中的任何地方都可以访问
    

#### Q13: 解释 Kotlin 中的 “when” 关键字

_when_ 关键字在 Kotlin 中用于替代 Java 中的 switch 运算符，当满足特定条件时，必须运行特定代码块，在 when 表达式中，它会逐一比较所有分支，直到找到匹配项。找到第一个匹配项后，它继续执行 when 块的结论并立即执行 when 块之后的代码。与 Java 或任何其他编程语言中的 switch case 不同，我们不需要在每个 case 的末尾使用 break 语句。

```
fun main() {
   
   var temp = "Interview"
   when(temp) {
       "Interview" -> println("面试进行中。。。")
       "Job" -> println("面试通过了")
       "Success" -> println("工作中困难的部分被解决了")
   }
}


```

#### Q14: 你对 Kotlin 中的 backing field 有什么理解？

​ _backing field_ 是一个自动生成的字段，它仅仅可以被用在拥有至少一个默认访问器 (getter、setter) 、或者在自定义访问器中通过 field 标识符修饰的属性中。_backing field_ 可以避免访问器的自递归而导致程序崩溃的 StackOverflowError 异常。

​ 而且 Kotlin 中的类不能有 field。但是，有时在使用自定义访问器时必须有一个 _backing field_ 。为此，Kotlin 提供了一个自动 backing field，可以使用 _field_ 标识符来访问。

```
var marks: Int = someValue
       get() = field
       set(value) {
           field = value
       }


```

> 此处字段标识符充当对 get() 和 set() 方法中属性 “标记” 值的引用。因此，每当我们调用 get() 时，我们都会返回该字段的值。同样，每当我们调用 set() 时，我们都会将 “marks” 属性值设置为“value”

#### Q15: 你对 Kotlin 中的密封类有什么了解？

Kotlin 引入了一种在 Java 中没有的新类形式。这些被称为 “密封类”。顾名思义，密封类遵循受约束或有界的类层次结构。

当然这个回答确实有些拗口，换一种说法，密封类其实就是具有一组子类的类，里面所有子类都继承这个密封类，当提前知道一个类型将符合其中一个子类类型时，它就会被使用。类型安全（即，编译器将在编译期间验证类型，如果将错误的类型分配给变量则抛出异常）通过密封类来确保，这限制了可以在编译时而不是运行时匹配的类型。

语法如下：

```
sealed class className


```

> 密封类的另一个显着方面是它们的构造函数默认是私有的。而且由于密封类自动抽象，因此无法实例化。

```
sealed class Person {

    class Eat : Person() {
        fun eatApple() {
            println("eat Apple")
        }

        fun eatRice() {
            println("eat Rice")
        }

    }
    class Sleep : Person() {
        fun startSleep() {
            println("start sleep")
        }
        fun endSleep() {
            println("end sleep")
        }
    }
}

fun main() {

    val personEat = Person.Eat()

    personEat.eatRice()
    personEat.eatApple()

    val personSleep = Person.Sleep()

    personSleep.startSleep()
    personSleep.endSleep()
}


```

​ 在上面的代码中，我们创建了一个名为 “Person” 的密封类，并在其中创建了两个名为 “Eat” 和“Sleep”的子类。在主函数中，我们创建两个子类的实例并调用它们的子方法。

#### Q16: Kotlin 中的 Inline 内联类是什么，我们什么时候需要它？

有时业务逻辑需要围绕某种类型创建包装器。但是，由于额外的堆分配，它引入了运行时开销。此外，如果包装类型是原始类型，性能损失会很严重，因为原始类型通常会在运行时进行大量优化。

**内联类**为我们提供了一种包装类型的方法，从而增加功能并自行创建新类型。与常规（非内联）包装器相反，它们将受益于改进的性能，这种情况是因为数据被内联到它的用法中，并且在生成的编译代码中跳过了对象实例化。

```
inline class Name(val s: String) {
    val length: Int
        get() = s.length

    fun greet() {
        println("Hello, $s")
    }
}    

fun main() {
    val name = Name("Kotlin")
    name.greet()
    println(name.length)
}


```

关于内联类的一些注意事项

*   在主构造函数中初始化单个属性是内联类的基本要求
*   内联类允许我们像普通类一样定义属性和函数
*   不允许初始化块、内部类和 _backing field_
*   内联类只能从接口中继承
*   内联类也是有效的 _final_

#### Q17: 你对 Kotlin 中的 lateinit 有什么理解？你什么时候会考虑使用它？

显而易见，_lateinit_ 表示延迟初始化。如果我们不想在构造函数中初始化一个变量，而是想稍后对其进行初始化，当然需要保证在使用它之前进行初始化，这个时候就可以使用 _lateinit_ 关键字声明该变量。它在初始化之前不会分配内存。我们不能将 _lateinit_ 用于原始类型属性，如 Int、Long 等。

```
lateinit var test: String

fun doSomething() {
    test = "Some value"
    println("Length of string is "+test.length)
    test = "change value"
}
```


```

其实在日常开发中，对一些用例会非常有用，例如

*   Android：在生命周期方法中初始化的变量；
*   使用 Dagger 进行 DI：注入的类变量在构造函数外部独立初始化；
*   单元测试设置：测试环境变量在 - 注释方法中初始化`@Before`；
*   Spring Boot 注释（例如。`@Autowired`）；

#### Q18: 解释下 Kotlin 中的惰性初始化 lazy

​ 有一些类的对象初始化非常耗时，导致整个类的创建过程被延迟。而 **by lazy 惰性初始化**有助于解决这类问题。当我们使用惰性初始化声明一个对象时，该对象仅在使用该对象时初始化一次。如果该对象没有被使用，则该对象不会被初始化。这使得代码更高效、更快速。

例如，假设我们有一个 _SlowClass_ 类，并且需要一个名为 _FastClass_ 的不同类中的该 _SlowClass_ 的对象：

```
class FastClass {
   private val slowObject: SlowClass = SlowClass()
}


```

我们这里生成的是一个大对象，会导致 _FastClass_ 的开发变慢或者延迟。有时可能不需 _SlowClass_ 对象。因此，_by lazy_ 关键字可以在这种情况下为我们提供帮助：

```
class FastClass {
   private val slowObject: SlowClass by lazy {
       println("Slow Object initialised")
       SlowClass()
   } 
   
   fun access() {
       println(slowObject)
   }
}
fun main() {
   val fastClass = FastClass()
   println("FastClass initialised")
   fastClass.access()
   fastClass.access()
}


```

> 在上面的代码中，我们使用惰性初始化 by lazy 在 FastClass 的类结构中实例化了一个 SlowClass 的对象。SlowClass 的对象只有在上面的代码中被访问时才会生成，也就是我们调用 FastClass 对象的 access() 方法时，整个 main() 方法中都存在同一个对象

#### Q19: 区分 lateinit 和 lazy? 什么时候应该使用 lateinit 以及什么时候应该使用 lazy?

还是用一个表格来展示 lateinit 和 by lazy 的区别:

<table><thead><tr><th align="center">lateinit</th><th align="center">by lazy</th></tr></thead><tbody><tr><td align="center">主要目的是将初始化延迟到稍后的时间节点</td><td align="center">主要目的是仅在稍后使用对象时才初始化对象。此外，在整个程序中维护对象的单个副本。</td></tr><tr><td align="center">可以从项目程序中任何地方初始化对象</td><td align="center">只有初始化器 lambda 可用于初始化它</td></tr><tr><td align="center">在这种情况下可以进行多次初始化</td><td align="center">在这种情况下只能进行一次初始化。</td></tr><tr><td align="center">它不是线程安全的。在多线程的环境中，是否正确初始化取决于开发者。</td><td align="center">默认情况下启用线程安全，确保初始化程序只被调用一次。</td></tr><tr><td align="center">仅适用于 var</td><td align="center">仅适用于 val</td></tr><tr><td align="center">添加了 isInitialized 方法以验证该值之前是否已被初始化。</td><td align="center">不可能取消初始化一个属性。</td></tr><tr><td align="center">不允许原始类型的属性</td><td align="center">运行使用原始类型属性</td></tr></tbody></table>

我们在决定是使用 lateinit 还是延迟初始化来进行初始化的时候，需要我们去遵循一些原则：

*   如果属性是可变的，之后可能会更改，那么推荐使用 _lateinit_
*   如果属性是在外部设置的（例如，如果您需要传入一个外部变量来设置它），请使用 _lateinit_。仍然有一种方法可以使用 lazy，但不是那么明显。
*   如果只打算初始化一次并由所有人共享，并且它们更多是在内部设置的（取决于类变量），那么惰性初始化 lazy 是可行的方法。我们仍然可以在战术意义上使用 _lateinit_，但是使用惰性初始化会更好地封装我们的初始化代码。
*   by lazy {...} 的初始化默认是线程安全的，并且能保证 by lazy { ... } 代码块中的代码最多被调用一次，而 lateinit var 默认是不保证线程安全的，它的情况完全取决于使用者的代码。

> 就像有些人说的一样，lateinit 是手动档，而 lazy 是自动档

#### Q20: Kotlin 中 fold 和 reduce 的基本区别是什么？什么时候使用哪个？

​ 对于这两个函数首先要知道它们都是 Kotlin 集合中的聚合操作函数，下面我简单分开来说说

*   _fold_ 接受一个初始值，第一次调用将接收该初始值和集合的第一个元素作为参数。
    
    ```
    listOf(1, 2, 3).fold(0) { sum, element -> sum + element }
    
    
    ```
    
    这样意味着，我传了初始值是 0，那么第一次调用的初始值参数为 0，同理，传了初始值是 10，第一次调用的初始值参数为 10；所以如果有时候需求必须指定默认值或参数，那么 _fold_ 绝对是很好的选择。
    
*   _reduce_ 不采用初始值，而是从集合的第一个元素开始作为累加器
    
    ```
    listOf(1, 2, 3).reduce { sum, element -> sum + element }
    
    
    ```
    

​ 对于一些不需要指定特定默认值的场景，比如说可以使用 reduce 实现集合求和累加，还可以将集合拼接成字符串等等

**总的来说，fold() 接受一个初始值并将其用作第一步的累积值，而 reduce() 的第一步则将第一个和第二个元素作为第一步的操作参数**。

#### Q21: Kotlin 中有哪些不同类型的作用域函数 (标准函数)？

这确实是 kotlin 老生常谈的问题了，_let_,_also_,_apply_,_with_,_run_ 这些标准函数在日常开发中使用非常频繁，简单概括一下:

*   _let_：扩展函数，let 默认当前这个对象作为闭包的 it 参数，返回值为函数最后一行或者 return。
*   _apply_：扩展函数，在 apply 函数范围内可以任意调用该对象的任意方法，并返回该对象。
*   _also_ : 默认当前这个对象作为闭包的 it 参数，返回它被调用的对象，可以对该对象进行相关操作，可用于在调用链上生成一些辅助逻辑。
*   _with_：非扩展函数，返回值是最后一行，这点类似 let。可以直接调用对象的方法，这点类似 apply。
*   _run_：扩展函数，run 和 with 很像，可以调用对象的任意函数，返回值是最后一行。

为了更加清晰的看出它们之间的主要区别，笔者提供了一个表格供参考

<table><thead><tr><th>函数</th><th>对象引用</th><th>返回值</th><th>是否是扩展函数</th></tr></thead><tbody><tr><td>let</td><td>it</td><td>Lambda 表达式结果</td><td>是</td></tr><tr><td>run</td><td>this</td><td>Lambda 表达式结果</td><td>是</td></tr><tr><td>run</td><td>-</td><td>Lambda 表达式结果</td><td>不是：调用无需上下文对象</td></tr><tr><td>with</td><td>this</td><td>Lambda 表达式结果</td><td>不是；把上下文当成参数</td></tr><tr><td>apply</td><td>this</td><td>上下文对象</td><td>是</td></tr><tr><td>aslo</td><td>it</td><td>上下文对象</td><td>是</td></tr></tbody></table>

​ ![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3027b038b3fd44faa4ede155f5210529~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

> 当然不同的标准函数的用途场景存在重叠，一切根据项目或团队中使用的特定约定来进行选择，避免过度嵌套不同的标准函数，当然不得不链式调用它们的时候，要格外注意当前上下文的值以及 _this_ 或者 _it_ 的值。

#### Q22: Kotlin 泛型中的 out 和 in 关键字？

提起 Kotlin 泛型不得不说到这两个关键字：in(逆变) 和 out(协变)，字面意思上就是 _in_ 表示这个参数 / 变量只能用来输入，不能读取，_out_ 就反过来，只能用来输出，不能读取。具体怎么体现呢，下面我们来简单说说

##### out（协变型）

如果我们的泛型类仅仅使用泛型类型作为函数的输出，那么就使用 out

```
interface Production<out T> {
    fun produce():T
}


```

这就是典型的生产者类接口，主要用来生产通用类型的输出，我们就记住 **（生产 = 输出 = out）**

##### in(逆变型)

如果我们的泛型类仅使用泛型类型作为函数的输入，那么就使用 in

```
interface Consumer<in T> {
    fun consume(item: T)
}


```

这就是典型的消费者类接口，主要使用的都是泛型类型，我们就记住 **（消费 = 输入 = in）**

##### 什么时候使用 in 和 out？

上面我们已经知道了 in 和 out 的基本描述，但是它们的意义是什么呢？举个经典的例子，我们定义一个炸鸡类对象

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/97614bc8aa824b37b8e3a2cdcd043156~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

```
open class Food
open class FastFood : Food()
class Checken: FastFood()


```

###### 炸鸡生产

可以进一步扩展它们分别进行生产食物，快餐 KFC，炸鸡，如下代码所示：

```
class FoodStore : Production<Food> {
    override fun produce(): Food {
        println ("Produce 食物")
        return Food()
    }
}

class FastFoodStore : Production<FastFood> {
    override fun produce(): FastFood {
        println("Produce 快餐")
        return FastFood()
    }
}

class InOutChecken : Production<Checken> {
    override fun produce(): Checken {
        println ("Produce 炸鸡")
        return Checken()
    }
}


```

接着我们让食品生产持有者，可以将这些全部都分配给它

```
val production1 : Production<Food> = FoodStore() 
val production2 : Production<Food> = FastFoodStore() 
val production3 : Production<Food> = InOutChecken()


```

可以看到无论是炸鸡还是快餐生产，它们都属于食品生产，因此就可以得出结论

> 使用了 `out` 关键字，我们可以将子类型的类分配给超类型的类

注意一下，反过来就会出错，因为食物或者快餐不仅仅只有炸鸡进行生产

###### 炸鸡消费者

根据上述的 _Consumer_ 通用接口，我们来消费下食物，快餐和炸鸡，如下代码所示：

```
class Everybody : Consumer<Food> {
    override fun consume(item: Food) {
        println("Eat 食物")
    }
}

class ChinesePeople : Consumer<FastFood> {
    override fun consume(item: FastFood) {
        println("Eat 快餐")
    }
}

class Cantonese : Consumer<Checken> {
    override fun consume(item: Checken) {
        println("Eat 炸鸡")
    }
}


```

现在我们让消费者持有炸鸡，然后将上面的类全部分配给它

```
val consumer1 : Consumer<Checken> = Everybody() 
val consumer2 : Consumer<Checken> = ChinesePeople() 
val consumer3 : Consumer<Checken> = Cantonese()


```

在这里，炸鸡的消费者是广东人，他也是中国人的一部分，同时也属于世界上的每一个人，由此我们可以得出结论：

> 使用了`in`关键字，我们可以将超类型的类分配给子类型的类

如果反过来就有会出错，食物的消费者可能是中国人或广东人，但它不仅仅只有中国人或广东人，有可能是美国人，韩国人呢...

总结一下，关于什么时候使用 in/out

*   _SuperType 可以分配 SubType，使用 in_
*   _SubType 可以分配给 SuperType，使用 out_

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6f880c9556c4471fbaa6c0c4be5aa1e5~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

> 更多 Kotlin 泛型详情学习可以去看 [扔物线大佬 Kotlin 泛型的视频](https://link.juejin.cn?target=)

#### Q23: Kotlin 泛型中的 * 和 Any 的区别是什么？

*   对于 Any 简单来说，它是 Kotlin 中所有类的共同基类，相当于 Java 中的 Object，而 Any？则表示允许传入空值。
    
*   对于 Kotlin 泛型中的 * 号 :
    
    *   首先要说回`out`和`in`两个关键字，使用关键字 `out` 来支持协变，等同于 Java 中的上界通配符 `? extends`；使用关键字 `in` 来支持逆变，等同于 Java 中的下界通配符 `? super`。
        
        ```
        var textViews: List<out TextView>
        var textViews: List<in TextView>
        
        
        ```
        
        只是换了一种写法，和 Java 的作用是一样的。`out` 表示，我这个变量或者参数只用来输出，不用来输入，你只能读我不能写我；`in` 就反过来，表示它只用来输入，不用来输出，你只能写我不能读我。
        
    *   在 Kotlin 中的`*` 号，相当于 `out Any`，其实就是 Java 中`?`作为泛型通配符使用，根据上述表表明`*`号中的变量参数只能用来输出。
        
    
    > 这里笔者只是简单概括了下主要的区别，详情学习可以去看 [扔物线大佬 Kotlin 泛型的视频](https://link.juejin.cn?target=)，非常简明易懂
    

#### Q24: 了解过 Kotlin 的 reified 关键字么? 它有什么作用？

##### 什么是 refied 关键字

​ 由于我们都知道 Kotlin 和 Java 一样都存在着**泛型擦除**问题，而 Kotlin 它知道 Java 所带来的这个问题，所以对此 Kotlin 留了一个后门，就是通过 _inline_ 函数保证使得泛型类的类型实参在运行时能够保留，这样的操作 Kotlin 中把它称为**实化**，对应需要使用 **reified** 关键字。而 _reified_ 意为具体化，使得 (抽象的东西) 变得更加具体化，它是 Kotlin 所增强的一种泛型的使用方式；

当然，使用 reified 关键字必要条件如下：

*   **必须是 inline 内联函数，使用 inline 关键字修饰**；
*   **泛型类定义泛型形参时必须使用 reified 关键字修饰**；

##### reified 背后的故事

​ 既然我们知道 reified 和 inline 函数是相辅相成的，使用 _inline_ 函数的最大一个好处就是**函数调用的性能优化和提升**，需要注意的是 _reflied_ 使用 _inline_ 函数并不是因为性能的问题，而是另外一个好处**它能使泛型函数类型实参进行实化**，在运行时能拿到类型实参的信息，相当于**带实化参数的函数每次调用都生成不同类型实参的字节码，动态插入到调用点**。由于生成的字节码的类型实参引用了具体的类型，而不是类型参数所以不会存在擦除问题；

​ 综上所述，这也是为啥 reifiied 关键字必须使用 _inline_ 关键字修饰的原因。换句话说，使用 _reifled_ 可以保证泛型类的类型实参可以在运行中被保留，由于是具体的参数类型，可有效避免了泛型擦除的问题。

#### Q25: Kotlin 的 SAM 转换是什么？

在 Kotlin 中，_SAM_ 的概念其实是从 Java 那边追溯过来的，在 Java 中，我们把单一方法的接口叫做 SAM(Single Abstract Method) 接口，从 Java8 之后通过 Lambda 可以大大简化对于 SAM 接口的调用。所以`SAM`就代表的是单一抽象方法，“SAM 类型” 是指像 _Runnable_，_Callable_ 等接口；Lambda 表达式其实就可以被认为是 SAM 类型，可以自由转换为它们。

这里简单举个例子来看下

```
fun main() {


    //方案一：匿名类对象
    buyCar(object : IBuy {
        override fun onBuy(money: Double) {
            println("buyCar:$money")
        }
    })

    //方案二：SAM构造方法
    buyCar(IBuy {
        println("BuyCar:$it")
    })

    //方案三：SAM构造方法(推荐)
    buyCar({
        println("BuyCar:$it")
    })

    
    //方案四：SAM构造方法（推荐）
    buyCar {
        println("BuyCar: $it")
    }

}

//买一辆一千万的车
fun buyCar(buy: IBuy) {
    buy.onBuy(10000000.0)
}

fun interface IBuy {
    fun onBuy(money: Double)
}



```

​ 因此，我们借助 _Lambda_ 表达式对 _SamType_ 调用的优化称为 **SAM 转换（Single Abstract Method Conversions）**，Kotlin 对此已经兼容了 Java 中的 SAM 转换，它只是将 Java 的 _SamType_ 翻译成了 _Lambda_，因此在 kotlin 的同名方法实际变成了一个高阶函数。