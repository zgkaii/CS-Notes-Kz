## 一、Java生态圈

随着Java以及Java社区的不断壮大，Java也早已不再是简简单单的一门计算机语言了，它更是一个平台、一种文化、一个社区。

- 作为一个平台，Java虚拟机扮演着举足轻重的作用
  - Groovy、Scala、JRuby、Kotlin等都是Java平台的一部分。
- 作为一种文化，Java几乎成为了“开源”的代名词。
  - 第三方开源软件和框架。如Tomcat、Struts，MyBatis，Spring等。
  - 就连JDK和JVM自身也有不少开源的实现，如openJDK、Harmony。
- 作为一个社区
  * Java拥有全世界最多的技术拥护者和开源社区支持，有数不清的论坛和资料。
  * 应用广泛，从桌面应用软件、嵌入式开发到企业级应用、后台服务器、中间件，都可以看到Java的身影。

![](https://img-blog.csdnimg.cn/20201005161011148.png)

每个语言都需要转换成字节码文件，最后转换的字节码文件都能通过Java虚拟机进行运行和处理。

<img src="https://img-blog.csdnimg.cn/20201005161126652.png" style="zoom:67%;" />

随着Java7的正式发布，Java虚拟机的设计者们通过JSR-292规范基本实现在Java虚拟机平台上运行非Java语言编写的程序。

Java虚拟机根本不关心运行在其内部的程序到底是使用何种编程语言编写的，它只关心**“字节码”文件**。也就是说Java虚拟机拥有语言无关性，并不会单纯地与Java语言“终身绑定”，**只要其他编程语言的编译结果满足并包含Java虚拟机的内部指令集、符号表以及其他的辅助信息，它就是一个有效的字节码文件，就能够被虚拟机所识别并装载运行**。

**字节码**

我们平时说的java字节码，指的是用java语言编译成的字节码。准确的说任何能在jvm平台上执行的字节码格式都是一样的。所以应该统称为：**jvm字节码**。

不同的编译器，可以编译出相同的字节码文件，字节码文件也可以在不同的JVM上运行。

Java虚拟机与Java语言并没有必然的联系，它只与特定的**二进制文件格式**——Class文件格式所关联，Class文件中包含了Java虚拟机指令集（或者称为字节码、Bytecodes）和符号表，还有一些其他辅助信息。

**多语言混合编程**

Java平台上的多语言混合编程正成为主流，通过特定领域的语言去解决特定领域的问题是当前软件开发应对日趋复杂的项目需求的一个方向。

试想一下，在一个项目之中，并行处理用clojure语言编写，展示层使用JRuby/Rails，中间层则是Java，每个应用层都将使用不同的编程语言来完成。而且，接口对每一层的开发者都是透明的，各种语言之间的交互不存在任何困难，就像使用自己语言的原生API一样方便，因为它们最终都运行在一个虚拟机之上。

对这些运行于Java虚拟机之上Java之外的语言，来自系统级的、底层的支持正在迅速增强，以JSR-292为核心的一系列项目和功能改进（如Da Vinci Machine项目、Nashorn引擎、InvokeDynamic指令、java.lang.invoke包等），推动Java虚拟机从“Java语言的虚拟机”向 “多语言虚拟机”的方向发展。

## 二、虚拟机与Java虚拟机

### 2.1 虚拟机

虚拟机（Virtual Machine），就是一台虚拟的计算机。它是一款软件，用来执行一系列虚拟计算机指令。大体上，虚拟机可以分为**系统虚拟机**和**程序虚拟机**。

- 大名鼎鼎的Visual Box，Mware就属于系统虚拟机，它们完全是对物理计算机的仿真，提供了一个可运行完整操作系统的软件平台。
- 程序虚拟机的典型代表就是Java虚拟机，它专门为执行单个计算机程序而设计，在Java虚拟机中执行的指令我们称为Java字节码指令。

无论是系统虚拟机还是程序虚拟机，在上面运行的软件都被限制于虚拟机提供的资源中。

### 2.2 Java虚拟机

Java虚拟机是一台执行Java字节码的虚拟计算机，它拥有独立的运行机制，其运行的Java字节码也未必由Java语言编译而成。

JVM平台的各种语言可以共享Java虚拟机带来的**跨平台性、优秀的垃圾回器，以及可靠的即时编译器**。

Java技术的核心就是Java虚拟机（JVM，Java Virtual Machine），因为所有的Java程序都运行在Java虚拟机内部。

Java虚拟机就是二进制字节码的运行环境，负责装载字节码到其内部，解释/编译为对应平台上的机器指令执行。每一条Java指令，Java虚拟机规范中都有详细定义，如怎么取操作数，怎么处理操作数，处理结果放在哪里。

特点：

- 一次编译，到处运行
- 自动内存管理
- 自动垃圾回收功能

### 2.3 JVM的位置

JVM是运行在操作系统之上的，它与硬件没有直接的交互。

<img src="https://img-blog.csdnimg.cn/20201005164955443.png" style="zoom:67%;" />

Java的体系结构：

<img src="https://img-blog.csdnimg.cn/20201005202622207.png" style="zoom:80%;" />

**JDK——Java Development ToolKit（Java开发工具包）**是整个JAVA的核心，包括了Java运行环境（Java Runtime Envirnment），一堆Java工具和Java基础的类库。

最主流的JDK是Sun公司发布的JDK，除了Sun之外，还有很多公司和组织都开发了属于自己的JDK，例如国外IBM公司开发了属于自己的JDK，国内淘宝也开发了属于自己的JDK，各个组织开发自己的JDK都是为了在某些方面得到一些提高，以适应自己的需求。
 JDK有以下三种版本：

- J2SE，standard edition，标准版，是通常用的一个版本。
- J2EE，enterpsise edition，企业版，使用这种JDK开发J2EE应用程序。
- J2ME，micro edition，主要用于移动设备、嵌入式设备上的Java应用程序。

**JRE——Java Runtime Enviromental（Java运行时环境）**，也就是我们说的Java平台，所有的Java程序都要在JRE下才能运行。包括JVM和Java核心类库和支持文件。与JDK相比，它不包含开发工具：编译器、调试器和其他工具。

**JVM——Java Virtual Mechinal（JAVA虚拟机）**。JVM是JRE的一部分，它是一个虚构出来的计算机，是通过在实际的计算机上仿真模拟各种计算机功能来实现的。JVM有自己完善的硬件架构，如处理器、堆栈、寄存器等，还具有相应的指令系统。JVM的主要工作是解释自己的质量集（即字节码）并映射到本地的CPU的指令集或OS的系统调用。Java语言是跨平台运行的，其实就是不同的操作系统，使用不同的JVM映射规则，让其与操作系统无关，完成了跨平台性。JVM对上层的Java源文件是不关心的，它关注的只是由源文件生成的类文件。类文件的组成包括JVM指令集，符合表以及一些补助信息。

### 2.4 JVM整体结构

- HotSpot VM是目前市面上高性能虚拟机的代表作之一。
- 它采用解释器与即时编译器并存的架构。
- 在今天，Java程序的运行性能早已脱胎换骨，已经达到了可以和C/C++程序一较高下的地步。

<img src="https://img-blog.csdnimg.cn/20201005165116595.png" style="zoom:67%;" />

执行引擎包含三部分：解释器，及时编译器，垃圾回收器。

### 2.5 Java代码执行流程

<img src="https://img-blog.csdnimg.cn/20201005165116576.png" style="zoom:80%;" />

只是能生成被Java虚拟机所能解释的字节码文件，那么理论上就可以自己设计一套代码了

### 2.6 JVM的架构模型

Java编译器输入的指令流基本上是一种**基于栈**的指令集架构，另外一种指令集架构则是**基于寄存器**的指令集架构。

这两种架构之间的区别：

**基于栈式架构的特点**

- 设计和实现更简单，适用于资源受限的系统；
- 避开了寄存器的分配难题：使用零地址指令方式分配。
- 指令流中的指令大部分是零地址指令，其执行过程依赖于操作栈。**指令集更小**，编译器容易实现。
- 不需要硬件支持，可移植性更好，更好实现跨平台。

**基于寄存器架构的特点**

- 典型的应用是x86的二进制指令集：比如传统的PC以及Android的Davlik虚拟机。
- **指令集架构则完全依赖硬件，可移植性差**。
- **性能优秀和执行更高效**。
- 花费更少的指令去完成一项操作。
- 在大部分情况下，基于寄存器架构的指令集往往都以一地址指令、二地址指令和三地址指令为主，而基于栈式架构的指令集却是以零地址指令为主。

**举例1**

同样执行2+3这种逻辑操作，其指令分别如下：

基于栈的计算流程（以Java虚拟机为例）：

```bash
0: iconst_2 // 常量2入栈
1: istore_1
2: iconst_3 // 常量3入栈
3: istore_2
4: iload_1
5: iload_2
6: iadd // 常量2/3出栈，执行相加
7: istore_3 // 结果5入栈
8: return
```

而基于寄存器的计算流程：

```bash
mov eax,2 //将eax寄存器的值设为1
add eax,3 //使eax寄存器的值加3
```

**字节码反编译**

我们编写一个简单的代码，然后查看一下字节码的反编译后的结果：

```java
public class StackStruTest {
    public static void main(String[] args) {
        int i = 2 + 3;
    }
}
```

然后我们找到编译后的 class文件，使用下列命令进行反编译：

```bash
javap -v StackStruTest.class
```

得到的文件为:

```java
 public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=1, locals=2, args_size=1
         0: iconst_5
         1: istore_1
         2: return
      LineNumberTable:
        line 10: 0
        line 14: 2
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       3     0  args   [Ljava/lang/String;
            2       1     1     i   I

```

倘若代码为：

```java
public class StackStruTest {
    public static void main(String[] args) {
        int i = 2;
        int j = 3;
        int k = i + j;
    }
}
```

我们找到编译后的 class文件，使用下列命令进行反编译得到后的文件：

```java
  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=4, args_size=1
         0: iconst_2
         1: istore_1
         2: iconst_3
         3: istore_2
         4: iload_1
         5: iload_2
         6: iadd
         7: istore_3
         8: return
      LineNumberTable:
        line 11: 0
        line 12: 2
        line 13: 4
        line 14: 8
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
            0       9     0  args   [Ljava/lang/String;
            2       7     1     i   I
            4       5     2     j   I
            8       1     3     k   I
```

**总结**

**由于跨平台性的设计，Java的指令都是根据栈来设计的**。不同平台CPU架构不同，所以不能设计为基于寄存器的。

栈的特点：

- 跨平台性
- 指令集小
- 指令多
- 执行性能比寄存器差

## 三、JVM生命周期

### 3.1 虚拟机的启动

Java虚拟机的启动是通过引导类加载器（bootstrap class loader）创建一个初始类（initial class）来完成的，这个类是由虚拟机的具体实现指定的。

### 3.2 虚拟机的执行

- 一个运行中的Java虚拟机有着一个清晰的任务：执行Java程序。
- 程序开始执行时他才运行，程序结束时他就停止。
- **执行一个所谓的Java程序的时候，真真正正在执行的是一个Java虚拟机的进程**。

### 3.3 虚拟机的退出

有如下的几种情况：

- 程序正常执行结束

- 程序在执行过程中遇到了异常或错误而异常终止
- 由于操作系统用现错误而导致Java虚拟机进程终止
- 某线程调用Runtime类或system类的exit方法，或Runtime类的halt方法，并且Java安全管理器也允许这次exit或halt操作。
- 除此之外，JNI（Java Native Interface）规范描述了用JNI Invocation API来加载或卸载 Java虚拟机时，Java虚拟机的退出情况。

## 四、JVM虚拟机分类

### 4.1 HotSpot VM

HotSpot历史最初由一家名为“Longview Technologies”的小公司设计。1997年，此公司被sun收购；2009年，Sun公司被甲骨文收购。

在JDK1.3版本时，HotSpot VM就成为默认虚拟机。

目前Hotspot占有绝对的市场地位，是**绝对的主流**。

- 不管是现在仍在广泛使用的JDK6，还是使用比例较多的JDK8中，默认的虚拟机都是HotSpot。
- Sun/Oracle JDK和openJDK的默认虚拟机。
- 从服务器、桌面到移动端、嵌入式都有应用。

HotSpot指的就是它的热点代码探测技术。

- 通过计数器找到最具编译价值代码，触发即时编译或栈上替换。
- 通过编译器与解释器协同工作，在最优化的程序响应时间与最佳执行性能中取得平衡。

### 4.2 JRockit

JRockit专注于服务器端应用。

- 它可以不太关注程序启动速度，因此JRockit内部不包含解析器实现，全部代码都靠即时编译器编译后执行。

大量的行业基准测试显示，JRockit JVM是世界上最快的JVM。

- 使用JRockit产品，客户已经体验到了显著的性能提高（一些超过了70%）和硬件成本的减少（达50%）。

优势：全面的Java运行时解决方案组合。

- JRockit面向延迟敏感型应用的解决方案JRockit Real Time提供以毫秒或微秒级的JVM响应时间，适合财务、军事指挥、电信网络的需要。
- MissionControl服务套件，它是一组以极低的开销来监控、管理和分析生产环境中的应用程序的工具。

2008年，JRockit被Oracle收购。

Oracle表达了整合两大优秀虚拟机的工作，大致在JDK8中完成。整合的方式是在HotSpot的基础上，移植JRockit的优秀特性。

### 4.3 IBM的J9

全称：IBM Technology for Java Virtual Machine，简称IT4J，内部代号：J9。

市场定位与HotSpot接近，服务器端、桌面应用、嵌入式等多用途VM广泛用于IBM的各种Java产品。

目前，有影响力的三大商用虚拟机之一，也号称是世界上最快的Java虚拟机。

2017年左右，IBM发布了开源J9VM，命名为openJ9，交给EClipse基金会管理，也称为Eclipse OpenJ9。

### 4.4 Azul VM

前面三大“高性能Java虚拟机”使用在通用硬件平台上这里Azu1VW和BEALiquid VM是与特定硬件平台绑定、软硬件配合的专有虚拟机I

- 高性能Java虚拟机中的战斗机。

Azul VM是Azu1Systems公司在HotSpot基础上进行大量改进，运行于Azul Systems公司的专有硬件Vega系统上的ava虚拟机。

每个Azu1VM实例都可以管理至少数十个CPU和数百GB内存的硬件资源，并提供在巨大内存范围内实现可控的GC时间的垃圾收集器、专有硬件优化的线程调度等优秀特性。

2010年，AzulSystems公司开始从硬件转向软件，发布了自己的zing JVM，可以在通用x86平台上提供接近于Vega系统的特性。

### 4.5 KVM和CDC / CLDC  Hotspot

Oracle在Java ME产品线上的两款虚拟机为：CDC/CLDC HotSpot Implementation VM KVM（Kilobyte）是CLDC-HI早期产品目前移动领域地位尴尬，智能机被Angroid和IOS二分天下。

KVM简单、轻量、高度可移植，面向更低端的设备上还维持自己的一片市场。

- 智能控制器、传感器
- 老人手机、经济欠发达地区的功能手机

### 4.6 Sun Classic VM

早在1996年Java1.0版本的时候，Sun公司发布了一款名为sun classic VM的Java虚拟机，它同时也是**世界上第一款商用Java虚拟机**，JDK1.4时完全被淘汰。

这款虚拟机内部只提供解释器。现在还有及时编译器，因此效率比较低，而及时编译器会把热点代码缓存起来，那么以后使用热点代码的时候，效率就比较高。

如果使用JIT编译器，就需要进行外挂。但是一旦使用了JIT编译器，JIT就会接管虚拟机的执行系统。解释器就不再工作。解释器和编译器不能配合工作。

现在hotspot内置了此虚拟机。

### 4.7 Apache Marmony

Apache也曾经推出过与JDK1.5和JDK1.6兼容的Java运行平台Apache Harmony。

它是IElf和Inte1联合开发的开源JVM，受到同样开源的openJDK的压制，Sun坚决不让Harmony获得JCP认证，最终于2011年退役，IBM转而参与OpenJDK

虽然目前并没有Apache Harmony被大规模商用的案例，但是它的Java类库代码吸纳进了Android SDK。

### 4.8 Taobao VM

由AliJVM团队发布。阿里，国内使用Java最强大的公司，覆盖云计算、金融、物流、电商等众多领域，需要解决高并发、高可用、分布式的复合问题。有大量的开源产品。

基于openJDK开发了自己的定制版本AlibabaJDK，简称AJDK。是整个阿里Java体系的基石。

基于openJDK Hotspot VM发布的国内第一个优化、深度定制且开源的高性能服务器版Java虚拟机。

- 创新的GCIH（GCinvisible heap）技术实现了off-heap，即将生命周期较长的Java对象从heap中移到heap之外，并且Gc不能管理GCIH内部的Java对象，以此达到降低GC的回收频率和提升Gc的回收效率的目的。
- GCIH中的对象还能够在多个Java虚拟机进程中实现共享
- 使用crc32指令实现JvM intrinsic降低JNI的调用开销
- PMU hardware的Java profiling tool和诊断协助功能
- 针对大数据场景的ZenGc 

taobao vm应用在阿里产品上性能高，硬件严重依赖inte1的cpu，损失了兼容性，但提高了性能。

目前已经在淘宝、天猫上线，把oracle官方VM版本全部替换了。

### 4.9 Dalvik VM

谷歌开发的，应用于Android系统，并在Android2.2中提供了JIT，发展迅猛。

Dalvik y只能称作虚拟机，而不能称作“Java虚拟机”，它没有遵循 Java虚拟机规范

不能直接执行Java的Class文件

基于寄存器架构，不是jvm的栈架构。

执行的是编译以后的dex（Dalvik Executable）文件。执行效率比较高。

- 它执行的dex（Dalvik Executable）文件可以通过class文件转化而来，使用Java语法编写应用程序，可以直接使用大部分的Java API等。

Android 5.0使用支持提前编译（Ahead of Time Compilation，AoT）的ART VM替换Dalvik VM。

### 4.10 Graal VM

2018年4月，oracle Labs公开了GraalvM，号称 "Run Programs Faster Anywhere"，勃勃野心。与1995年java的”write once，run anywhere"遥相呼应。

GraalVM在HotSpot VM基础上增强而成的跨语言全栈虚拟机，可以作为“任何语言”
的运行平台使用。语言包括：Java、Scala、Groovy、Kotlin；C、C++、Javascript、Ruby、Python、R等

支持不同语言中混用对方的接口和对象，支持这些语言使用已经编写好的本地库文件

工作原理是将这些语言的源代码或源代码编译后的中间格式，通过解释器转换为能被Graal VM接受的中间表示。Graal VM提供Truffle工具集快速构建面向一种新语言的解释器。在运行时还能进行即时编译优化，获得比原生编译器更优秀的执行效率。

**总结**

具体JVM的内存结构，其实取决于其实现。不同厂商的JVM，或者同一厂商发布的不同版本，都有可能存在一定差异。我们学习及开发都主要以**oracle HotSpot VM**为默认虚拟机。