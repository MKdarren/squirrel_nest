

### 规则引擎

#### 一、概述

 规则引擎由推理引擎发展而来，是一种嵌入在应用程序中的组件，实现了将业务决策从应用程序代码中分离出来，并使用预定义的语义模块编写业务决策。

  规则引擎具体执行可以分为接受数据输入，解释业务规则，根据业务规则做出业务决策几个过程。
  使用规则引擎可以把复杂、冗余的业务规则同整个支撑系统分离开，做到架构的可复用移植。
  规则引擎通常允许您在不重新启动系统或部署新的可执行代码的情况下更改规则。规则引擎不是一个新的东西的魔法盒，它旨在成为一个提供更高级别抽象的工具，以便您可以更少地关注开发细节。



#### 二、分类

**常用规则引擎 Drools、QlExpress、Groovy、Aviator**

其他的规则引擎IIlog JRules(最有名的商用BRMS), Visual Rules(国内商业规则引擎品牌)，Jess(AI系的代表)



###### 1. Drools (适用语言java, Python)

###### 2. QlExpress (适用语言java)

###### 3. Groovy (适用语言java)

###### 4.  Aviator (适用语言java)



##### a. Drools



###### 简介

Drools 是用 Java 语言编写的开放源码规则引擎，基于Apache协议，基于RETE算法，于2005年被JBoss收购。

Drools 是用 Java 语言编写的开放源码规则引擎，使用 Rete 算法对所编写的规则求值，允许使用声明方式表达业务逻辑，将复杂多变的规则从硬编码中解放出来，以规则脚本的形式存放在文件中，使得规则的变更不需要修正代码重启机器就可以立即在线上环境生效.



###### 特点:  

1. 简化系统架构，优化应用
2. 提高系统的可维护性和维护成本
3. 方便系统的整合
4. 减少编写“硬代码”业务规则的成本和风险
5. 最活跃的开源规则引擎

   

##### b. QLExpress



###### 简介

一个轻量级的类java语法规则引擎，作为一个嵌入式规则引擎在业务系统中使用。让业务规则定义简便而不失灵活。让业务人员就可以定义业务规则。支持标准的JAVA语法，还可以支持自定义操作符号、操作符号重载、函数定义、宏定义、数据延迟加载等。

QLExpress在阿里集团内部有很强的影响力，被广泛应用在电商场景中，在业务灵活多变的场景下常常需要规则引擎的支持。



###### 特点

1. 不依赖于任何第三方的java 库
2. 支持标准的JAVA语法，可以支持自定义操作符号、操作符号重载、函数定义、宏定义、数据延迟加载等
3. 可读性和功能更贴合业务需要，可以使业务的灵活度大大增强
4. 线程安全，引擎运算过程中的产生的临时变量都是threadlocal类型
5. 高效执行，比较耗时的脚本编译过程可以缓存在本地机器，运行时的临时变量创建采用了缓冲池的技术
6. 安全控制,可以通过设置相关运行参数，预防死循环、高危系统api调用等情况
7. 代码精简，依赖最小，250k的jar包适合所有java的运行环境，在android系统的低端pos机也得到广泛运用



###### 缺点：

qlExpress本身只是一个脚本语言，需要被封装成规则引擎使用



##### c. Groovy



###### 简介

groovy是在java平台上的、具有象Python，Ruby和Smalltalk语言特性的灵活动态语言，groovy保证了这些特性象java语法一样被java开发者使用, groovy代码被编译成java字节码，然后能集成到java应用程序中或者web应用程序，整个应用程序都可以是groovy编写的 — groovy是非常灵活的。

groovy与java平台非常融合，groovy的许多代码是使用java实现的，其余部分是用groovy实现的，当你使用groovy编程的时候，许多情况下你正在写特殊的java程序，在java平台上的所有强大功能——包括大量的java类库也可以直接在groovy中使用



###### 特点

1. Groovy是一种动态语言，它和Java一样，也运行于Java虚拟机中，并且可以使用Java所有的库
2. 结合了Python、Ruby和Smalltalk的许多强大的特性
3. 可以作为编程语言也可以作为脚本语言



##### d. Aviator



###### 简介

Aviator的设计目标是轻量级和高性能 ，Aviator非常小，加上依赖包也才450K,不算依赖包的话只有70K；当然，Aviator的语法是受限的，它不是一门完整的语言，而只是语言的一小部分集合。

其次，Aviator的实现思路与其他轻量级的求值器很不相同，其他求值器一般都是通过解释的方式运行，而Aviator则是直接将表达式编译成Java字节码，交给JVM去执行。

**Aviator的定位是介于Groovy这样的重量级脚本语言和IKExpression这样的轻量级表达式引擎之间**



#### 三、性能比较



###### 1.测试



硬件：Core2 7250 2G双核/2G内存

操作系统：Win7

JDK ：1.6.0.24

Drools ：5.1

IKExpression ：2.1.2

Aviator：2.0

Groovy：1.8

运行JVM参数为：-Xms512m -Xmx512m -XX:CompileThreshold=10000 -XX:MaxPermSize=128m

针对同一功能的表达式，分别执行100万次，每次跑三遍

```bash
执行结果为：
execute Drools total time = 66318ms
execute Drools total time = 66303ms
execute Drools total time = 66802ms

execute IKExpresion total time = 12603ms
execute Aviator total time = 4855ms
execute Groovy total time = 1722ms

execute IKExpresion total time = 12465ms
execute Aviator total time = 5035ms
execute Groovy total time = 1841ms

execute IKExpresion total time = 12591ms。
execute Aviator total time = 4809ms
execute Groovy total time = 1784ms

```



从执行100万次表达式求值看，Groovy最快，Aviator其次，IKExpression然后，Drools最慢. 数据统计图如下

![](/Users/zhoulibin/OneDrive/markDown 图片/规则引擎1.jpg)

![](/Users/zhoulibin/OneDrive/markDown 图片/规则引擎2.jpg)



**Groovy是最快的，一秒钟可以执行56万次！**



###### 2.分析



Drools是一个高性能的规则引擎，但是设计的使用场景和在本次测试中的场景并不太一样，Drools的目标是一个复杂对象比如有上百上千的属性，怎么快速匹配规则，而不是简单对象重复匹配规则，因此在这次测试中结果垫底。

IKExpression是依靠解释执行来完成表达式的执行，因此性能上来说也差强人意，和Aviator，Groovy编译执行相比，还是性能差距还是明显。

Aviator会把表达式编译成字节码，然后代入变量再执行，整体上性能做得很好

Groovy是动态语言，依靠反射方式动态执行表达式的求值，并且依靠JIT编译器，在执行次数够多以后，编译成本地字节码，因此性能非常的高。对应于eSOC这样需要反复执行的表达式，Groovy是一种强大的功能规则引擎，简洁的语法，和Java完美集成





#### 四、拓展



以上对比发现Groovy性能非常好，详细的分析下为什么！

上文有提到Groovy是动态语言，依靠反射方式动态执行表达式的求值，并且依靠JIT编译器，在执行次数够多以后，编译成本地字节码，因此性能非常的高，所以看下JIT对Groovy的性能影响.

```bash
#当VM的参数CompileThreshold = 10000
VM Args:-Xms64m -Xmx64m -XX:CompileThreshold=10000

execute IKExpresion total time = 12553ms

execute Aviator total time = 4900ms

execute Groovy total time = 1782ms

#当VM的参数CompileThreshold = 1000000
VM Args:-Xms64m -Xmx64m -XX:CompileThreshold=1000000
execute IKExpresion total time = 45913ms
execute Aviator total time = 8914ms
execute Groovy total time = 18559ms

```



###### 注：

因为我们测试的是执行100万次，以上通过改变CompileThreshold的值来控制JIT对执行结果的影响，

-XX:CompileThreshold为 JIT编译的阈值， 当函数的调用次数超过-XX:CompileThreshold时，JIT就将字节码编译成本地机器码. 在Client 模式下， XX:CompileThreshold 的取值为1500, 在Server 模式下， 取值是 10000.

JIT编译完成后， JVM便会使用本地代码代替原来的字节码解释执行。



数据对比整理结果：

![](/Users/zhoulibin/OneDrive/markDown 图片/规则引擎3.jpg)



可以明显的看出，Groovy执行时间变慢了，变为原来的11倍左右，IKExpression也差不多慢了4倍，Aviator本身就编译成为了字节码，因此受到的影响较小，时间为原来的2倍。也就是说原来Groovy从执行1万次的解释执行以后，后面的99万次由JIT编译器编译为本地字节码后，本地字节码的性能是解释执行的11倍！

那么大家可能有个疑问，是不是JIT都是好的呢，我们什么代码都让JIT编译为本地字节码，这样不是性能就非常高了。其实不然，这个和你的应用场景是密切相关的，如果你的代码执行的次数不够，那么就没有必要编译为本地字节码，否则执行性能的提升的幅度还抵消不了JIT编译浪费的时间。JIT默认都是开启的，在JVM的 client模式CompileThreshold=1500，server模式是CompileThreshold=10000。更多一点的信息，可以参考Java关于JIT的原理和相关知识.
