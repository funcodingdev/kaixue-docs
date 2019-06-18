# Kotlin 基础语法（一）

Google 在 I/O 2019 上，宣布 Kotlin 成为 Android 的第一开发语言，对于开发者来讲意味着，将来更多的官方示例会首选 Kotlin，Google 对 Kotlin 在开发、构建等各个方面的支持也会更优先。

在这个大环境下，很多公司的移动开发岗也已经把 Kotlin 作为面试的考察点之一，甚至作为简历筛选的必要条件，学会并掌握 Kotlin 成了 Android 开发者的当务之急。

「Kotlin 好难学啊」、「Kotlin 真的有那么好吗」相信屏幕前的你也有这些疑问。鉴于 Kotlin 在国内还不算普及，而学习一门新语言有不少成本，本系列文章，将会帮助国内开发者学习并掌握 Kotlin。

## 搭建 Kotlin 开发环境

新建一个 Android 项目：

![image-20190618165547599](http://ww2.sinaimg.cn/large/006tNc79gy1g45euvu7aqj30q80gu3za.jpg)

语言选择 Kotlin 是为了让项目支持 Kotlin，其实也就 2 个 `build.gradle` 文件有所不同：

- 项目根目录下的

    ![image-20190618165947454](http://ww4.sinaimg.cn/large/006tNc79gy1g45ez1g8fdj31e40hqdkb.jpg)

- app 目录下的

    ![image-20190618170205176](http://ww4.sinaimg.cn/large/006tNc79gy1g45f1fy08dj31i50u07dh.jpg)

如果是现有的项目要支持 Kotlin，只需要在这两个目录的 `build.gradle` 加上红色方框内的部分就可以了。

来看看 IDE 帮我们创建好的 MainActivity.kt：

Kotlin 文件都是以 `.kt` 结尾的，Java 则是以 `.java` 结尾。

![image-20190618171301284](http://ww1.sinaimg.cn/large/006tNc79gy1g45fctne1nj31200ekjuw.jpg)

Java 里有的东西：

- `package`
- `import`
- `class`

这些关键字 Java 里也有，概念上也类似，不过其中还是有一些小区别的，但我们现在不用关心。

Java 里没有的东西：

- `:`
- `override`
- `fun`
- `?`

还有一点，Kotlin 里是**没有分号**的，这点区别于 Java。

这些东西都是 Kotlin 的语法，也先不管，我们自己新建一个来屏蔽掉这些我们不认识的东西。

在新建 Java Class 的入口发现一个叫 Kotlin File/Class 的选项，这就是我们新建 Kotlin 文件的入口。

![](http://ww3.sinaimg.cn/large/006tNc79gy1g42sk3roflj314a08s40r.jpg)

这里我们先不管其他选项，选择新建 Class：

![image-20190618173125004](http://ww3.sinaimg.cn/large/006tNc79gy1g45fvy6g31j30je0aeabo.jpg)

创建完成后的 Sample.kt：

![image-20190618173159412](http://ww2.sinaimg.cn/large/006tNc79gy1g45fwjbnwyj30l406yjru.jpg)

这个类就没有刚才我们不认识的那些东西了。

至此，Kotlin 开发环境就搭建好了，小结下：

- Android 项目要支持 Kotlin，需要在项目根目录和 app 目录下的 `build.gradle` 添加 Kotlin 相关的依赖。
- Java 文件以 `.java` 结尾，而 Kotlin 文件以 `.kt` 结尾。

接下来，让我们一起开始学习基础语法吧。

---

## 变量

### 变量的声明与赋值

Kotlin 里声明一个变量要这么写：

```kotlin
var name: String
```

但如果真这么写，会报错：

![image-20190618174946052](http://ww2.sinaimg.cn/large/006tNc79gy1g45gf14gukj30g405s3yv.jpg)

这个提示是在说，属性需要在声明的同时初始化，除非你把它声明成抽象的。

Java 里的 field 在 Kotlin 里叫 Property，不过它们其实不一样，Kotlin 的 Property 功能会多些。

变量还能抽象？嗯，这是 Kotlin 的功能，不过这里先不理它，后面会讲到。

为什么要初始化？因为 Kotlin 的变量是没有默认值的，这点不像 Java，Java 的 field 有默认值：

```java
String name; // 默认值是 null
int count; // 默认值是 0
```

但这些 Kotlin 是没有的。不过其实，Java 也只是 field 有默认值，局部变量也是没有默认值的，如果不给它初始值也会报错：

![image-20190618180036907](http://ww2.sinaimg.cn/large/006tNc79gy1g45gqbk9s2j30h605gweu.jpg)

好，那我们就给它一个默认值 null 吧。

![image-20190618180232613](http://ww3.sinaimg.cn/large/006tNc79gy1g45gsbviiaj30ks0603yy.jpg)

又不行，告诉我需要赋一个非空的值给它才行，怎么办？Java 的那套不管用了，算了我还是用 Java 吧。

其实这都是 Kotlin 的空安全设计相关的内容。很多人尝试上手 Kotlin 之后快速放弃，就是因为搞不明白它的空安全设计，导致代码各种拒绝编译，最终选择放弃。所以咱先别急，我先来给你讲一下 Kotlin 的空安全设计。

### Kotlin 的空安全设计

简单来说就是通过 IDE 的提示来避免调用 null 对象，从而避免 NullPointerException。其实 androidx 就有的，用一个注解就可以标记变量是否可能为空，然后 IDE 会帮助检测和提示：

![image-20190618181345475](http://ww2.sinaimg.cn/large/006tNc79gy1g45h3zlw4vj30re04o3yy.jpg)

而到了 Kotlin 这里，就有了语言级别的默认支持，而且从警告变成了报错（编译失败）：

![image-20190618181424759](http://ww1.sinaimg.cn/large/006tNc79gy1g45h4ofyn0j30i003i3yq.jpg)

在 Kotlin 里面，所有的变量默认都是不允许为空的，如果你给它赋值 null，就会报错，像上面那样。

这种有点强硬的要求，其实是很合理的：既然你声明了一个变量，就是要使用它对吧？那你把它赋值为 null 干嘛？要尽量让它有可用的值啊。Java 在这方面很宽松，我们成了习惯，但 Kotlin 更强的限制其实在你熟悉了之后，是会减少很多运行时的问题的。

不过，还是有些场景，变量的值真的无法保证空与否，比如你要从服务器取一个 JSON 数据，并把它解析成一个 User 对象：

![image-20190604173433383](http://ww4.sinaimg.cn/large/006tNc79gy1g449vf0i82j30sm0480sv.jpg)

这个时候，空值就是有意义的。对于这些可以为空值的变量，你可以在类型右边加一个 `?` 号，解除它的非空限制：

![image-20190604173503812](http://ww1.sinaimg.cn/large/006tNc79gy1g449w2j9z9j30oi03kt8u.jpg)

加了问号之后，一个 Kotlin 变量就像 Java 变量一样没有非空的限制，自由自在了。

你除了在初始化的时候可以给它赋值为空值，在代码里的任何地方也都可以：

![image-20190618182209270](http://ww2.sinaimg.cn/large/006tNc79gy1g45hcqd9idj30po08gwfx.jpg)

这种类型之后加 `?` 的写法，在 Kotlin 里叫**可空类型**。

不过，可空类型的变量会有新的问题：

由于对空引用的调用会导致空指针异常，所以 Kotlin 在可空变量直接调用的时候 IDE 会报错：

![image-20190618182525781](http://ww4.sinaimg.cn/large/006tNc79gy1g45hg50qy3j310409mjtl.jpg)

「可能为空」的变量，Kotlin 不允许用。那怎么办？用之前检查一下吧：

![image-20190601213438929](http://ww3.sinaimg.cn/large/006tNc79gy1g44anzrjp3j31ao066jsi.jpg)

哎？这怎么还报错？这个报错的意思是即使你检查了非空也不能保证下面调用的时候就是非空（多线程情况下，其他线程可能把它再改成空的）。

不过 Kotlin 里其实不是这么玩的，而是用 `?.`：

![image-20190618182658493](http://ww2.sinaimg.cn/large/006tNc79gy1g45hhqjzcbj30gw01wjrh.jpg)

也就是说，如果你要在 Kotlin 里使用一个可能为空的变量，代码大概是这样的：

![image-20190601215028877](http://ww3.sinaimg.cn/large/006tNc79gy1g45hint48uj31ew0ekjt8.jpg)

这个写法同样会对变量做一次非空确认之后再调用方法，这是 Kotlin 的写法，并且它可以做到线程安全，所以这种写法叫做  **safe call**。

另外还有一种双感叹号的用法：

![image-20190618182939108](http://ww2.sinaimg.cn/large/006tNc79gy1g45hkj81wqj30hc01waa5.jpg)

意思是告诉编译器，我保证这里的 view 一定是非空的，编译器你不要帮我做检查了，有什么后果我自己承担。

![âåå§ ç´§ç®å å­æç©º ä¸æç½éª¨ç²¾âçå¾çæç´¢ç»æ](http://ww3.sinaimg.cn/large/006tNc79gy1g45hop35j2j3085064aa1.jpg)

这种「肯定不会为空」的断言式的调用叫做 **non-null asserted call**。

一旦用了非空断言，实际上和 Java 就没什么两样了，但也就享受不到 Kotlin 的空安全设计带来的好处了（在编译时做检查，而不是运行时抛异常）。

以上就是 Kotlin 空安全设计。

理解了它之后再来看变量声明，跟 Java 虽然完全不一样，只是写法上不同而已。

很多人在上手的时候都被变量声明搞懵，原因就是 Kotlin 的空安全设计所导致的这些报错：

- 变量需要手动初始化，所以不初始化的话报错；
- 变量默认非空，所以初始化赋值 null 的话报错，之后再次赋值为 null 也会报错；
- 变量用 `?` 设置为可空的时候，使用的时候因为「可能为空」又报错。

关于空安全，最重要的是记住一点：所谓「可空不可空」，关注的全都是使用的时候，即「这个变量在使用时是否可能为空」。

另外，Kotlin 的这种空安全设计在与 Java 的互相调用上是完全兼容的，Java 里面的 @Nullable 注解，在 Kotlin 里调用时同样会触发编译器的空安全检查。

![image-20190617194307505](http://ww4.sinaimg.cn/large/006tNc79gy1g44e2o21h3j30e005yjrp.jpg)

![image-20190617194247150](http://ww1.sinaimg.cn/large/006tNc79gy1g44e2bg9xgj30x603qq3c.jpg)

空安全我们讲了这么多，但是有些时候我们声明一个变量是不会让它为空的：

![image-20190618201102556](http://ww2.sinaimg.cn/large/006tNc79gy1g45ki11atnj308e01mwef.jpg)

比如这个 view，其实在实际场景中我们希望它一直是非空的。

但如果你这么写：

![image-20190618201359804](http://ww2.sinaimg.cn/large/006tNc79gy1g45kl3k8qjj30n203mt94.jpg)

虽然编译器不会报错，运行起来就程序崩溃了，原因是 findViewById() 是在 onCreate 之后才能调用。

那怎么办呢？其实我们很想告诉编译器「我很确定我用的时候绝对不为空，但第一时间我没法给它赋值」。

Kotlin 给我们提供了一个选项：延迟初始化。

### 延迟初始化

具体是这么写的：

![image-20190604171730123](http://ww3.sinaimg.cn/large/006tNc79gy1g45knzhm9yj30py032q2x.jpg)

这个 `lateinit` 的意思是：告诉编译器我没法第一时间就初始化，但我肯定会在使用它之前完成初始化的。

它的作用就是让 IDE 不要对这个变量检查初始化和报错。换句话说，加了这个 `lateinit` 关键字，这个变量的初始化就全靠你自己了，编译器不帮你检查了。

然后我们就可以在 onCreate 中进行初始化了：

![image-20190618202428127](http://ww4.sinaimg.cn/large/006tNc79gy1g45kw003toj30ou080wfr.jpg)

当然，变量声明除了这么写：

![image-20190618202959727](http://ww2.sinaimg.cn/large/006tNc79gy1g45l1qurhlj30c201w3yi.jpg)

还可以这样写：

![image-20190618203037881](http://ww4.sinaimg.cn/large/006tNc79gy1g45l2er6oej308u01yt8n.jpg)

「这个是啥东西，怎么没有声明变量类型？」别害怕，这其实是用到了 Kotlin 的类型推断的特性。

### 类型推断

