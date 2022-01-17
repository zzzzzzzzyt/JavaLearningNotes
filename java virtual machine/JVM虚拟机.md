# <u>JVM虚拟机</u>

在idea中安装了一个插件  jclasslib Bytecode viewer 可以直接看编译完的操作流程

**自己先把重点摘出来**



------



# 内存与垃圾回收篇



![image-20211122132805276](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122132805276.png)



## ==类加载子系统==



类加载子系统作用

![image-20211122133742193](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122133742193.png)

类的加载过程

![image-20211122134236162](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122134236162.png)





### 类的加载过程



#### 类的加载过程一：Loading

![image-20211122134457237](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122134457237.png)



![image-20211122134739707](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122134739707.png)

#### 类的加载过程二：Linking

![image-20211122134839686](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122134839686.png)

#### 类的加载过程三：Initialization

![image-20211122135626023](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122135626023.png)

**tips：**

**1、如果当前的类中没有声明静态变量和没有静态代码块，则不会存在<clinit>类构造器方法**

**2、任何一个类声明以后，内部至少存在一个类的构造器**

**例子**：为什么能直接给number赋值  因为它再linking的prepare阶段已经被初始化为0

![image-20211122140452925](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122140452925.png)



### 类加载器的分类

![image-20211122143015866](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122143015866.png)

![image-20211122143723109](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122143723109.png)

**tips:**

**1、对用户自定义类来说：默认使用系统类加载器进行加载**

**2、Java的核心类库都是使用引导类加载器进行加载的**

**3、在程序中获取不到引导类加载器，因为它是由c/c++进行编写的**



#### 启动类加载器

![image-20211122144521742](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122144521742.png)



####  扩展类加载器

在idea中打印时它的简写是ExtClassLoader

![image-20211122144845102](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122144845102.png)

 

#### 应用程序类加载器

![image-20211122145118109](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122145118109.png)

#### 自定义加载器



**什么时候使用自定义加载器**

![image-20211122145922300](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122145922300.png)







 **用户自定义类加载器 实现步骤**

![image-20211122150323963](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122150323963.png)



#### ClassLoader的常用方法即获取方法

**(简单了解下)**

![image-20211122150644917](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122150644917.png)

![image-20211122150931893](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122150931893.png)



### 双亲委派机制



**什么是双亲委派机制**

![image-20211122151757576](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122151757576.png)



**双亲委派机制工作原理**



![image-20211122152527289](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122152527289.png)



例子1：

![image-20211122153722854](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122153722854.png)

执行main方法时候 向上加载ClassLoader    然后引导类加载器加载后发现 string是没有main方法的 因为这是加载不到当前类



例子2：

![image-20211122154326220](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122154326220.png)

在java.lang包下面根本没有这个类  所以 引导类加载器加载时抛出安全异常  这个lang包是有访问权限的 它是阻止我们在这个包下自定义类（起到保护作用）







**沙箱安全机制**

![image-20211122154747918](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122154747918.png)

上面这个例子1、2就是沙箱安全机制起了作用





**双亲委派机制的优势**

1、避免类的重复加载

2、保护程序安全，防止核心API被随意修改（看例子1、例子2）





### 其他 

#### 1、在JVM中表示两个class对象是否为同一个类存在两个必要条件：

![image-20211122155345926](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122155345926.png)



#### 2、对类加载器的引用

![image-20211122155541703](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122155541703.png)



**3、类的主动使用和被动使用**

![image-20211122155645829](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122155645829.png)



## ==运行时数据区==

### 运行时数据区概述及线程

![image-20211122132805276](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122132805276.png)

运行时数据区：灰色的为单独线程私有的，红色的为多个线程共享的。

![image-20211122161731510](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122161731510.png)

一个JVM实例对应一个Runtime实例



**程序计数器不会报异常 没有GC**

**虚拟机栈和本地方法栈会报异常 没有GC**

**堆和方法区（JDK7 永久代  JDK8 元空间）会报异常 有GC**



#### 线程

![image-20211122162409321](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122162409321.png)



### 程序计数器（PC寄存器）



#### **PC Register介绍**

![image-20211122163202791](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122163202791.png)





**作用**

![image-20211122163518883](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122163518883.png)



**介绍**

![image-20211122164129940](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122164129940.png)

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122164205493.png" alt="image-20211122164205493" style="zoom:90%;" />







**例子：PC寄存器的意义  作用**

![image-20211122165105643](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122165105643.png)



#### **PC寄存器面试中常问的两个问题**



**问题1：**

![image-20211122165254532](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122165254532.png)

**问题2：**

![image-20211122165431839](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211122165431839.png)





### 虚拟机栈

#### 虚拟机栈概述

==栈是运行时的单位，而堆是存储的单位==



![image-20211123133955696](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123133955696.png)





**举例子**

![image-20211123133643259](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123133643259.png)

**注意一个个方法就代表了一个个栈帧**



##### **栈的特点（优点）**

 ![image-20211123134140606](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123134140606.png)

##### 面试题：开发中遇到的异常有哪些？

==栈中可能出现的异常==

![image-20211123134454134](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123134454134.png)



##### 设置栈内存大小

![image-20211123165944311](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123165944311.png)

**在idea中设置的方法**

![image-20211123135424178](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123135424178.png)



👇**修改后运行事例**

![image-20211123135328696](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123135328696.png)





#### 栈的存储单位



##### 栈中存储什么？

![image-20211123140423483](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123140423483.png)



##### 线程运行原理

![image-20211123140805225](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123140805225.png)

执行完毕弹出栈

tips:

1、不同线程中所包含的栈帧是不允许互相引用的，即不可能在一个栈帧之中引用另一个线程的栈帧

2、Java方法有两种返回函数的方式，一种是正常的函数返回，使用return指令；另外一种是抛出异常。两种方式，都会导致栈帧被弹出。



#### 栈帧的内部结构

![image-20211123142742212](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123142742212.png)







#### 局部变量表（虚拟机栈中的一部分）

![](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123144344935.png)

![image-20211123145210859](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123145210859.png)



👇 看看例子  局部变量表

 ![image-20211123151555696](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123151555696.png)

![image-20211123151626135](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123151626135.png)

![image-20211123151638677](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123151638677.png)



![image-20211123151654312](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123151654312.png)

![image-20211123151732644](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123151732644.png)

![image-20211123151817805](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123151817805.png)



##### 局部变量表  最基本的存储单元是Slot（变量槽）

![image-20211123152303507](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123152303507.png)

![image-20211123152725526](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123152725526.png)





👇例子​  ​自己要能分析

![image-20211123153034450](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123153034450.png)





👇例子 有重复利用  变量c使用之前已经销毁的变量b占据的slot的位置

![image-20211123153329777](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123153329777.png)







##### 局部变量表的补充说明



![image-20211123154149247](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123154149247.png)





#### 操作数栈（虚拟机栈中的一部分）

![image-20211123154805395](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123154805395.png)



![image-20211123155513673](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123155513673.png)

![image-20211123155722374](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123155722374.png)

##### 代码追踪（看实例代码 来理解）  

**这里操作数栈容量只有2 自己好好理解**

![image-20211123160318766](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123160318766.png)



![image-20211123160530826](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123160530826.png)



//iadd操作就是将操作数栈中的两个数取出 然后通过执行引擎在cpu中运算        然后再压回操作栈中





#### 栈顶缓存技术（了解下即可）

他们提出的技术

**将栈顶元素全部缓存在物理CPU的寄存器中，以此降低对内存的读/写次数，提升执行引擎的执行效率**



#### 动态链接（或指向运行时常量池的方法引用）（虚拟机栈中的一部分）

![image-20211123164156147](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123164156147.png)



例子👇   动态链接指向常量池

![image-20211123164212018](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123164212018.png)

![image-20211123164224642](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123164224642.png)





**为什么需要常量池呢？**

（字节码文件需要很多的数据支持 但通常这些数据很大以至于我们不能直接保存到字节码文件中，所以通过符号引用）

常量池的作用，就是为了提供一些符号和常量，便于指令的识别





#### 方法的调用：解析与分派

![image-20211123180949259](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123180949259.png)

![image-20211123181117306](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123181117306.png)



//为什么会产生早期绑定和晚期绑定的原因

![image-20211123182510716](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123182510716.png)



##### 解释：虚方法与非虚方法

![image-20211123183335970](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123183335970.png)





**虚拟机中提供了以下几条方法调用指令：**



![image-20211123183533217](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123183533217.png)



👇看例子：

![image-20211123183853975](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123183853975.png)

![image-20211123183931495](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123183931495.png)



//下面这个show() 也是子类定义的方法 用这个体现下 调用的情况

![image-20211123184021641](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123184021641.png)

**得出结果**

![image-20211123184836539](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123184836539.png)

![image-20211123184919059](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123184919059.png)



##### 方法的调用：关于invokedynamic指令



![image-20211123185250717](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123185250717.png)



**动态类型语言和静态类型语言**



![image-20211123185737611](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123185737611.png)



//lambda表达式使得java表达式一定程度具备了动态类型语言的特点



##### 方法的调用：方法重写的本质

![image-20211123190620027](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123190620027.png)



**为了减少频繁的使用动态分派    提高性能  jvm采用在类的方法区建立一个虚方法表**

![image-20211123190942293](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123190942293.png)



👇例子1：

![image-20211123191256193](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123191256193.png)



👇例子2：

![image-20211123191525453](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123191525453.png)



![image-20211123191655482](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123191655482.png)



![image-20211123191853463](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211123191853463.png)





#### 方法的返回地址（虚拟机栈中的一部分）

![image-20211124134533915](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124134533915.png)

（退出之后，需要恢复上层方法的局部变量表、操作数栈、将返回值压入调用者栈帧的操作数栈、设置PC寄存器值等，让调用者和方法继续执行下去）



##### **正常退出和异常退出的区别**

![image-20211124134605547](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124134605547.png)



##### **正常退出的返回**

![image-20211124135102273](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124135102273.png)

 

##### **异常退出的返回**

![image-20211124135425132](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124135425132.png)





#### 一些附加信息（虚拟机栈中的一部分）（了解）



**栈帧中还允许携带与Java虚拟机实现相关的一些附加信息。例如，对程序调试提供支持的信息。**



#### 栈的相关面试题

##### 举例栈溢出的情况？（StackOverflowError）

​	通过-Xss设置栈的大小；如果栈的大小是固定的话  会出现栈溢出情况；如果栈大小是变化的话，可能会出现OOM

##### 调整栈大小，就能保证不出现溢出吗？

​	不能

##### 分配的占内存越大越好吗？

​	不是！对于自身栈可能会好  减缓栈溢出的到来 但是挤占了其他栈的空间  其他栈空间变小

##### 垃圾回收是否会涉及到虚拟机栈？

​	不会   虚拟机栈存在Error  但不存在GC

##### 方法中定义的局部变量是否线程安全？

​	具体问题具体分析

​	👇例子

![image-20211124142837838](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124142837838.png)

![image-20211124143117513](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124143117513.png)

![image-20211124143204180](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124143204180.png)



### 本地方法栈

（学习本地方法栈  先了解下什么是本地方法接口）

####  ==本地方法接口、本地方法接口==



什么是本地方法？

使用native关键字修饰的方法就称为本地方法 （标识符native可以与所有其他的java标识符连用，但是abstract除外）

native代表调用的是本地方法  它有方法体但不是java代码实现的，abstract代表的是抽象方法 没有方法体

![image-20211124143503430](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124143503430.png)



为什么要使用Native Method？



![image-20211124144548449](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124144548449.png)

![image-20211124144613678](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124144613678.png)



现状

目前该方法使用的越来越少了，除非是与硬件有关的应用



#### ==本地方法栈==

==Java虚拟机栈用于管理Java方法的调用，而本地方法栈用于管理本地方法的调用    其他和虚拟机栈一致==   

![image-20211124145713266](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124145713266.png)





==不是所有的JVM都支持本地方法栈==

![image-20211124150105342](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124150105342.png)



### 堆



#### 堆的核心概述

##### 概述

==一个进程中的多个线程共享堆空间    但不是所有堆空间都是共享的，每个线程在堆内都有一块TLAB 私有的缓冲区==

![image-20211124155612469](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124155612469.png)

![image-20211124160201422](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124160201422.png)



👇例子  证明了创建了就分配内存空间

![image-20211124155146551](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124155146551.png)



![image-20211124155157632](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124155157632.png)

将以上两个程序编译后 修改参数 然后启动

然后在jdk文件夹中有 下面这个  启动

![image-20211124155316338](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124155316338.png)



![image-20211124155438530](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124155438530.png)

![image-20211124155459184](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124155459184.png)



##### 内存细分

![image-20211124161514813](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124161514813.png)

==记住这个约定 概念都是一样的== 

**面试题问到jdk8中有什么变化的话  记得要回答堆内存的划分  永久区改成了元空间**

堆空间是只包括新生代和老年代

![image-20211124162004423](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124162004423.png)





#### 设置堆内存大小与OOM



![image-20211124162533191](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124162533191.png)

**设置的内存大小和最后获得的内存大小不同的原因是，Eden Space和Survivor Space，只存在伊甸园区和两个幸存者区之一，另一个幸存者区是不放数据的**



##### 查看你设置的参数

![image-20211124164551929](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124164551929.png)

方式二必须是程序执行完之后才能进行打印  打印GC的处理细节

例子👇

![image-20211124165505138](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124165505138.png)

![image-20211124165446937](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124165446937.png)

![image-20211124165527778](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124165527778.png)

![image-20211124165519852](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124165519852.png)



**OutOfMemory举例**

![image-20211124182705905](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211124182705905.png)





#### 年轻代与老年代



![image-20211125132925002](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125132925002.png)



##### 调整参数步骤（一般情况下是不进行修改的）



**新生代与老年代的比例。默认值是2**

![image-20211125133209024](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125133209024.png)



**同时可以调整伊甸园区和幸存者区的比例（默认值是8  但是实际上并不是  因为有个自适应 如果要想8：1：1需要自己去显式指定下）**  

![image-20211125134305654](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125134305654.png)

![image-20211125135128696](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125135128696.png)



#### 图解对象分配过程

##### **概述**

**伊甸园区满了  会触发YGC   幸存者区满了 不会触发，  注意这不代表幸存者区不会进行垃圾回收 ，在伊甸园区满了触发YGC时会同时对幸存者区进行回收，还有些特殊情况  直接晋升到老年代  下面会讲**

![image-20211125135330305](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125135330305.png)

##### **图解**

![image-20211125140656268](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125140656268.png)



**对象分配的特殊过程**

![image-20211125141512964](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125141512964.png)





##### 总结

![image-20211125140800719](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125140800719.png)





**举例子**👇

加载过程   在老年代满的时候  就会进行Major GC 如果回收了还是满  就报oom

![image-20211125142032555](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125142032555.png)



**之后还有很多的调优工具需要进行学习**



#### Minor GC、Major GC、Full GC



调优的目的就是让GC用的少一点  



##### 概述

![image-20211125143548199](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125143548199.png)



##### 年轻代GC(Minor GC)触发机制：

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125143758490.png" alt="image-20211125143758490" style="zoom:90%;" />



##### 老年代GC(Major GC/Full GC)触发机制：

![image-20211125144138620](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125144138620.png)



##### Full GC触发机制：==（后面细讲）==

![image-20211125144304860](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125144304860.png)



#### 堆空间分代思想

==为什么需要把Java堆分代？不分代就不能正常工作了吗？==

（就像要把好学生坏学生分开一样  如果给坏学生辅导基础知识，好学生是没有必要被进行辅导的啊 减少时间的浪费）

![image-20211125150038979](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125150038979.png)







#### 内存分配策略

其实就是上面的总结

![image-20211125151849031](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125151849031.png)



![image-20211125152154215](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125152154215.png)

空间分配担保：后面会细说





#### 为对象分配内存：TLAB



==为什么要有TLAB(Thread Local Allocation Buffer)？==

![image-20211125152848603](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125152848603.png)

==什么是TLAB？==

![image-20211125153326543](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125153326543.png)

==TLAB的再说明==

![image-20211125153428504](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125153428504.png)



==对象分配过程：TLAB==

![image-20211125154103288](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125154103288.png)



#### 小结  堆空间的参数设置

==常用的参数==

![image-20211125155055797](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125155055797.png)

**打印出来所有的参数的默认值   如果是最终值    =前面有：的代表是被修改过的**

**当设置eden的占比时  如果过大 会导致minor gc没用了，过小的话 会频繁调用minor gc导致性能下降**

==解释说明 什么是 设置空间分配担保   -XX:HandlePromotionFailure==

![image-20211125160614800](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125160614800.png)





#### 堆是分配对象的唯一选择吗

==是，虽然有栈上分配  但是还没应用==

![image-20211125161157280](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125161157280.png)



##### **逃逸分析概述**

![image-20211125161742578](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125161742578.png)



**如何快速的判断是否发生了逃逸分析，就看new的对象是否有可能在方法外被调用。**



例子1👇

![image-20211125161913487](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125161913487.png)

例子2👇



![image-20211125162928104](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125162928104.png)

**只要没有发生逃逸 就考虑在栈上分配**





##### 逃逸分析参数设置 

**JDK 6u23 大版本能说JDK7之后 就默认开启逃逸分析了**

![image-20211125163107405](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125163107405.png)



##### 结论（优化开发性能）

局部变量随着方法就会被回收，方法外的则不能

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125163323349.png" alt="image-20211125163323349" style="zoom:50%;" />





##### 逃逸分析：代码优化

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125163709000.png" alt="image-20211125163709000" style="zoom:80%;" />





###### 代码优化-栈上分配（但是目前虚拟机并没有应用栈上分配）：

![image-20211125163906503](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125163906503.png)





例子👇

![image-20211125165600729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125165600729.png)

**关闭逃逸分析**

![image-20211125165659672](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125165659672.png)

结果 121ms



**开启逃逸分析**

![image-20211125165735931](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125165735931.png)

结果4ms





###### 代码优化-同步省略（消除）：

![image-20211125181122792](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125181122792.png)



例子👇

![image-20211125181243356](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125181243356.png)

tips：在编译时仍能看见锁的身影，只有在运行时才能去掉



###### 逃逸分析-分离对象或标量替换：



![image-20211125181953732](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125181953732.png)

**替换后结果如下：**

![image-20211125190954694](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125190954694.png)



==标量替换参数设置==

//进行过测试  关闭后不能进行标量替换   性能下降

![image-20211125182145416](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125182145416.png)



#### 本章小结

![image-20211125183015575](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211125183015575.png)





### 方法区

#### 栈、堆、方法区的交互关系



![image-20211126133746060](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126133746060.png)



#### 方法区的理解

==方法区看作是一块独立于Java堆的内存空间（方法区别名非堆）==

![image-20211126134822591](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126134822591.png)





![image-20211126135328257](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126135328257.png)



==本质上，方法区和永久代并不等价。仅是对hotspot而言的。==

==Hotspot中方法区的演进   到了JDK8 终于完全废弃了永久代概念，改用了在本地内存中实现的元空间来代替==

元空间和永久代区别，元空间不在虚拟机设置的内存中，而是使用本地内存



#### 设置方法区大小与OOM



##### 设置方法区大小



###### **JDK7**

![image-20211126140447652](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126140447652.png)

###### **JDK8**

![image-20211126141346959](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126141346959.png)



##### OOM举例





**不设置空间的话  不会报异常 因为最大空间是本地内存空间 ，  设置了后 报溢出异常**

![image-20211126142146281](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126142146281.png)



##### 如何解决OOM（之后会细讲）

![image-20211126142649404](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126142649404.png)





#### 方法区的内部结构



**方法区存储什么**

下图的是比较经典的分法，但是现在里面有些结构是有变化的

![image-20211126143232367](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126143232367.png)



==类型信息==

![image-20211126143458679](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126143458679.png)

==域信息==

![image-20211126143614553](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126143614553.png)

==方法信息==

![image-20211126143711636](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126143711636.png)





**代码举例👇**

![image-20211126150510813](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126150510813.png)



类似👇

![image-20211126150609072](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126150609072.png)



**一个知识点：**

![image-20211126150942729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126150942729.png)







**补充说明**

![image-20211126151140124](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126151140124.png)

![image-20211126151031892](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126151031892.png)



##### 运行时常量池

（要知道运行时常量池  必须要知道常量池）

**常量池**

![image-20211126151629642](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126151629642.png)



**为什么需要常量池**

![image-20211126151823387](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126151823387.png)

//和之前的动态链接很像    就是好几个地方要用  你把它放到常量池中，等要用的时候  通过符号加载常量池中的结构





**常量池中有什么**

![image-20211126152827959](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126152827959.png)



**小结：**

**==常量池，可以看做是一张表，虚拟机指令根据这张常量表找到要执行的类名、方法名、参数类型、字面量等类型。==**



**到底什么是运行时常量池**

![image-20211126153715157](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126153715157.png)











#### 方法区使用举例

![image-20211126153932748](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126153932748.png)

因为没有创建对象  所以下面例子 就没有涉及到堆空间的显示了



**指令执行**

![image-20211126154307632](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126154307632.png)

![image-20211126155102514](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126155102514.png)

![image-20211126155111247](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126155111247.png)



......中间有些步骤省略



![image-20211126155351701](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126155351701.png)

![image-20211126155551715](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126155551715.png)





#### 方法区的演进细节

很多虚拟机中是不存在永久代的概念的

**Hotspot中方法区的变化**

![image-20211126160437475](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126160437475.png)

==jdk1.8之前都还是用的虚拟内存==



==**永久代为什么要被元空间替换？**==

**1）为永久代设置空间大小是很难确定的。**

​	 在某些场景下，如果动态加载类过多，容易产生Perm区的OOM。

​	 而元空间和永久代之间最大的区别在于：元空间并不在虚拟机中，而是使用本地内存。因此，在默认情况下，元空间的大小仅受本地内存限制。

**2）对永久代进行调优是很困难的。**

​	 full GC很浪费时间



==**为什么要把字符串常量池（StringTable）进行变换   从永久代移到堆上面？**==

**StringTable(之后会详细讲)**

![image-20211126162901580](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126162901580.png)



==**证明静态变量存在哪 **==

通过下面的例子1得出结论，静态引用对应的对象实体始终都存在堆空间

通过下面的例子2得出结论，是引用名的存放有变化



例子1👇

创建一个100M的数组 



6、7设置的参数

![image-20211126163411279](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126163411279.png)

8设置的参数

![image-20211126163556981](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126163556981.png)



看各个版本的存放情况

**jdk6的情况**

![image-20211126163518063](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126163518063.png)



**jdk7的情况**

![image-20211126163304299](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126163304299.png)



**jdk8的情况**

![image-20211126163642532](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126163642532.png)



例子2👇

![image-20211126164042002](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126164042002.png)

![image-20211126164033820](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126164033820.png)



进行测试



![image-20211126165842759](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126165842759.png)

三个对象的数据都落在伊甸园区，结论只要是对象实例必然会在Java堆中分配



![image-20211126164602825](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126164602825.png)

这个静态变量本身是存在对象里的，对象存在堆中，证明了静态变量存在堆中

==静态变量在 JDK7 转移到 Class 对象中存储，Class 对象存储在堆中==



#### 方法区的垃圾回收

==可以回收，也可以不回收==

（费力不讨好   收集很必要 但有时候又会收集不好） 

==方法区的垃圾收集主要是回收两部分内容：常量池中废弃的常量和不再使用的类型。==

- **常量池中废弃的常量（了解）**

  ![image-20211126181622157](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126181622157.png)





- **不再使用的类型（了解）**

![image-20211126181800492](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126181800492.png)



#### 总结



![image-20211126182454176](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126182454176.png)



##### 常见面试题

![image-20211126182643736](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126182643736.png)



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211126182706441.png" alt="image-20211126182706441"  />



### 对象的实例化内存布局与访问定位

==学完这章可以回答的问题==

![image-20211129131738050](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129131738050.png)



#### 对象的实例化



##### 创建对象的方式

![image-20211129132258977](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129132258977.png)



##### 创建对象的步骤



![image-20211129133129427](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129133129427.png)



按框的顺序贴图

1、![image-20211129134249436](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129134249436.png)

2、

![image-20211129134444180](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129134444180.png)

3、

![image-20211129134824861](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129134824861.png)

4、

![image-20211129134925419](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129134925419.png)

5、

![image-20211129135030714](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129135030714.png)

6、

![image-20211129135322250](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129135322250.png)

7、

![image-20211129135415027](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129135415027.png)



**测试对象实例化的过程**



![image-20211129135808185](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129135808185.png)





#### 对象的内存布局

![image-20211129140348989](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129140348989.png)



**图示**

![image-20211129140654264](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129140654264.png)



#### 对象的访问定位



![image-20211129141715740](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129141715740.png)



**句柄访问**



![image-20211206164256813](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211206164256813.png)



**直接指针（Hotspot采用）**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129141902301.png" alt="image-20211129141902301" style="zoom: 55%;" />



### 直接内存(了解)



![image-20211129142613814](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129142613814.png)



![image-20211129143122559](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129143122559.png)



## ==执行引擎==



![image-20211129152435070](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129152435070.png)



### 执行引擎概述

![image-20211129144547105](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129144547105.png)



![image-20211129144605896](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129144605896.png)



**执行引擎其主要任务就是将高级语言解释/编译为机器语言  让对应平台能识别（JVM中的执行引擎充当了将高级语言翻译为机器语言的译者）** 

![image-20211129144925000](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129144925000.png)



#### 执行引擎的工作过程

![image-20211129145739226](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129145739226.png)



![image-20211129150113493](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129150113493.png)

  

### Java代码编译和执行过程



![image-20211129150528743](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129150528743.png)

**可以选择解释器（绿色）/编译器（蓝色）**



==**问题**==

**什么是解释器，什么是JIT编译器？**

![image-20211129151418717](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129151418717.png)



**为什么说Java是半编译半解释型语言？**

![image-20211129151453818](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129151453818.png)





### 机器码、指令、汇编语言（了解）



![image-20211129153725590](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129153725590.png)



#### 机器码

![image-20211129152615013](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129152615013.png)



#### 指令

![image-20211129152852325](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129152852325.png)



#### 指令集

![image-20211129152939327](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129152939327.png)



#### 汇编语言

![image-20211129153004478](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129153004478.png)



#### 高级语言

![image-20211129153318923](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129153318923.png)

#### 字节码

![image-20211129153557644](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129153557644.png)



### 解释器

![image-20211129154053225](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129154053225.png)

Java源文件直接通过jvm生成机器指令也具有跨平台性，但是为了让性能最好需要在先编译成字节码文件，然后再去执行。



**解释器工作机制（或工作任务）**

![image-20211129154645295](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129154645295.png)



**在Java发展历史里，一共有两套解释执行器，即古老的字节码解释器、现在普遍使用的模板解释器**

**基于解释器执行已经沦落为低效的代名词**



### JIT编译器



#### Java代码的执行分类

![image-20211129161148947](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129161148947.png)





#### **Hotspot中进行执行的架构**

![image-20211129161221996](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129161221996.png)



**Hotspot JVM的执行（也解释了为什么不剔除解释器）**

![image-20211129161520739](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129161520739.png)

==因为程序启动后，解释器可以马上发挥作用，省去编译的时间，立即执行。编译器要想发挥作用，把代码编译成本地代码，需要一定的执行时间。但编译为本地代码后，执行效率高==



#### JIT概念解释



![image-20211129162640125](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129162640125.png)



#### 热点代码及探测方式(要不要用即时编译器)



![image-20211129163023883](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129163023883.png)



**什么算热点代码呢  怎么样算探测方式呢**

![image-20211129163320098](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129163320098.png)



**方法调用计数器**

![image-20211129163645729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129163645729.png)



 ![image-20211129163944487](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129163944487.png)





**热度衰减（如果不做设置，方法调用计数器统计的并不是方法被调用的绝对次数，而是一个相对的执行频率）**



![image-20211129164225145](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129164225145.png)



**回边计数器**



![image-20211129164628620](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129164628620.png)



![image-20211129164647996](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129164647996.png)





#### HotSpot VM设置程序执行方式（了解）



![image-20211129164856532](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129164856532.png)



#### HotSpot VM中JIT分类

![image-20211129165431091](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129165431091.png)

**当64位操作系统HotSopt中的JIT默认是-server**



**-client和-server有各自的优缺点   优化策略如下**

![image-20211129165910084](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129165910084.png)





**我们其实可以不只用c2的   如下策略可以使我们既用c1又用c2**

![image-20211129170135225](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129170135225.png)



**总结**

![image-20211129175628333](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129175628333.png)

#### 写在最后（了解）

1、Graal编译器

![image-20211129175943410](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129175943410.png)

2、AOT编译器

![image-20211129180122862](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129180122862.png)

![image-20211129180337505](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211129180337505.png)





## ==String Table==

**(通过JVM角度对String进行剖析)**



### String的基本特性



#### 特性1

![image-20211130132821569](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130132821569.png)



==**new的都是放在堆空间  通过字面量定义的 在常量池中**==



**tips：实现序列化的目的**

**（序列化，就是把对象转化为字节流，才能进行网络传输。**
**把该字节序列保存起来(例如:保存在一个文件里),以后可以随时将该字节序列恢复为原来的对象。甚至可以将该字节序列放到其他计算机上或者通过网络传输到其他计算机上恢复，只要该计算机平台存在相应的类就可以正常恢复为原来的对象。）**



**jdk1.9之后就改用byte[]数组进行存储了    同时StringBuffer和StringBuilder内部的存储也发生了改变**

![image-20211130133707210](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130133707210.png)



#### 特性2

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130133910492.png" alt="image-20211130133910492" style="zoom:80%;" />





**例子(不可变性)**👇：

![image-20211130134315734](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130134315734.png)



![image-20211130134359074](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130134359074.png)



![image-20211130134553620](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130134553620.png)





<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130135056230.png" alt="image-20211130135056230" style="zoom: 67%;" />

对上面str的理解  可以看自己写的面试题 方法的参数传递机制    String 包装类对象的不可变性



#### 特性3



![image-20211130140100965](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130140100965.png)





### String的内存分配



![image-20211130140755336](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130140755336.png)

**new的都是放在堆空间  通过字面量定义的 在常量池中**



**字符串常量池存储的位置**

![image-20211130140915375](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130140915375.png)



==**为什么StringTable要进行调整?**==

**①permSize默认比较小 ②永久代垃圾回收频率低**



### String的基本操作

例子👇

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130142947707.png" alt="image-20211130142947707" style="zoom:80%;" />



### 字符串的拼接操作

![image-20211130151648179](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130151648179.png)



**例子**👇：

例1：对应第一条   常量与常量的拼接结果在常量池，原理是编译期优化

![image-20211130143750293](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130143750293.png)





例2：对应上面多条  进行回顾

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130144907801.png" alt="image-20211130144907801" style="zoom:80%;" />



例3：对上面的第三条 进行字节码分析



![image-20211130150025158](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130150025158.png)

了解：在jdk5.0之后使用的是StringBuilder，在jdk5.0之前使用的是StringBuffer



例4：

**1.字符串拼接操作不一定使用的是StringBuilder！**

​           **如果拼接符号左右两边都是字符串常量或者常量引用，则仍然使用编译期优化，即非StringBuilder的方式。**

**2.针对于final修饰类、方法、基本数据类型、引用数据类型的量的结构时，能使用上final的时候建议使用上。例如 下面这个s1加了final  其实就相当于一个常量**

![image-20211130150426380](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130150426380.png)

例5：对StringBuilder直接拼接字符串和String的字符串拼接方式进行比较

==main对两个方法 进行10w次的调用(下面的方法 效率明显高)==   

![image-20211130152639183](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130152639183.png)

![image-20211130151942107](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130151942107.png)

**对StringBuilder的改进空间：在实际开发中，如果基本确定要前前后后添加的字符串长度不高于某个限定值highLevel的情况下，建议使用构造器的方法去实例化   StringBuilder  s = new StringBuilder(highLevel);//new char[highLevel]   因为不去指定值的话    它会默认创建一个char数组  如果不够了 会重新创建  然后进行复制   这个的话既浪费了内存  又减慢了执行速度**



### intern()的使用



![image-20211130155720756](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130155720756.png)

intern()只是在不存在的时候放进去



#### **如何保证变量s指向的是字符串常量池中的数据呢？**

![image-20211130155909144](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130155909144.png)





#### **面试题**

**题目：new String("ab")会创建几个对象？**

看字节码，就知道是两个。

​	一个对象是：new关键字在堆空间创建的

​	另一个对象是：字符串常量池中的对象。字节码指令：ldc

**拓展：new String("a")+new String("b")呢？**

​	对象1：new StringBuilder()

​	对象2：new String("a")

​	对象3：常量池中的"a"

​	对象4：new String("b")

​	对象5：常量池中的"b"



​	深入剖析：StringBuilder的toString():

​		对象6：new String("ab")

​		   强调一下，toString()的调用，在字符串常量池中，没有生成"ab"

**总结：上面两个题目  一个在常量池中会创建ab     一个在常量池中不创建ab**





**面试题：intern()的使用：jdk6 vs jdk7/8**

![image-20211130162037379](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130162037379.png)

==**jdk6两个打印的都是false**==

==**jdk7/8打印的一个是false一个是true**==

**原因**👇



![image-20211130163215344](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130163215344.png)

**jdk7/8中如果串池中有，则不会放入。返回已有的串池中的对象的地址     如果没有，则会把对象的引用地址复制一份，放入串池，并返回串池中的引用地址  **



**上面题的拓展问题：将String s4  = "11" 往上提一下   答案是false**

![image-20211130163947733](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130163947733.png)



#### String的intern()的使用

![image-20211130164351576](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130164351576.png)



#### intern练习题



**题1**

![image-20211130164927125](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130164927125.png)



**题1变题  在前面先创建了一个ab**

![image-20211130165129353](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130165129353.png)



**题2**



![image-20211130165435970](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130165435970.png)



#### intern()的效率测试：空间角度



![image-20211130180807870](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130180807870.png)



//因为加了 intern 指向的是数组值指的是常量池中的值    创建的堆中的对象可以进行回收

![image-20211130181207011](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211130181207011.png)









### StringTable的垃圾回收



//PrintStringTableStatistics   打印字符串常量池中的打印信息

![image-20211201134145054](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201134145054.png)



### G1中的String去重操作(了解)



#### 背景说明

![image-20211201134840807](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201134840807.png)



#### 实现

![image-20211201135043876](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201135043876.png)





#### 命令行选项



![image-20211201135239522](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201135239522.png)



## ==垃圾回收==



==垃圾回收相关大厂面试题==

![image-20211201140549367](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201140549367.png)

![image-20211201140622174](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201140622174.png)



### 垃圾回收概述



#### 什么是垃圾

![image-20211201140811153](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201140811153.png)

**引用类型才考虑回收**![image-20211201141014585](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201141014585.png)

**一个进程对应一个运行时数据区    如果没有垃圾回收的话  垃圾对象会保留到进程结束  运行时数据区关闭才销毁**



#### 为什么需要GC

 ![image-20211201141530191](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201141530191.png)



#### 早期垃圾回收



 **早期垃圾回收**

![image-20211201142000601](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201142000601.png)

**内存泄漏：本身不用了 但没办法进行回收**



**有了垃圾回收**

![image-20211201142214776](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201142214776.png)



#### Java垃圾回收机制

==**好处**==

![image-20211201142747763](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201142747763.png)



==**担忧**==

![image-20211201142806285](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201142806285.png)



**应该关心哪些区域的回收**



![image-20211201143425379](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201143425379.png)![image-20211201143544254](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201143544254.png)





### 垃圾回收相关算法



==**标记阶段：对象存活判断**==

![image-20211201144943240](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201144943240.png)



#### 标记阶段：引用计数算法



![image-20211201145325049](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201145325049.png)

**因为它无法处理循环引用的问题  所有Java的垃圾回收器中没有使用这类算法**



**循环引用**👇

![image-20211201145838353](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201145838353.png)

****

- 当P指向空的时候  其他可能已经用不到了 但是它们的引用计数不为0 无法被回收（也就是内存泄漏  没有用了  但是无法被回收）



##### **Java没有使用计数垃圾回收算法证明  **

**-- 刚开始没有打开System.gc() eden区有占用    打开了之后发现占用大量减少，这正好反证了没有使用计数算法    因为被回收了  如果是按照计数回收的话  应该还存在**  

![image-20211201150739707](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201150739707.png)



**堆栈中结构**

![image-20211201150914158](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201150914158.png)



##### **小结**

![image-20211201151035087](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201151035087.png)





#### 标记阶段：可达性分析算法（或根搜索算法、追踪性垃圾收集）



![image-20211201151533083](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201151533083.png)

##### 实现思路

![image-20211201151641657](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201151641657.png)



**GC Roots  所直接或间接连接的路径称为引用链**

![image-20211201152027517](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201152027517.png)



##### ==在Java 语言中，GC Roots包括以下几类元素（面试常考）==

![image-20211201152156294](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201152156294.png)



👇**指的是如果你单独看某个区域的垃圾回收时  要考虑这个区域的对象是否被其他区域的对象所引用    （分代收集和局部回收） 就比如说只看年轻代时   老年代中的对象也可以是GC Roots集合内的** 

![image-20211201153037116](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201153037116.png)





**小技巧：存放在堆外，又保存了堆内存里面的对象  那它就是一个Root**

![image-20211201152901981](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201152901981.png)



**注意：**

![image-20211201153433385](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201153433385.png)





#### 对象的finalization机制



![image-20211201153808208](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201153808208.png)

![image-20211201154601715](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201154601715.png)



##### 虚拟机中的对象一般处于三种可能的状态

![image-20211201154957579](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201154957579.png)

**复活了之后  又要被杀  那就救不了了  因为finalize()只会被调用一次**



##### 具体过程

![image-20211201155411918](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201155411918.png)



##### 代码演示：可复活的对象

![image-20211201160334319](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201160334319.png)



**注释掉了重写的finalize的方法  看执行的区别**

![image-20211201160549127](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201160549127.png)

![image-20211201160611298](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201160611298.png)





#### MAT与JProfiler的GC Roots溯源

**分析程序**

![image-20211201164146687](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201164146687.png)

![image-20211201164159731](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201164159731.png)



##### MAT查看变换

**MAT的介绍**

![image-20211201161129371](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201161129371.png)



![image-20211201162328231](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201162328231.png)

**获取dump文件**

程序和MAT之间交互的媒介dump

![image-20211201162428842](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201162428842.png)

![image-20211201162609511](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201162609511.png)



![image-20211201163307950](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201163307950.png)

保存的这个快照是临时的   关闭了java visualVM 就会消失  如果还要 就需要保存起来

![image-20211201163319602](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201163319602.png)



**通过MAT对dump进行分析**

![image-20211201163656360](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201163656360.png)

![image-20211201163929269](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201163929269.png)



**👇两次dump文件的区别    第二次不在局部变量表中了  不属于gc roots**

![image-20211201164231553](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201164231553.png)

![image-20211201164239720](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201164239720.png)





##### JProfile GC Roots 溯源

**通过溯源对内存泄漏的问题  进行监控**

![image-20211201181359280](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201181359280.png)



![image-20211201181413552](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201181413552.png)



![image-20211201181423838](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201181423838.png)

![image-20211201181750752](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201181750752.png)

![image-20211201181928877](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201181928877.png)

![image-20211201182116641](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211201182116641.png)





------





==**垃圾清除阶段**==

![image-20211202134232961](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202134232961.png)



#### 清除阶段：标记-清除算法（Mark - Sweep）



![image-20211202135744769](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202135744769.png)

**注意：标记的是可达对象**



![image-20211202135911570](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202135911570.png)





![image-20211202140050348](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202140050348.png)

**意思就是  下次有对象  如果垃圾的位置空间够  就直接覆盖     计算机格式化 就是这个原理  当你格式化了 可以恢复 但恢复前千万不要往盘里放东西**



#### 清除阶段：复制算法



![image-20211202140832052](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202140832052.png)



![image-20211202141003775](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202141003775.png)



==**年轻代中的回收  伊甸园区、幸存者区就用的复制算法**==



![image-20211202142258565](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202142258565.png)



![image-20211202142436055](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202142436055.png)

**老年代不适合复制算法 因为大部分对象都还在存活**





#### 清除阶段：标志-压缩算法（或标记-整理、Mark-Compact）算法



![image-20211202142642002](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202142642002.png)

**标记-清除算法可以在老年代使用但是还要考虑清除碎片问题**



![image-20211202143455886](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202143455886.png)



![image-20211202143913650](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202143913650.png)

==**为对象分配内存**==

**复制算法、标记-压缩 :指针碰撞**

**标记-清除：空闲列表分配**



![image-20211202143926637](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202143926637.png)



#### 小结

##### 对比三种算法

![image-20211202144353293](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202144353293.png)





#### 分代收集算法

==不同生命周期的对象可以采取不同的收集方式，以便提高回收效率==



![image-20211202145913932](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202145913932.png)



**例如老年代（像cms  先是mark-sweep  如果回收不佳  启用备用回收器 备用回收器的算法是mark-compact）**

![image-20211202150303831](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202150303831.png)



#### 增量收集算法、分区算法



##### 增量收集算法



![image-20211202150935018](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202150935018.png)



![image-20211202151224168](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202151224168.png)



##### 分区算法（前面的都是分代）



![image-20211202152111561](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202152111561.png)





![image-20211202152138343](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202152138343.png)





### 垃圾回收相关概念

####  System.gc()的理解

![image-20211202153556865](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202153556865.png)

**System.gc()提醒jvm的垃圾回收器执行gc，但是不确定是否马上执行**



例子👇：

![image-20211202153837482](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202153837482.png)

![image-20211202153855038](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202153855038.png)

![image-20211202153909074](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202153909074.png)

**方法一**（没有回收   将其从新生代放到了老年代）

![image-20211202154055642](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202154055642.png)

**方法二**（在youngGC中 就已经进行回收了）

![image-20211202154152018](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202154152018.png)

**方法三**（这个要和方法4对照着看   虽然在局部变量表中没有显示它   但是局部变量表的大小是2   this是0   代表它占用了1  所以没被回收）

![image-20211202154309506](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202154309506.png)

**方法四**（此时buffer超出作用域了   定义的value就会占据它的槽slot    就代表buffer占用的这个槽就没有指向的对象的引用了）

![image-20211202154911107](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202154911107.png)

**方法五**（在方法一的时候没有回收   到了方法五中 进行回收    方法一形成的栈帧结束  局部变量表销毁  没有变量指向它了）

![image-20211202155049814](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202155049814.png)



#### 内存溢出与内存泄漏

##### 内存溢出

没有空闲内存，并且垃圾收集器也无法提供更多内存  

![image-20211202161244789](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202161244789.png)



**（注意报oom之前肯定会进行一次full gc）**

![image-20211202161101645](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202161101645.png)



- **没有空闲内存**

  ![image-20211202160357729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202160357729.png)



##### 内存泄漏（Memory Leak）



![image-20211202161304498](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202161304498.png)

**内存泄漏是有可能导致内存溢出的   但这不是一定的**

**宽泛上讲的内存泄漏（例子）： 就比如你要定义一个局部变量  它在方法执行结束后就可以被回收  但是定义成了静态变量，本来生命周期不是很长但是被定义的很长**



**==图解==**

![image-20211202162318769](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202162318769.png)

==**举例（面试官问严格意义上的内存泄漏）**==

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202162515657.png" alt="image-20211202162515657" style="zoom:80%;" />



#### Stop The World



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202163021592.png" alt="image-20211202163021592" style="zoom:80%;" />



- **==STW时间和采用哪款GC无关，所有的GC都有这个时间，好的垃圾回收器也只能说垃圾回收器越来越优秀，回收效率越来越高，尽可能地缩短了暂停时间。==**
- **==STW是JVM在后台自动发起和自动完成的。在用户不可见的情况下，把用户正常的工作线程全部停掉。==**
- **==开发中不要用System.gc()；会导致Stop-the-world的发生==**



#### 垃圾回收的并行与并发



**程序中的并行与并发**

![image-20211202164259354](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202164259354.png)

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202164408728.png" alt="image-20211202164408728" style="zoom:80%;" />



**垃圾回收的并发与并行**

![image-20211202164544524](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202164544524.png)



![image-20211202164803209](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202164803209.png)



#### 安全点与安全区域（了解）



##### 安全点

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202164951240.png" alt="image-20211202164951240" style="zoom:67%;" />

==如何在GC发生时，检查所有线程都跑到最近的安全点停顿下来呢？（面试可能问）==

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202165412418.png" alt="image-20211202165412418" style="zoom:67%;" />



##### 安全区域

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202165520963.png" alt="image-20211202165520963" style="zoom:67%;" />



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211202165658405.png" alt="image-20211202165658405" style="zoom:67%;" />





#### 引用

==**我们希望能描述这样一类对象：当内存空间还足够时，则能保留在内存中；如果内存空间在进行垃圾收集后还是很紧张，则可以抛弃这些对象**==

**==既偏门又非常高频的面试：强引用、软引用、弱引用、虚引用有什么区别？具体使用场景是什么？（学完要会回答）==**



![image-20211203141807496](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203141807496.png)



![image-20211203142011820](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203142011820.png)





<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203142809753.png" alt="image-20211203142809753" style="zoom:80%;" />



##### 强引用--不回收



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203143333745.png" alt="image-20211203143333745" style="zoom:80%;" />



**例子：下面两个都是强引用**

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203143420752.png" alt="image-20211203143420752" style="zoom:80%;" />



**强引用特点**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203143613100.png" alt="image-20211203143613100" style="zoom:80%;" />



##### 软引用--内存不足即回收

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203143832145.png" alt="image-20211203143832145" style="zoom:80%;" />

**==当内存足够    不会回收软引用的可达对象           当内存不够时    会回收软引用的可达对象   回收了不一定会报OOM==**

**先是对不可触及的对象进行回收  如果回收后发现内存依旧不够开始对软引用对象进行回收**

**软引用是不会导致出现OOM的 因为软引用到后面都是被回收完了**



**例子：生成软引用**

1、

![image-20211203150307579](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203150307579.png)

2、

![image-20211203150410876](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203150410876.png)





##### 弱引用--发现即回收



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203151131138.png" alt="image-20211203151131138" style="zoom:80%;" />



![image-20211203151548697](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203151548697.png)



**面试题：你开发中使用过WeakHahsMap吗？**

在内存不足时可以及时回收数据



##### 虚引用--对象回收跟踪



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203152619450.png" alt="image-20211203152619450" style="zoom:80%;" />



![image-20211203152740500](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203152740500.png)

**//一旦将obj对象回收，就会将此虚引用存放到引用队列中。可以看下代码**



##### 终结器引用（了解）



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203154533820.png" alt="image-20211203154533820" style="zoom:80%;" />





### 垃圾回收器

#### GC分类与性能指标



##### 分类

**==按线程数分，可以分为串行垃圾回收器和并行垃圾回收器==**

![image-20211203160417848](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203160417848.png)

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203160118464.png" alt="image-20211203160118464" style="zoom:80%;" />



**==按照工作模式分，可以分为并发式垃圾回收器和独占式垃圾回收器==**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203160540049.png" alt="image-20211203160540049" style="zoom:80%;" />



**==按碎片处理方式分，可分为压缩式垃圾回收器和非压缩式垃圾回收器==**



![image-20211203160858525](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203160858525.png)



**==按工作的内存区间分，又可分为年轻代垃圾回收器和老年代垃圾回收器==**



##### 评估GC的性能指标

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203161031663.png" alt="image-20211203161031663" style="zoom:80%;" />



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203161500194.png" alt="image-20211203161500194" style="zoom:80%;" />



==分别注重吞吐量和注重低延迟的表现==



![image-20211203162130935](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203162130935.png)







==吞吐量==

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203162033921.png" alt="image-20211203162033921" style="zoom:80%;" />



==吞吐量vs暂停时间==

![image-20211203163615860](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203163615860.png)

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203163848502.png" alt="image-20211203163848502" style="zoom:80%;" />





#### 不同的垃圾回收器概述



**==问题：Java常见的垃圾收集器有哪些？要知道==**

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211203170036802.png" alt="image-20211203170036802" style="zoom:67%;" />





==**七款经典收集器与垃圾分代之间的关系**==



![image-20211204132714001](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204132714001.png)



==**垃圾回收器的组合关系**==



![image-20211204132832733](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204132832733.png)



**JDK 8时废弃了红虚线的组合，JDK9彻底移除**

**JDK 14废弃了绿色虚线**

**青色虚线代表在JDK14将这款垃圾回收器remove**



==**为什么要有很多收集器？**==

**因为Java的使用场景很多，移动端，服务器等。所以就需要针对不同的场景，提供不同的垃圾收集器，提高垃圾收集的性能。我们选择的只是对具体应用最合适的收集器。**





**==如何查看默认的垃圾收集器==**

![image-20211204134457794](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204134457794.png)





例子1👇

![image-20211204134659631](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204134659631.png)

![image-20211204134729694](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204134729694.png)







例子2👇

![image-20211204134646494](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204134646494.png)



#### Serial回收器：串行回收



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204135555932.png" alt="image-20211204135555932"  />



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204140033048.png" alt="image-20211204140033048"  />



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204140329649.png" alt="image-20211204140329649"  />

//设置hotspot参数之后     然后在上面的指令可以查看  使用的收集器



![image-20211204140805392](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204140805392.png)

 

#### ParNew回收器：并行回收



![image-20211204140923273](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204140923273.png)



**下面是它和SerialOld收集器的结合使用    它还能和CMS结合   但是jdk14之后就不行了**

![image-20211204141231826](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204141231826.png)



![image-20211204141338813](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204141338813.png)



**开启设置**

![image-20211204141520632](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204141520632.png)





#### Parallel回收器：吞吐量优先



 ![image-20211204142204640](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204142204640.png)





![image-20211204142515928](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204142515928.png)

**高吞吐量适合在后台运算而不需要太多交互的任务       同时在jdk1.6提供了Parallel Old收集器     基于并行回收的和stw机制**  



![image-20211204143028770](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204143028770.png)



==**在程序吞吐量优先的应用场景中，Parallel 收集器和Parallel Old 收集器的组合，在Server模式下的内存回收性能很不错。**==

==**在Java8中，默认是此垃圾收集器**==





**参数配置(在Java8中默认是此垃圾收集器       其他版本  二者相互激活  开启一个即可)**

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204143421221.png" alt="image-20211204143421221" style="zoom:80%;" />

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204144109191.png" alt="image-20211204144109191" style="zoom:80%;" />

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204144454444.png" alt="image-20211204144454444" style="zoom:80%;" />





#### CMS回收器：低延迟



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204144939670.png" alt="image-20211204144939670" style="zoom:80%;" />



![image-20211204150813707](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204150813707.png)



![image-20211204150937377](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204150937377.png)



**运行流程**



![image-20211204151022536](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204151022536.png)

![image-20211204152129750](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204152129750.png)

 



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204152434853.png" alt="image-20211204152434853" style="zoom:100%;" />

**因为CMS收集器的垃圾收集算法采用的是标记-清除算法       意味着每次执行完内存回收后，由于被执行内存的无用对象的内存空间可能是不连续的一些内存块，所以不可避免的会产生一些内存碎片，那么CMS在为新对象分配内存空间时，只能使用空闲列表执行内存分配**



![image-20211204153305827](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204153305827.png)



**CMS的优缺点**

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204153355017.png" alt="image-20211204153355017" style="zoom:80%;" />



**重新标注是为了确定之前怀疑是垃圾的到底是不是垃圾      但是还有部分对象本身就不是垃圾 在并发标记执行过程中变成垃圾  无法对这些垃圾进行及时回收    这些垃圾称为浮动垃圾** 



**CMS收集器可以设置的参数**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204154257373.png" alt="image-20211204154257373" style="zoom:80%;" />

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204154558718.png" alt="image-20211204154558718" style="zoom:80%;" />





<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204155839354.png" alt="image-20211204155839354" style="zoom:80%;" />







**JDK后续版本中CMS的变化**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204160458557.png" alt="image-20211204160458557" style="zoom:80%;" />







#### G1回收器：区域化分代式



**==问题==**

==既然我们已经有了前面几个强大的GC，为什么还要发布Garbage First(G1)GC?==



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204161142839.png" alt="image-20211204161142839" style="zoom:80%;" />

 **全功能收集器  即支持老年代也支持年轻代**



==为什么名字叫做Garbage First(G1)呢？==



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204161836512.png" alt="image-20211204161836512" style="zoom:80%;" />

**因为这个收集器的侧重点在于回收垃圾最大量的区间（Region），所以我们给G1一个名字：垃圾优先**





<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204162749120.png" alt="image-20211204162749120" style="zoom:80%;" />



==**G1回收器的特点（优势）**==



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204163211592.png" alt="image-20211204163211592" style="zoom:80%;" />

![image-20211204164352999](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204164352999.png)

![image-20211204164910003](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204164910003.png)

**软实时代表的是尽可能在你给定的时间内完成**



==**缺点**==

![image-20211204165638454](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211204165638454.png)





**==G1回收器的参数设置==**



![image-20211205135902251](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205135902251.png)



**==G1回收器的常见操作步骤==**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205140239809.png" alt="image-20211205140239809" style="zoom:80%;" />



**==G1回收器的适用场景==**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205140445079.png" alt="image-20211205140445079" style="zoom:80%;" />



==**分区Region：化整为零**==



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205141419888.png" alt="image-20211205141419888" style="zoom:80%;" />



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205141643564.png" alt="image-20211205141643564" style="zoom:80%;" />



region内部的储存方式  指针碰撞

多个线程用同个region时可以单独给每个线程分配TLAB



==**设置Humongous的原因**==

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205141825275.png" alt="image-20211205141825275" style="zoom:80%;" />

如果分配到老年代 这就是宽泛意义上的内存泄漏，明明不想让它存活那么久的



==**G1回收器垃圾回收过程**==



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205142446119.png" alt="image-20211205142446119" style="zoom:80%;" />

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205142953576.png" alt="image-20211205142953576" style="zoom:67%;" />



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205143220911.png" alt="image-20211205143220911" style="zoom: 80%;" />



==**G1回收器垃圾回收过程：Remembered Set**==



![image-20211205144159294](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205144159294.png)



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205144557654.png" alt="image-20211205144557654" style="zoom:67%;" />



##### G1回收过程（了解）

**过程一：年轻代GC**



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205151214047.png" alt="image-20211205151214047" style="zoom:80%;" />

tips:只有伊甸园区在内存不够的情况下 才会触发young GC 幸存者区不能触发



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205151721538.png" alt="image-20211205151721538" style="zoom:80%;" />



**过程**



![image-20211205152250063](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205152250063.png)



**过程二：并发标记过程**



![image-20211205152628942](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205152628942.png)



**过程三：混合回收**



![image-20211205153028858](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205153028858.png)



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205153723724.png" alt="image-20211205153723724" style="zoom:80%;" />



**可选过程四：Full GC**



![image-20211205154059545](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205154059545.png)



##### G1回收器优化建议



![image-20211205154727458](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205154727458.png)



#### 垃圾回收器总结



![image-20211205154858673](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205154858673.png)



**怎么选择垃圾回收器**

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205155716637.png" alt="image-20211205155716637" style="zoom: 80%;" />



**==最后需要明确一个观点：==**

1.没有最好的收集器，更没有万能的收集；

2.调优永远是针对特定场景、特定需求，不存在一劳永逸的收集器



==**面试**==



![image-20211205160118990](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205160118990.png)



#### GC日志分析



<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205160418249.png" alt="image-20211205160418249" style="zoom:80%;" />



**举例**



![image-20211205160711048](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205160711048.png)





![image-20211205161041092](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205161041092.png)





![image-20211205161224240](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205161224240.png)



**日志补充说明：**



![image-20211205161518731](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205161518731.png)

![image-20211205161830810](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205161830810.png)







**Minor GC**

![image-20211205162154245](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205162154245.png)



**Full GC**

![image-20211205162132810](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205162132810.png)



**看看宋红康JVMP198  举例子**

JDK7和JDK8中的不同  如果要存入的大于年轻代内存空间 7会把年轻代中的回收 放到老年代  这个放到年轻代，但是8会把这个直接塞进老年代



**把日志输出  然后在相关的软件中进行分析（之后调优会进行细讲的）**

![image-20211205163528478](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205163528478.png)

![image-20211205163748214](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205163748214.png)



演示了GCViewer(在github上下载)、GCEasy



GCViewer界面

![image-20211205164204123](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205164204123.png)



GCEasy界面

![image-20211205164235515](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205164235515.png)





#### 垃圾回收器的新发展



![image-20211205164759179](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205164759179.png)



==**Shenandoah GC**==

![image-20211205165007278](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205165007278.png)



![image-20211205165352775](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205165352775.png)



==**ZGC**==



![image-20211205165546024](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205165546024.png)



![image-20211205165830780](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205165830780.png)

**在windows上使用ZGC    (JDK14新特性)** 



![image-20211205165926074](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211205165926074.png)



**其他回收器**

AliGC、Zing











------



# 字节码与类的加载篇



## ==Class文件结构==

### 概述

 

#### 字节码文件的跨平台性



![image-20211207202953318](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207202953318.png)

**所有的JVM全部遵守Java虚拟机规范，也就是说所有的JVM环境都是一样的，这样一来字节码文件可以在各种JVM上运行**



#### Java的前端编译器



**==前端编译器的主要任务就是将符合Java语法规范的Java代码转换为符合JVM规范的字节码文件==**

**在java语言中JDK默认提供的编译器是javac。javac是一种能将Java源码编译为字节码的前端编译器。**

![image-20211207204308729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207204308729.png)



#### 透过字节码指令看代码细节



![image-20211207204859528](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207204859528.png)

**有些操作  你单独看代码是看不出来的  需要通过字节码**



**==例子1==**

![image-20211207205247039](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207205247039.png)

**上面本应该是false  因为是引用数据类型和基本数据类型  是无法比较的  但是有拆箱装箱机制  所以 可以比较   为true**

**下面为什么是true和false   点到字节码里面可以进行查看  因为Integer的cache里面存的是-128-127   没有128所以要新创建对象**



![image-20211207205550703](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207205550703.png)





==**例子2**==



![image-20211207210202207](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207210202207.png)

**也是false   因为上面的str是通过StringBuilder的toString的  所以两个的地址是不一致的**





**==例子3==**



![image-20211207210841550](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207210841550.png)



![image-20211207211032715](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207211032715.png)

**成员变量（非静态）的赋值过程：① 默认初始化 - ② 显式初始化/代码块中初始化 - ③ 构造器中初始化 - ④ 有了“对象.属性”或“对象.方法”的方法对成员变量进行赋值。**

**利用f去调用  因为属性不具有多态性   所以f.x = 20**







### 虚拟机的基石：Class文件



![image-20211207213251089](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207213251089.png)



![image-20211207213706075](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211207213706075.png)

**比如：操作码 （操作数）**



==**如何查看字节码文件**==

**方式一：一个一个二进制的看     视频中用的是Notepad++，需要安装一个HEX-Editor插件，或者使用Binary Viewer**

**方式二：使用javap指令：jdk自带的反解析工具  只能作用于被编译过的文件  进行反编译  javap -v StackStruTest.class    后面加> xx.txt   就是把反编译的结果输出到txt上   **

**方式三：使用IDEA插件：jclasslib或jclasslib bytecode viewer客户端工具**



### Class文件结构（要记一下 下面的位置顺序）



![image-20211208133109206](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208133109206.png)



![image-20211208133119058](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208133119058.png)

**本质是二进制流   如果存储下来  那就可以固定在磁盘  没有存储下来 还可以通过网络进行传输**



![image-20211208133827529](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208133827529.png)



![image-20211208133948799](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208133948799.png)





==换句话说，充分理解了每一个字节码文件的细节，自己也可以反编译出Java源文件来。==



![image-20211208134757323](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208134757323.png)

![image-20211208134957056](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208134957056.png)

![image-20211208135346237](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208135346237.png)

 



**举例**

![image-20211208134343007](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208134343007.png)





![image-20211208135454936](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208135454936.png)





![image-20211209130339841](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209130339841.png)



![image-20211209143741206](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209143741206.png)



![image-20211209151114544](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209151114544.png)



**挨个解读(还想看就去回顾宋红康老师的那几个视频)**





#### 魔数：Class文件的标志



![image-20211208141625059](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208141625059.png)

**类似于图片、MP3格式的文件打开也有魔数的概念     是用来检验是不是合格的该类型文件**



#### Class文件版本号





![image-20211208142157502](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208142157502.png)

![image-20211208142712633](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208142712633.png)

**minor_version小版本 副版本                   major_version 大版本 主版本**





#### 常量池：存放所有常量



![image-20211208143217111](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208143217111.png)

![image-20211208143723404](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208143723404.png)

**常量池常量数量    常量池表    常量池表中用于存放编译时期生成的各种字面量和符号引用**



==常量池计数器==

![image-20211208144051659](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208144051659.png)



==常量池==

![image-20211208144504002](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208144504002.png)



![image-20211208144530772](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208144530772.png)



**字面量和符号引用**

![image-20211208144937860](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208144937860.png)

![image-20211208145050797](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208145050797.png)

![image-20211208145105224](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208145105224.png)

![image-20211208145343928](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208145343928.png)

![image-20211208145436481](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208145436481.png)

![image-20211208145558341](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208145558341.png)



![image-20211208145832928](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208145832928.png)



**常量类型和结构**

![image-20211208151055743](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208151055743.png)

![image-20211208151116390](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208151116390.png)

**字符串1的长度是要加上它的长度u2  比如是03后面就要加上3个长度**

![image-20211208161526166](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208161526166.png)



**总结1**

![image-20211208161640386](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208161640386.png)



**总结2**

![image-20211208161804358](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208161804358.png)







**==底下的这些表示 还有集合 可以在jclasslib里看到  如下👇==**  

![image-20211208164628432](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208164628432.png)





#### 访问标识（access_flag、访问标志、访问标记）

![image-20211208162107561](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208162107561.png)

 ![image-20211208162519257](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208162519257.png)

![image-20211208162649733](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208162649733.png)





#### 类索引、父类索引、接口索引集合

![image-20211208162851888](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208162851888.png)

![image-20211208164206540](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208164206540.png)

![image-20211208164351826](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208164351826.png)

![image-20211208164342972](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211208164342972.png)



#### 字段表集合

![image-20211209130430525](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209130430525.png)

==在java语言中不能定义相同字段名的数据   但是字节码文件中可以==



**fields_count(字段计数器)**

![image-20211209131117137](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209131117137.png)



**fields [] (字段表)**

![image-20211209131450526](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209131450526.png)



==**字段表访问标识**==

![image-20211209131716574](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209131716574.png)



**==字段名索引==**

![image-20211209131957357](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209131957357.png)



**==描述符索引==**

![image-20211209132138922](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209132138922.png)

![image-20211209132116168](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209132116168.png)



**==字段的属性计数器==**

属性个数



**==属性表集合==**

对于常量才有

![image-20211209132637525](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209132637525.png)





#### 方法表集合

![image-20211209132854372](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209132854372.png)

==在java中重载的方法的方法签名需要不一致（就是输入参数）（如果是方法返回值不一样 也不行）  但字节码文件中允许 方法签名一致  只需要方法返回值不相同就行了==





**methods_count(方法计数器)**



![image-20211209134055718](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209134055718.png)



**methods [] (方法表)**

![image-20211209134310654](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209134310654.png)



**==方法表访问标志==**

![image-20211209134602080](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209134602080.png)



**==方法名索引==**

指向常量池中的方法名

**==描述符索引==**

指向常量池中输入参数和返回参数



#### 属性表集合

![image-20211209135556282](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209135556282.png)



**attributes_count(属性计数器)**

![image-20211209135946618](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209135946618.png)



**==属性的通用格式==**

![image-20211209140811423](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209140811423.png)



**==属性类型==**

![image-20211209140904791](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209140904791.png)

**很多信息   这个去官网上查看    docs.oracle.com/javase/specs/jvms/se8/html/jvms-4.html#jvms-4.7**

属性表内部还会有属性

 

**最后的一般都是附加属性**



#### 小结

![image-20211209151332605](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211209151332605.png)

**上面的大体知道顺序就行了**





###  使用javap指令解析Class文件



#### 解析字节码的作用

![image-20211210125059373](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210125059373.png)



#### javac-g操作

![image-20211210125432530](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210125432530.png)

（直接javac编译的不含局部变量表     javac-g包含局部变量表      或者用eclipse idea编译会自动生成局部变量表）





#### javap的用法

![image-20211210130622464](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210130622464.png)



**视频按照重组顺序讲解**



**代码为👇**

![image-20211210130929711](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210130929711.png)

![image-20211210130956628](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210130956628.png)





**讲解指令顺序**

![image-20211210130807963](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210130807963.png)

- 显示固定的类  在这个类之前的权限的类和成员也会显示  就比如说显示protected的 也就会显示public

- -package   显示非私有的信息 



![image-20211210131829460](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210131829460.png)

- -s (默认不带私有的信息  如果想带加一个-p)

  ![image-20211210131936866](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210131936866.png)

- -l (如果本身字节码中就不包含局部变量表  那么就不会生成)

![image-20211210132131535](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210132131535.png)

- -c (反编译    可以看到code   code就是具体的执行指令)

![image-20211210132413875](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210132413875.png)

- -v -verbose   (信息最全    常量池什么的都能看到  但是仍然不包括私有的信息)  



![image-20211210133900657](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210133900657.png)



**如果想要信息最全的话    可以使用javap -v -p    字节码文件**



#### 使用举例

**视频中的例子是将字节码文件 用javap -v -p进行反编译 和 jclasslib进行比较**

==要回顾  可以看视频236    因为里面截图的话太多了  就没有截了==



#### 总结

![image-20211210135805760](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210135805760.png)

上面的灰色的  在jclasslib里可以看到  但javap反编译 又把它变回static了



## ==字节码指令集与解析举例（就不做笔记了 知道大概）==

**==康师傅238-265   里面的笔记就不写的那么细致了   不懂了在快速回顾这里面的章节==**

### 概述

![image-20211210141925267](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210141925267.png)



#### 执行模型(了解)

![image-20211210142615454](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210142615454.png)



#### 字节码与数据类型

![image-20211210142849444](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210142849444.png)

![image-20211210143323437](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210143323437.png)



#### 指令分类

![image-20211210143531468](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210143531468.png)



### 加载与存储指令

**加载是加载到操作数栈里    存储是将数据保存在局部变量表中**

![image-20211210145212202](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210145212202.png)

![image-20211210145228584](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210145228584.png)

![image-20211210145430666](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210145430666.png)

 有些可能没有写操作数  但操作数都隐含在指令中。



#### 复习：再谈操作数栈与局部变量表

![image-20211210150109889](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150109889.png)

![image-20211210150302609](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150302609.png)



![image-20211210150355542](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150355542.png)

![image-20211210150409218](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150409218.png)

 ![image-20211210150647979](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150647979.png)

![image-20211210150635532](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150635532.png)



#### 1-局部变量压栈指令

**后面的n那些跟着的是索引**

![image-20211210150917122](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210150917122.png)



#### 2-常量入栈指令

**后面的i那些跟着的是数据**

![image-20211210152814392](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210152814392.png)

**当 int i = 5; iconst_5    但是int i = 6 超出范围了  就只能用bipush 6    如果超过bipush、sipush的范围就会使用  ldc指令**

![image-20211210152913411](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210152913411.png)

![image-20211210153425009](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210153425009.png)

==**三个指令表示范围是依次慢慢变大的**==



**例子👇**

==指令==

![image-20211210153349677](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210153349677.png)





==范围==

![image-20211210153750626](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210153750626.png)



#### 3-出栈装入局部变量表指令

![image-20211210154124543](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210154124543.png)



### 算术指令

![image-20211210160831323](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210160831323.png)

![image-20211210160845385](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210160845385.png)

![image-20211210161028270](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210161028270.png)

**比如 10/0.0就是无穷大 Infinity       0.0/0.0就不确定  不确定是无穷大还是0  所以是NaN**



#### 所有算术指令

![image-20211210161438137](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210161438137.png)



==**几个结果相同 指令不同的**==

​	![image-20211210162641061](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210162641061.png)



==**在减法或除法运算中后出栈的是被减数或者被除数**==



**==取反操作比较巧妙  获取一个常数负一 然后进行取反==**



==**方法中的方法 还会开辟一个新的栈帧  千万注意!!**==



**举例**

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210163635773.png" alt="image-20211210163635773" style="zoom: 67%;" />

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210163745412.png" alt="image-20211210163745412" style="zoom:67%;" />

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210163824691.png" alt="image-20211210163824691" style="zoom:67%;" />

**彻底搞定++运算符**

==前++和后++完全一致 如果不涉及任何运算的话  字节码没有区别==

![image-20211210164401250](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210164401250.png)



==涉及运算==

![image-20211210165340967](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210165340967.png)



后++是先拿出去  然后局部变量表中自增后 再把操作数栈中的 放回局部变量表中

前++是自增以后 再拿到操作数栈中再拿回来



**==思考题==**

![image-20211210164758588](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210164758588.png)

![image-20211210164815187](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210164815187.png)

这个就是  后++是先拿出去  然后局部变量表中自增后 再把操作数栈中的 放回局部变量表中    拿回来正好还是原来的位置  那就覆盖掉了



#### 比较指令的说明

![image-20211210182000662](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211210182000662.png)



### 类型转换指令

![image-20211211133310537](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211133310537.png)

**主要指的是布尔类型之外的七种类型**

==**宽化窄化  可以理解为类型的容量变化**==

#### 1-宽化类型转换

![image-20211211134345395](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211134345395.png)

**是可能发生精度损失的**

![image-20211211140313169](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211140313169.png)



#### 2-窄化类型转换

**有些没有对应的指令   比如long类型转换为byte类型  会先进行long转换为int  再int转换为byte**

![image-20211211140748686](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211140748686.png)



**比较特别的转换(short到byte的转换 直接就是i2b  把short看作int)**

![image-20211211141806985](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211141806985.png)

![image-20211211141827817](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211141827817.png)

![image-20211211142145911](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211142145911.png)



### 对象的创建与访问指令

![image-20211211142807600](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211142807600.png)

**java中也存在对象向下转换    称为强制类型转换      基本数据类型称为窄化类型转换**



#### 1-创建指令

![image-20211211143702029](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211143702029.png)



**举例**

![image-20211211144805729](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211144805729.png)



####  2-字段访问指令

**字节码操作：如果是对应类结构的话  不用把当前对象再压入栈中进行操作   可以直接赋      get是出栈操作   put是压栈操作** 

![image-20211211145119257](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211145119257.png)

![image-20211211145441175](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211145441175.png)

![image-20211211145539376](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211145539376.png)

![image-20211211145549522](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211145549522.png)



**==举例2（看）==**

![image-20211211150329191](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211150329191.png)



#### 3-数组操作指令

**(这里的store不是修改局部变量表   而是修改堆里数组的值)**

![image-20211211150532409](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211150532409.png)

![image-20211211150845989](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211150845989.png)



**==举例分析==**

![image-20211211152244684](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211152244684.png)



#### 4-类型检查指令

![image-20211211152320181](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211152320181.png)



**例子**

![image-20211211152630760](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211152630760.png)



### 方法调用与返回指令



#### 1-方法调用指令

![image-20211211153834453](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211153834453.png)

**静态绑定的方法不会涉及到重写              动态分派就是运行的方法可能是被重写了的**



**==方法调用指令：invokespecial：静态分派==**

![image-20211211155115037](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211155115037.png)

**==方法调用指令：invokestatic：静态分派==**

![image-20211211155322102](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211155322102.png)

//如果是既声明是static又声明是private那它调用的还是已类为准  就是invokestatic



**==方法调用指令：invokeinterface==**

![image-20211211155817650](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211155817650.png)**在接口中定义了静态方法的话    调用编译后产生的字节码  不是invokeinterface了而是invokestatic**



#### 2-方法返回指令

![image-20211211160318930](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211160318930.png)



**举例**

![image-20211211160531628](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211160531628.png)

![image-20211211160738636](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211211160738636.png)



### 操作数栈管理指令



### 控制转移指令

#### 1-条件跳转指令

#### 2-比较条件跳转指令

针对的是int（short和byte类型）、引用数据类型

#### 3-多条件分支跳转

#### 4-无条件跳转



### 异常处理指令

#### 1-抛出异常指令

#### 2-异常处理与异常表



### 同步控制指令

#### 1-方法级的同步

#### 2-方法内指定指令序列的同步





## ==类的加载过程(类的生命周期)详解==

### 01-概述

![image-20211212142203754](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212142203754.png)



![image-20211212182317959](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212182317959.png)



#### 大厂面试题

![image-20211212182534129](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212182534129.png)

![image-20211212182746520](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212182746520.png)



### 02-过程一：Loading(加载)阶段

#### 1-加载完成的操作

![image-20211212183150890](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212183150890.png)

#### 2-二进制流的获取方式

![image-20211212183619922](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212183619922.png)

#### 3-类模型与Class实例的位置

![image-20211212184252546](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212184252546.png)

![image-20211212184354683](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212184354683.png)

![image-20211212184523242](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212184523242.png)



**例子（通过反射获取到堆中的实例  clazz在栈上    实例又指向方法区的类模板）**

![image-20211212184953661](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212184953661.png)

![image-20211212185156907](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212185156907.png)

#### 4-数组类的加载

![image-20211212185416890](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212185416890.png)



### 03-过程二：Linking(链接)阶段

#### 1-环节1：链接阶段之认证

![image-20211212185939519](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212185939519.png)

![image-20211212190426923](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212190426923.png)

![image-20211212190521139](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212190521139.png)



#### 2-环节2：链接阶段之准备

**(类的初始化  涉及到的是静态结构)**

![image-20211212192223756](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212192223756.png)

![image-20211212192435658](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212192435658.png)

#### 3-环节3：链接阶段之解析

![image-20211212193219511](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212193219511.png)

![image-20211212194426944](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212194426944.png)

![image-20211212194549952](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211212194549952.png)

### 04-过程三：Initialization(初始化)阶段

![image-20211213132959608](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213132959608.png)

**静态变量的赋值 静态代码块的执行都是在这一阶段 在clinit方法执行时执行**

![image-20211213134414004](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213134414004.png)

 **类中没有加static的变量称为实例变量    加了的称为类变量**



#### 1-static与final的搭配问题

![image-20211213140715366](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213140715366.png)

**例子**

![image-20211213140731451](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213140731451.png)

**只要涉及到方法的支持     哪怕是加了final也是在clinit中赋值**

**==最终结论：使用static+final修饰，且显示赋值中不涉及到方法或构造器调用的基本数据类型或String类型的显式赋值，是在链接阶段的准备环节进行。==**



#### 2- < clinit >()的线程安全性

![image-20211213141343823](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213141343823.png)

//可能会出现死锁问题 



#### 3-类的初始化情况：主动使用vs被动使用

**主动使用会进行初始化  被动使用不会进行初始化  同时这不代表该类不被加载**

![image-20211213142006239](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213142006239.png)

![image-20211213142310122](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213142310122.png)

![image-20211213142537531](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213142537531.png)

**tips:**

**1、文件输出 如果要将自定义类的实例对象输出 千万要记得让类实现序列化接口**

**2、测试了一下  反序列化调用clinit是不是因为强制转换类型才调用？  原来并不是**



**==如果针对代码，设置参数-XX:+TraceClassLoading ,可以追踪类的加载信息并打印出来。==**

![image-20211213152250837](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213152250837.png)



### 05-过程四：类的Using(使用)

![image-20211213162218122](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213162218122.png)

### 06-过程五：类的Unloading(卸载)

![image-20211213162618186](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213162618186.png)

![image-20211213163135499](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213163135499.png)

![image-20211213163412532](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213163412532.png)

![image-20211213164109349](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213164109349.png)



#### 回顾：方法区的垃圾回收

![image-20211213163430496](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211213163430496.png)



## ==再谈类的加载器==

### 01-概述

![image-20211214151441780](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214151441780.png)

![image-20211214153524355](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214153524355.png)



#### 1-大厂面试题

![image-20211214153746873](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214153746873.png)

![image-20211214153821301](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214153821301.png)

#### 2-类加载的分类

![image-20211214153851809](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214153851809.png)

#### 3-类加载器的必要性

![image-20211214154325502](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214154325502.png)

#### 4-命名空间

![image-20211214154622157](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214154622157.png)



**自定义加载器加载的是这个自己放的路径，而系统自带的加载器还是加载默认情况下out里面的字节码文件**



#### 5-类加载机制的基本特征

![image-20211214155832291](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214155832291.png)



### 02-复习：类的加载器分类

**==类的加载器 可以看之前的==**

#### **启动类加载器（引导类加载器）BootstrapClassLoader**

==这个类加载使用C/C++语言实现的，嵌套在JVM内部。==

==并不继承自java.lang.ClassLoader，没有父加载器==

==加载扩展类和应用程序类加载器，并指定为他们的父类加载器==

==当你获取一个类的加载器   当加载器为null时 代表加载它的类加载器是引导类加载器==

#### **扩展类加载器 ExtensionClassLoader **

==和下面的系统类加载器是并列的 但是系统类加载器的parent**属性**是扩展类加载器  这并没有影响==

#### **系统类加载器 AppClassLoader**

==是用户自定义类加载器的默认父加载器==

==通过ClassLoader的getSystemClassLoader()方法获取==

#### **用户自定义类加载器**

![image-20211214165623908](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211214165623908.png)

### 03-测试不同的类加载器

![image-20211216133132596](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216133132596.png)

 ![image-20211216133436316](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216133436316.png)

==基本数据类型不用加载    引用数据类型需要类加载器加载      两个null的意义是不一样的==



### 04-ClassLoader源码解析

**==ClassLoader是一个抽象类  但是内部没有抽象方法==**

![image-20211216134503046](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216134503046.png)



#### ClassLoader的主要方法（P292进行了源码解析）

**满足双亲委派机制的主要逻辑就是由loadClass()来实现的**

![image-20211216135140487](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216135140487.png)

**findClass方法中的核心方法是defineClass方法**

![image-20211216142227073](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216142227073.png)

![image-20211216142510830](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216142510830.png)



#### SecureClassLoader与URLClassLoader

![image-20211216143130786](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216143130786.png)

==知道URLClassLoader中对findClass进行了一个实现==



#### ExtClassLoader与AppClassLoader

![image-20211216143637716](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216143637716.png)

![image-20211216143720218](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216143720218.png)

==AppClassLoader中虽然重载了loadClass()方法  但其内部还是调用了父类的loadClass()方法  所以其依然遵守双亲委派模式==



#### Class.forName()与ClassLoader.loadClass()

![image-20211216144045689](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216144045689.png)

**==还有区别就是Class.forName()是主动使用   ClassLoader.loadClass()是被动使用 不会调用类的初始化==**

 

### 05-双亲委派模型

#### 定义与本质

![image-20211216145206457](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216145206457.png)

![image-20211216145335920](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216145335920.png)

![image-20211216145352541](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216145352541.png)



#### 优势与劣势

![image-20211216145637891](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216145637891.png)

![](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216151846100.png)

![image-20211216152148877](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216152148877.png)

**Tomcat中的类加载器违背了双亲委派机制**



#### 破坏双亲委派机制 

**双亲委派模型主要出现过3次较大规模“被破坏”的情况**

##### **破坏双亲委派机制1**

![image-20211216153042719](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216153042719.png)



##### **破坏双亲委派机制2**

**如果有基础类型又要调用回用户的代码   这时候就出现了线程上下文类加载器，这个行为实际打通了双亲委派模型的层次结构来逆向使用类加载器，已经违背了双亲委派模型的一般性原则**

![image-20211216154233725](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216154233725.png)

**默认上下文加载器就是应用类加载器**



##### **破坏双亲委派机制3**

![image-20211216154600299](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216154600299.png)

**热部署就类似于电脑的外设  插上就能用  不好用就换**



##### 小结

![image-20211216155207296](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216155207296.png)



#### 热替换的实现

![image-20211216160143691](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216160143691.png)

![image-20211216163255241](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216163255241.png)



### 06-沙箱安全机制

![image-20211216164157132](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216164157132.png)



#### JDK1.0时期

![image-20211216164419647](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216164419647.png)



#### JDK1.1时期

![image-20211216164747515](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216164747515.png)



#### JDK1.2时期

![image-20211216164828904](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216164828904.png)

![image-20211216164847843](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216164847843.png)



#### JDK1.6时期

 ![image-20211216164948121](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211216164948121.png)



### 07-自定义类的加载器

![image-20211217132708592](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217132708592.png)

![image-20211217132835467](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217132835467.png)



#### 实现方式

**推荐对findClass进行重写**

![image-20211217132956936](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217132956936.png)

![image-20211217133307403](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217133307403.png)



==**自定义类加载器例子👇**==

![image-20211217133715701](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217133715701.png)

 ![image-20211217134042143](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217134042143.png)

![image-20211217161515370](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217161515370.png)

==**测试**==

![image-20211217134242684](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217134242684.png)



### 08-Java9新特性

![image-20211217134824136](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217134824136.png)

![image-20211217135144091](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217135144091.png)

![image-20211217135157150](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217135157150.png)

![image-20211217135352878](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217135352878.png)

![image-20211217135411508](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217135411508.png)

![image-20211217135454519](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217135454519.png)

![image-20211217135517862](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211217135517862.png)





# 性能监控与调优篇



## ==概述篇==

### 1-大厂面试题

![image-20211218134832181](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218134832181.png)

![image-20211218135037314](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135037314.png)



### 2-背景说明

![image-20211218135205186](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135205186.png)



### 3-调优概述

![image-20211218135430058](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135430058.png)



### 4-性能优化的步骤

**性能监控**

![image-20211218135827364](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135827364.png)

![image-20211218135633085](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135633085.png)





**性能分析**

![image-20211218140345732](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218140345732.png)

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135655252.png" alt="image-20211218135655252" style="zoom:98%;" />



**性能调优**

![image-20211218140644493](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218140644493.png)

![image-20211218135802894](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218135802894.png)

 

### 5-性能评价/测试指标

**停顿时间展开**

![image-20211218141148526](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218141148526.png)

![image-20211218141208377](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218141208377.png)



![image-20211218140921924](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218140921924.png)

![image-20211218141554504](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218141554504.png)



## ==JVM监控及诊断工具-命令篇（纯文本的界面看）==



### 01-概述

![image-20211218142819252](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218142819252.png)



#### **简单命令行工具**

![image-20211218143135727](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218143135727.png)



### 02-jps：查看正在运行的Java进程



#### **基本情况**

![image-20211218143935166](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218143935166.png)



#### 测试

![image-20211218145049723](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218145049723.png)



#### 基本语法

![image-20211218145123252](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218145123252.png)

**options参数**

![image-20211218145222192](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218145222192.png)

![image-20211218145449044](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218145449044.png)



![image-20211218145552940](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218145552940.png)

**jps-m 就是进程启动时传递给主类的参数**



![image-20211218145933142](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218145933142.png)

**jps-v 可以显示JVM参数**



**==综合使用时可以是jps-lv或者jps-l-v     参数中-q是独立的不能混合用==**



**hostid参数**

![image-20211218150355887](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211218150355887.png)



### 03-jstat：查看JVM统计信息



#### 基本情况

![image-20211219195201782](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219195201782.png)



#### 基本语法

![image-20211219195447962](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219195447962.png)



![image-20211219195808702](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219195808702.png)

**-t参数经验**

![image-20211219202248563](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219202248563.png)

![image-20211219201620045](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219201620045.png)



**tips：**当你interval和count不写时  默认只查询一次   当你要写了一个参数后 默认是interval

**例子：**

![image-20211219200426111](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219200426111.png)



==**option参数展开**==

![image-20211219200901919](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219200901919.png)

![image-20211219200931277](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219200931277.png)







**例子JIT相关**

![image-20211219201222339](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219201222339.png)



**例子垃圾回收相关**

![image-20211219201805476](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219201805476.png)



#### 补充

![image-20211219202510974](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219202510974.png)



### 04-jinfo：实时查看和修改JVM配置参数

如果是设置过的参数 在运行时可以用其他命令查看  比如jps -v 可以看出设置的内存大小

#### 基本情况

![image-20211219202736742](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219202736742.png)

![image-20211219203018036](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219203018036.png)



#### 基本语法

![image-20211219203210679](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219203210679.png)

![image-20211219203326015](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219203326015.png)

**修改**

![image-20211219204010298](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219204010298.png)

![image-20211219204024396](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219204024396.png)

**运行结束后   再次运行 参数失效**



**相较于拓展类型  jinfo的力度更小一点**

#### 扩展

![image-20211219204449718](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219204449718.png)



### 05-jmap：导出内存映像文件＆内存使用情况

#### 基本情况

![image-20211219204930790](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219204930790.png)



#### 基本语法

 ![image-20211219210300878](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219210300878.png)

![image-20211219210251973](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219210251973.png)



#### 使用1：导出内存映像文件

![image-20211219211136609](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219211136609.png)![image-20211219211205575](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219211205575.png)



**生成dump文件分为两种方式**

![image-20211219211043801](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219211043801.png)



==**手动和自动针对的场景不一样  不是非要你进行二选一**==

**手动**

:cactus: format=b的目的就是jmap生成的文件能和hprof格式的文件匹配起来

:dancer:加了:live就是代表只保存活着的对象

**自动**

![image-20211219212019833](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219212019833.png)



#### 使用2：显示堆内存相关信息

![image-20211219212353962](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219212353962.png)

**针对的是时间点上的相关数据  和jstat相比较弱**



#### 使用3：其他作用

![image-20211219212359840](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219212359840.png)



#### 小结

==**必须要在安全点进行操作**==

![image-20211219213112258](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219213112258.png)





### 06-jhat：JDK自带堆分析工具

#### 基本情况

![image-20211219214011137](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219214011137.png)



#### 基本语法

![image-20211219214131881](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219214131881.png)



![image-20211219214609824](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211219214609824.png)





### 07-jstack：打印JVM中线程快照

#### 基本情况

![image-20211220105242104](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220105242104.png)

![image-20211220105257677](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220105257677.png)



#### 基本语法

![image-20211220105426837](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220105426837.png)

![image-20211220105454333](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220105454333.png)

**通过这个指令可以分析出来 是哪个线程 是什么状态引起的 对应的操作是什么**

![image-20211220110151547](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220110151547.png)

**不通过jvm查看  也可以用java中Thread类的getAllStackTraces方法查看**



### 08-jcmd：多功能命令行

#### 基本使用

![image-20211220110750250](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220110750250.png)

**代替了大部分前面的命令   除了jstat**

#### 基本语法

![image-20211220110949497](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220110949497.png)

**通过help调用出指令  然后 用 jcmd pid 具体命令 可以进行执行**





### 09-jstatd：远程主机信息收集（了解）

![image-20211220111553936](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220111553936.png)





## ==JVM监控及诊断工具-GUI篇==

### 01-工具概述

![image-20211220122446953](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220122446953.png)



**==图形化综合诊断工具==**

![image-20211220123059871](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220123059871.png)

![image-20211220123332562](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220123332562.png)



### 02-jConsole

#### 基本概述

![image-20211220123800677](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220123800677.png)



#### 启动

![image-20211220124155277](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220124155277.png)

**或者在cmd中直接输入jconsole就可以了**



![image-20211220124145946](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220124145946.png)

![image-20211220125226910](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220125226910.png)



#### 三种连接方式

![image-20211220124326017](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220124326017.png)

**本地连接  启动jconsole的用户和启动java程序的用户必须是同一个**



#### 主要作用

**对JVM中内存、线程、类等监控  还能检测死锁**



### 03-Visual VM

#### 基本概述

![image-20211220130109022](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220130109022.png)

JVisualVM和VisualVM一个在jdk bin目录下一个是通过独立安装的



#### 插件的安装

![image-20211220131743972](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220131743972.png)

![image-20211220132114465](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220132114465.png)



**安装插件版本一定是要对应**



#### 连接方式

![image-20211220132248712](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220132248712.png)



#### 主要功能

![image-20211220133938425](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220133938425.png)

![image-20211220134539842](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220134539842.png)

**可以自己试着查看     功能很强大      上面功能实现步骤 看shk323之后**

**可以生成dump文件  查看dump文件  两个dump文件进行比较     还可以抽样  热点线程**

**当程序始终结束不了  检查看看有没有死锁  cpu谁占用率比较高    如果fullgc多或者oom 看内存 dump文件  比较**



### 04-eclipse MAT

**==主要是用来分析dump文件==**

#### 基本概述  

![image-20211220142757004](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220142757004.png)



#### 获取堆dump文件

**dump文件内容**

![image-20211220144012355](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220144012355.png)



**两点说明**

![image-20211220144350224](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220144350224.png)



**获取dump文件**

![image-20211220145322960](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211220145322960.png)



#### 分析堆dump文件

**看shk328  或者自己进行分析  很多常用的方法  他视频中有讲  要看看**

![image-20211221142155074](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221142155074.png)

**==浅堆与深堆==**

**浅堆**

![image-20211221145743668](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221145743668.png)

比如这里就和value的取值无关  只是记录它是引用对象



**深堆**

![image-20211221150204300](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221150204300.png)



**补充：对象的实际大小**

![image-20211221150510567](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221150510567.png)

所能触及的  而不是只能通过它访问的



**实际的案例讲解浅堆深堆是怎么计算出来的  看shk332**



**==支配树==**

![image-20211221152825626](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221152825626.png)

![image-20211221152922427](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221152922427.png)





#### 例：TomCat堆溢出分析

看shk334



### 补充1：再谈内存泄漏

#### 内存泄漏的理解与分类

![image-20211221162420309](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221162420309.png)

![image-20211221162634460](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221162634460.png)

![image-20211221162814067](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221162814067.png)

![image-20211221162920880](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221162920880.png)



#### Java中内存泄露的8种情况

![image-20211221163045147](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221163045147.png)



![image-20211221165258438](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221165258438.png)



![image-20211221165350811](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221165350811.png)



![image-20211221165421628](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221165421628.png)



![image-20211221165519084](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221165519084.png)



![image-20211221165649778](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221165649778.png)



![image-20211221170458943](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221170458943.png)

**放进去了以后  又把参与计算哈希值的值修改了  那就移除不掉  找不到了       下面的例子就是说移除失败 最后打印还能看到    还有例子336可看**

![image-20211221170952557](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221170952557.png)

![image-20211221170958762](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221170958762.png)





![image-20211221171328969](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221171328969.png)



![image-20211221171603960](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221171603960.png)



#### 内存泄漏案例分析

看337-338     一些隐蔽的泄漏问题



### 补充2：支持使用OQL语言查询对象信息

![image-20211221183113956](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221183113956.png)



#### SELECT子句

![image-20211221183419805](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221183419805.png)

#### FROM子句

![image-20211221183821884](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221183821884.png)

#### WHERE子句

![image-20211221183844050](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221183844050.png)

#### 内置对象与方法

![image-20211221183942249](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211221183942249.png)



### 05-JProfiler

#### 基本概述

**介绍**

![image-20211222191351174](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222191351174.png)



**特点**

![image-20211222191541737](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222191541737.png)



**主要功能**

![image-20211222192034350](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222192034350.png)





#### 安装与配置

==安装与配置  看shk341就行了==



#### 具体使用

![image-20211222194102403](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222194102403.png)

**数据采集方式**

![image-20211222194247127](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222194247127.png)

![image-20211222194301499](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222194301499.png)



**==具体实现 看shk    然后熟悉的话  还得再进行运用时再进行熟悉==**

![image-20211222195536712](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211222195536712.png)

#### 案例分析

**==看shk视频==**



### 06-Arthas（服务器）

#### 基本概述

**背景**

**==主要是针对项目上线后 对服务器进行监控==**

![image-20211223090525815](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223090525815.png)



**概述**

![image-20211223093358337](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223093358337.png)



**基于哪些工具开发而来**

![image-20211223093555273](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223093555273.png)



**官方使用文档**

==**https://arthas.aliyun.com/zh-cn/**==

**==学习指令只要打开官方文档进行查询即可==**



#### 安装与使用（linux）

#### 相关诊断指令

看shk351-358

#### ![image-20211223095123802](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223095123802.png)

### 07-Java Mission Control

#### 启动

jdk bin目录下的

#### 概述

![image-20211223102159485](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223102159485.png)



#### 功能：实时监控JVM运行时的状态

#### Java Flight Recorder(飞行记录器)

![image-20211223102718257](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223102718257.png)



### 08-其他工具

![image-20211223103110251](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211223103110251.png)



**==用到的时候   从shk363之后找  这就不做笔记了太多了==**

## ==JVM运行时参数==

**-  -X  -XX  三种类型的参数选项**

**==tips==**

1.

![image-20211224084614122](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224084614122.png)

2.程序的执行方式

![image-20211224084635593](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224084635593.png)

3.类型-XX重要

![image-20211224084849838](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224084849838.png)

4.添加JVM参数选项

![image-20211224090423248](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224090423248.png)



5.常用的JVM参数选项   堆、栈、方法区等内存大小设置

![image-20211224091820769](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224091820769.png)







![image-20211224092256584](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224092256584.png)

 ![image-20211224093606046](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224093606046.png)

**要想默认的伊甸园区和幸存者区的8：1：1有效 需要管不AdaptiveSizePolicy还得显式的给SurvivorRatio进行赋值         如果显式的定义了SurvivorRatio那么肯定是以它为准   不管你开没开自适应**



6.

![image-20211224093904705](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224093904705.png)



7.

![image-20211224095643731](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224095643731.png)

**查看默认垃圾收集器**

![image-20211224095716662](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224095716662.png)

**Serial回收器**

![image-20211224100533124](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224100533124.png)

**ParNew回收器**

![image-20211224100713656](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224100713656.png) 

**Parallel回收器**

![image-20211224100821016](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224100821016.png)

![image-20211224101130963](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224101130963.png)

**CMS回收器**

![image-20211224101148563](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224101148563.png)

![image-20211224101403168](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224101403168.png)

![image-20211224101546981](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224101546981.png) 

**G1回收器**

![image-20211224101743966](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224101743966.png)

![image-20211224101722031](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224101722031.png)

**怎么选择垃圾回收器**

  ![image-20211224102012539](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224102012539.png)

7.GC日志相关选项

![image-20211224103410629](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224103410629.png)

![image-20211224103442849](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224103442849.png)

8.其他参数

![image-20211224103749911](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224103749911.png)

9.通过java代码获取JVM参数

![image-20211224104903819](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224104903819.png)

![image-20211224104926070](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224104926070.png)







## ==分析GC日志==

**复习GC分类**

![image-20211224112437996](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224112437996.png)

![image-20211224112824527](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224112824527.png)



**GC日志分类**

==MinorGC日志 （解析的话看377）==

![image-20211224113623030](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224113623030.png)



==FullGC  （解析的话看378）==

![image-20211224113716257](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224113716257.png)



==日志中各种垃圾回收器的叫法==

![image-20211224113903794](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224113903794.png)

==GC前后情况==

![image-20211224114000830](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224114000830.png)

==GC时间==

![image-20211224114128799](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224114128799.png)

==GC结束后打印的JVM堆总大小  并不是真正的总大小是新生代的9/10+老年代 因为其中一个幸存者区不算进去==







**==GC日志分析工具==**

![image-20211224115702970](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224115702970.png)

![image-20211224115743950](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224115743950.png)

**GCeasy**

![image-20211224120611692](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224120611692.png)

**GCViewer**

![image-20211224121259371](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224121259371.png)



 **其他工具**

 ![image-20211224121407023](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20211224121407023.png)







**大厂学院里有后面的**

## ==OOM常见各种场景及解决方案==

## ==性能优化案例==

## ==Java代码层及其他层面调优==





















































































































