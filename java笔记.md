常用的DOS命令

1. cls---清屏

2. exit---退出当前DOS窗口

3. 右键标记---复制

4. dir---当前页面所有子文件

5. cd---改变目录

   cd  目录路径

6. cd..---回到上一级目录

   cd\---直接回到根目录

7. d：

   c：切换盘符



# idea快捷键

`psvm`  生成main方法

`sout` 生成System.out.println();

IDEA不需要一直保存CTRL+s，自动保存

`ctrl+y` 删除一行

`ctrl+shift+F10` 运行

`左箭头  右箭头 ` 左侧的列表展开，关闭

`alt+insert` 新建一个类

`esc` 退出任何窗口，可以实现光标从project转到代码行

`ctrl+shift+F12` 窗口变小变大

`alt+左箭头\右箭头` 切换窗口

`alt+数字` 切换相关窗口

双击 shift  打开全局搜索界面，可以搜索类，或者方法  最常用：写一个类，然后ctrl点过去

在类中搜索方法名  ctrl + F12



# .exe与.class的区别

.exe是win系统特有的

.class字节码文件是跑在jvm上的

- 特殊的可执行文件，需要jvm
- 优点：跨平台
- 缺点：过于依赖虚拟机



# JDK,JRE,JVM

- JDK：java开发工具箱
- JRE：java运行环境
- JVM：java虚拟机

JDK包括JRE，JRE包括JVM

JVM不能独立安装，JDK和JRE都可以独立安装，有单独的JDK安装包，有单独的JRE安装包，没有单独的JVM安装包

安装JDK的时候，JRE就自动安装了，同时JRE内部的JVM也就自动安装了

安装JRE的时候，JVM也就自动安装了

问题：假设在软件公司开发了一个新的软件，现在要去客户那边给客户把项目部署一下，把项目跑起来，需要安装JDK吗？

不需要，只需要安装JRE就行了，JRE体积很小，安装非常便捷快速。



java体系的技术被划分为三大块：

- JavaSE：标准版
- JavaEE：企业版
- JavaME：微型版



## jdk新特性

```java
java +,java文件的路径名
```

这样也可以运行，但是不会在磁盘上生成.class文件，而是生成在内存里。



# path

path环境变量的作用就是给windows操作系统指路的，告诉windows操作系统去哪里找这个命令文件

path环境变量中有很多很多的路径，路径和路径之间用半角（英文）分号分隔

更改完环境变量之后，dos命令窗口一定要重新启动。



# classpath

> 是java特有的环境变量

**classpath是给类加载器指路的**，一般来讲不用配置。若不配置，类加载器会默认到当前文件夹下找.class文件，若配置了，类加载器只能到配置的位置找.class 文件了，不会到当前路径下加载了，配还不如不配。

若要配置，在windows环境变量窗口中新建一个环境变量class，再输入值，用分号隔开。



# java_home

javaweb中会用到



# 注释和文档

- 生成Java文件的API
  - 网上查阅JavaDoc的详解，都找得到
    - @author
    - @since
    - @version
  - 指令
- 打开生成API的目录——**index.html**
- **方法外部注释一定要用/**,不要用//**
- 方法内部注释，单行用//，多行用/*（在语句上面写，且//后面加空格）
- 所有**类**都要加上**创作者和日期**
- 特殊注释标记（标记人，标记时间，[预计处理时间]）
  - TODO：需要实现，但还未实现
  - FIXME：错误代码，无法工作，需要纠正



# 注意事项

## 常量

- 常量定义不同于c/c++
  - c/c++：const
  - Java：final

## 字符串

### 相关方法

```java
int	compareTo(String anotherString); // 按字典顺序比较两个字符串
String	concat(String str); //拼接
boolean	contains(CharSequence s);//包含则为true
boolean	endsWith(String suffix);//测试此字符串是否以指定的后缀结尾。
boolean	equals(Object anObject);  
byte[]	getBytes(); // 使用平台的默认字符集将此 String编码为字节序列，将结果存储到新的字节数组中
int	indexOf(int ch);//返回指定字符第一次出现的字符串内的索引。
int	indexOf(int ch, int fromIndex);//返回指定字符第一次出现的字符串内的索引，以指定的索引开始搜索。
int	indexOf(String str);//返回指定子字符串第一次出现的字符串内的索引
int	indexOf(String str, int fromIndex);//返回指定子串的第一次出现的字符串中的索引，从指定的索引开始。
boolean	isEmpty();//返回 true如果，且仅当 length()为 0 
// 同理也有	lastIndexOf,也是从指定索引向后搜索
boolean	matches(String regex);//告诉这个字符串是否匹配给定的 regular expression 
String	replace(CharSequence target, CharSequence replacement);// 将与字面目标序列匹配的字符串的每个子字符串替换为指定的字面替换序列。
String	substring(int beginIndex, int endIndex);// 返回一个字符串，该字符串是此字符串的子字符串。
char[]	toCharArray();//将此字符串转换为新的字符数组
String	trim();// 返回一个字符串，其值为此字符串，并删除任何前导和尾随空格。
static String valueOf();// 返回字符串形式
// 自动调用toString()方法，println()中也调用了valueOf()方法
    
```



### StringBuffer

java当中的字符串是不可变的，每一次拼接都会创建新的字符串

StringBuffer  利用数组拷贝扩容，默认byte[]容量为16 

优化StringBuffer的性能：最好减少底层数组的扩容次数，预估计以下，给一个大一些的初始化量     关键点：给一个**合适**的初始化容量

#### 与StringBuilder的区别

- StringBuffer 的方法前都有一个`synchronized` 修饰，表示StringBuffer在多线程环境下是安全的，而StringBuilder多线程不安全
- StringBuilder效率更高





- 格式化输出
  - System.out.printf();（同C语言）
- 格式化创建
  - String.format();
- 等等一系列操作，一定要下功夫，很重要！包括正则表达式。
- 为了开发的友好，隐含了’\0’
  - ‘\0’的作用——结束符，堵住字符串，不然会“烫烫烫”

## 自动类型转换

- 从低到高

  ：byte/short/char->int->long->float->double

  - 《主角与配角》小品（朱时茂、陈佩斯）
    - 前半段：int与char
    - 后半段：String与char——有函数不用
  - 能String就不要char

## 数组

初始化：（推荐）

```java
int[] array = {1,2,3};
```

分配方式：对象

```java
int[] array = new int[5];
```

数组的length是变量，不是方法，不用括号！！

以上都是静态数组，java不常用，因为java有专门的数组类**Arrays**



# OOP

java没有指针的概念，对象变量**引用**对象，而不是指向对象

一个对象变量没有实际包含一个对象，而是仅仅引用一个对象

```java
Date deadline;// 定义一个对象变量deadline，它可以引用Date类型的对象，但是deadline不是一个对象，不能对deadline使用Date类的方法
Date birthday = new Date();// 此时对象变量birthday引用了一个对象，可以对birthday使用Date的方法
// 可以显式的将对象变量设置为null
Date deadline = null;
// 如果将一个方法应用于一个值为null的对象上，就会产生运行时错误

```

1. getter和setter都是public，允许外部方法访问的



## 增强for循环---For Each

```java 
for (int num:list){
    System.out.println(num);
}
```



# 方法的重载

> 优点：一个名字闯天下

- 方法名字相同
- 参数不同
  - 个数不同
  - 类型不同
  - 顺序不同（注意要是不同类型形参的顺序）

```java
public static int sum(int x,int y){
	return x + y;
}
public static double sum(int x,int y){
	return x + y;
}
public static int sum(int x,int y,int z){
	return x + y + z;
}
```

只有函数的返回类型不同，不叫作重载，会报错





# 常用jar包搜索

maven repository

## jar包添加流程

- 去maven repository搜索，下载
- 项目文件下new directory
- 把jar包拖到directory下
- 右键jar包，点击add as library
- 不要忘记这一步，不然可能还是会出现找不到set方法的情况
- ![image-20210125204427639](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210125204427639.png)



导入包时，若两个类名相同但属于不同的包，则要写出完整的包名+类名

```java
java.util.Date deadline = new java.util.Date();
java.sql.Date today = new java.sql.Date();
```

`import`语句的唯一好处是简洁



# 构造方法

若自己在类下写了一个构造方法，记得把无参构造器加上，这非常重要！！构造方法的最终目的：初始化对象（实例）



# this 的两种情况

- （调用该类的其他构造器）this.name = name ; 这里this.name指**类中的name**
- （引用隐式参数）用在方法中，如在sleep()中可以调用eat()方法，这时eat()就要用this.eat()。this这里指创建的**实例**



# 垃圾回收机制

```java
System.gc();
```



# 静态变量、方法

> 建立在**类**的基础上，用类名直接访问、
>
> 静态类，变量，方法是一套，非静态类，变量，方法是一套

### 特点：不能改动了；针对类

- 静态变量：如小区名。

  public 时直接调用Dogs.plot ; private 时写 getPlotInstance() ;

  ```java
  private static String getPlotInstance(){
      return plot;  // 这里不用写this
  }
  ```

  调用时使用

  ```java
  Dogs.getPlotInstance();//在不new一个新的对象的情况下，直接获得小区名
  ```

  此时使用static类型的变量，return时不能returnthis.plot了，而是直接return plot。

- 静态方法：如给所有的狗打针。

  静态方法的调用用类名.    若使用引用.会使程序员产生困惑（会认为这个方法是一个实例方法），若是引用. 其实还是要看该引用所属的类，而不是看其指向的对象的类。（多态中会有这种情况）

静态代码块（自己看书）

```java

public class Employee {
	
	//静态代码块-----------1
	static {
		//do something...
	}
	
	//初始化块------------2
	{
		//do something...
	}
	
	private void fun() {
		//代码块---------3
		{
			//do something...
		}
	}

```

1. 在类进行加载时会执行静态代码块（优于初始化块、构造函数），并且只执行一次，这是一个SUN准备的类加载时机，在类加载时想做的工作写到这里。

2. 在执行构造函数前会执行初始化块。

3. 在执行方法时会执行相应的代码块。



## 单例设计模式



# 内部类

一个文件内部通常只有一个类

> 一个文件里面只能有一个public 

内部类分两种情况：（不常用）

1. 一个文件里面有两个类
2. 一个文件里面有一个类，该类里面还有一个类



# 继承

> 有其父必有其子
>
> **不能继承父类的构造方法**

从一个抽象的Animal类中继承他们的共性，在每一个类中再写他们的个性

```java
public class Dogs extends Animal{
    // 个性...
}
```

- java不支持多继承，即一个类同时继承两个类，但C++是支持的

- 但java支持多层继承（饿狼传说）

可以使用如下代码实现java的多继承

```java
class A extends B;
class B extends C;
```

这样A就同时继承了B和C类



## 注意事项：

1. 默认修饰符：（什么也不加）即在同包中的类之间可见（public），在不同包中的类之间不可见（private）
2. 子类继承父类的方法时，子类当中重写的方法的访问权限（access）不能比父类中的低。



# 子类当中方法的重写

> 在子类当中，凡是有@override的方法，此方法一定来自它的父类，但是它又不学它的父类，成为了子类自己拥有的特性，从它的父类那里革新了，**重写了父类的方法**

注意与重载的区分：

重载是指：方法的参数个数和参数类型不同

## super的用法

- （调用超类的方法）在子类中使用super.方法名，调用父类中同名的方法
- （调用超类的构造器）子类写构造方法时，若父类中已有构造方法，则使用如下形式继承

```java
public Dogs(String name, int age){
    super(name, age);
}
// 调用构造器的语句只能作为另一个构造器的第一条语句出现
```





# final

> 一句话：final表示最终的，不可变的

特点

1. final修饰类名，该类不能被继承了

2. final修饰方法，该方法在子类中不能被重写了，但是还是可以被调用，只是不能为所欲为地修改了

3. final修饰变量，该变量不能再被更改了（规范：**此时该变量为常量，全部大写，遵守命名规范**）

   final修饰的实例变量一般和static联合使用，称为常量

   ```java
   public static final double PI = 3.14;
   ```

4. final修饰的引用一但指向某个对象，则不能再重新指向其他对象，但该引用指向的对象内部的数据是可以修改的。

5. final修饰的实例变量必须手动初始化，不能采用系统默认值。



# abstract抽象

1. 抽象类：只能被继承，不能被new

2. 抽象方法：不能有实际意义（**抽象方法必须在抽象类中**，即该类必须有abstract修饰符）

   但是抽象类中不一定有抽象方法。

3. 一但某个类继承了抽象类，则该类中必须要重写抽象类中所有的的抽象方法，且**不使用super**（否则编译不通过)

   重写时去掉abstract，加上大括号（函数体）



非抽象类继承抽象类必须要将抽象方法实现



# interface接口

> 抽象类是对具体事物的抽象，而接口是对动作，行为的抽象

## frank

1. 其中所有的方法都是抽象的，不能有body（默认方法抽象，不加abstract）
2. 接口的实现：implements. 类实现接口时，所有的方法都要实现（重写）
3. 接口可以new
4. 匿名内部类：new一个接口，可以没有名字

```java
// Human是一个interface
new Human(){
    @Override
    public void eat(){
        System.out.println("中国人吃中国菜");
    }
}.eat();
```

## 老杜

1. 接口也是一种引用数据类型

2. 接口是完全抽象的（抽象类是半抽象），或者说接口是特殊的抽象类

3. 接口定义

   [修饰符列表] interface 接口名{}     没有class

4. 接口里面只能有两样东西，**常量**和**抽象方法**（没有方法体）

   ```java
   public abstract void sum(int a,int b); // public abstract 可以省略
   public static final double PI = 3.1415926; // public static final可以省略
   int k = 100; // k也是常量，public static final 省略了
   ```

5. 接口之间支持多继承

   ```java
   interface A extends B,C{
       
   }
   ```

   

### 接口的基础语法

1. 接口是一种“引用数据类型”。
2. 接口是完全抽象的。
3. 接口怎么定义  [修饰符列表]  interface  接口名
4. 接口支持多继承（接口与接口之间支持多继承）
5. 接口中只有常量+抽象方法
6. 接口中的所有元素都是public修饰的
7. 接口中抽象方法的public abstract可以省略
8. 接口中常量的public static final 可以省略
9. 接口中方法**不能有**方法体。
10. 一个非抽象的类实现接口的时候，必须将接口中所有的方法加以实现。
11. 一个类可以同时实现多个接口。
12. 继承，实现同时出现时，继承在前，实现在后。
13. 使用接口写代码时，可以使用多态，父类型引用指向子类型对象。

### 接口的实现

类和类之间叫做继承extends，类和接口之间叫做实现implements，你也可以把它当作继承。

编写一个**非抽象**的类去实现implements一个接口，必须要将接口中的抽象方法==**重写，覆盖，实现**==，否则会报错（常量不用管，自动继承）；编写一个**抽象类**（加上abstract）去实现implements一个接口，不用重写，不会报错。

==结论：当一个非抽象的类实现接口的话，必须将接口中所有的抽象方法全部实现，覆盖，重写。==

#### 注意事项：

子类中实现（其实是继承）接口中的方法时，方法的访问权限级别不能比接口中的public更低，可以相等或者更高。（子类中至少要是public）public已经是最高了，所以实现接口只能是public

#### 面向接口编程

```java
MyMath mm = new MyMathmpl();// MyMathmpl是实现接口MyMath的子类
```



### 类与接口

一个类可以实现多个接口，但是该类中要实现所有实现接口中的抽象方法，一个都不能少。这种多实现机制弥补了java当中的一个缺陷：单继承。java当中的多实现接口弥补了java当中的单继承缺陷。

注意事项：

1. 经过测试，接口与接口之间没有继承关系，也可以进行强制类型转换。

   ```java
   interface A{
   }
   interface B{
   }
   class C implements B{
   }
   B b = new C();
   A a = (A)b;// 这样编译器也不报错，但是在运行时可能会出现ClassCastException异常
   
   // 若这样写，就没问题了
   interface D{
   }
   interface E{
   }
   interface F{
   }
   class G implements D,E,F{
       
   }
   D d = new G();
   E e = new G();
   F f = new G();
   E e2 = (E)d;// 这样写 没问题，因为d的对象是G，而G is a E。
   ```



### 继承和实现都存在

继承在前，实现在后   extends在前，implements在后

接口是一个可以插拔的东西，比如一个Flyable接口，如果不实现这个接口，就表明没有给你插翅膀，就表明你不能飞，如果实现了，就证明你可以飞

同一个接口，调用同一个fly()方法，最后的执行效果不同，因为实现接口的类不同，也就时说，将翅膀插在了不同的动物身上，方法重写的不同。



### 接口在开发中的作用

> 类似多态在开发中的作用

面向抽象编程，可以改成面向接口编程，有了接口就有了可插拔，可插拔就表示扩展力很强。

举例：去饭馆吃饭，这当中有接口么？

菜单就是接口（菜单上有一个抽象的照片，西红柿炒鸡蛋）

谁面向接口调用（顾客面向菜单点菜，调用接口）

谁负责实现这个接口（后台的厨师负责把西红柿鸡蛋做好，是接口的实现者）

这个接口有什么用呢？让“厨师”和“顾客”解耦合了，顾客不用找后厨，后厨不用找顾客，他们之间通过一个抽象的菜单进行沟通。



==凡是能够用`has a` 来描述的，统一以属性的方式存在。（若是自定义的数据类型，则可以理解为结构体变量）==

能够用`is a` 来描述的，可以进行继承。

接口没办法new对象，只能new子类，接口和多态一定是连在一起的。接口加上多态，才可以达到解耦合的目的。



#### 解耦合

接口可以解耦合，解开的是谁和谁的耦合？

任何一个接口都有调用者和实现者，接口可以将调用者和实现者解耦合。调用者面向接口调用，实现者面向接口实现。

若删掉Customer.java和Test.java，则剩余三个程序仍然可以编译通过；若删掉AmericanCook.java和ChinaCook.java和Test.java，则剩余的两个程序仍然可以编译通过。因为Customer之和FoodMenu接口发生关系，AmericanCook和ChinaCook也只和FoodMenu发生关系。

在实际开发中，项目经理可能将接口先定义好，接口的调用者Customer可能给一个团队去做，而AmericanCook和ChinaCook可能交给另一个团队去做，这样项目组的两个团队可以同时开始写代码，项目组开发效率马上提高了。    相当于把项目切成一块一块的，最后通过接口拼起来。

整个项目中最难的部分是接口的定义，定义接口的人是架构师，或者说是系统分析师，或者高级软件工程师，或者项目经理，他有丰富的开发经验

### 抽象类和接口有什么区别

> 只谈语法的区别

因为接口是完全抽象的，我们能不能让抽象类完全抽象？这个问题从项目中学习体会

1. 抽象类是半抽象的，接口是完全抽象的。
2. 抽象类中有构造方法，接口中没有构造方法
3. 接口和接口之间支持多继承，类和类之间只能单继承。
4. 一个类可以同时实现多个接口，一个抽象类只能继承一个类（单继承）
5. 接口中只允许出现常量和抽象方法。

提前透漏：一般接口使用的比抽象类多，抽象类使用的少

接口一般都是对行为的抽象。抽象类既可以抽象行为，又可以抽象数据。





# 多态

> 要有两个类，一个子类一个父类

## frank

一个对象变量可以指示多种实际类型的现象被称为多态。

运行时能够自动地选择调用哪个方法地现象称为动态绑定。



1. 父类new子类：向上转型（**子类new父类会报错**）

```java
HuaHu huaHu = new HuaMuLan;
// 替父从军
```



2. alt+enter， 强制类型转换，向下转型

> 如果要访问的方法是子类当中特有的，则必须要使用向下转型，不要随便做强制类型转换

```java
// 做回自己
HuaMuLan huaMuLan = (HuaMuLan)huaHu;
```

多态作用：实现多功能



## ==**老杜举例：**==

### 多态内容

代码可以这样写吗？

父类型的引用允许指向子类型的对象

```java
Animal a = new Bird(); // 子转向父，向上转型,自动类型转换
Cat c = new Animal(); // 父转向子，向下转型，强制类型转换，需要加强制类型转换符，但一般不这么说，因为自动和强制类型转换是指基本数据类型的
a.move();
// 此时编译时，调用Animal中的move方法，执行时调用的是Bird中的重写之后的move方法
```

注意三个问题：（可以继承需要考虑的问题）

1. Animal和Cat之间有继承关系吗？
2. Animal是父类，Cat是子类
3. Cat is a Animal，能不能说通？

a是一个父类型的引用，bird是一个子类型的对象

==**无论是向上转型还是向下转型，两种类型之间必须有继承关系，否则编译器报错**== 编译只检查类型错误（这句话不适用在接口方面，编译时不报错，但是在运行时该报错还是会报错）

什么是多态？  多种形态，多种状态

分析上面的`a.move();`

1. Java程序分为编译阶段和运行阶段。在编译阶段，对于编译器来说，编译器只知道a的类型是Animal，所以编译器在检查语法的时候，会去Animal.class字节码文件中找move()方法，找到了，绑定上move()方法，编译通过，静态绑定成功。（==**编译阶段属于静态绑定**==）

2. 运行阶段时，实际上在堆内存中创建的java对象是cat对象，所以move的时候，真正参与move的对象是一只猫，所以运行阶段会动态执行cat对象的move()方法，这个过程属于运行阶段绑定。（==**运行阶段的绑定属于动态绑定**==）

   多态表示多种形态：编译的时候是一种形态，执行的时候是一种形态。

只有**引用**和**类名**才能.

一个典型的会报错的操作

```java
Animal a = new Cat();
a.catchMouse();
```

报错的原因：编译器只知道a的类型是animal，去Animal.class文件中寻找catchMouse方法，没找到，报错

假设代码写到了这里，我非要用catchMouse()方法，怎么办？这个时候必须使用向下转型（强制类型转换）       ==**如果要访问的方法是子类当中特有的，则必须要使用向下转型**==

```java
Cat x = (Cat)a; // 因为a是Animal类，Animal与Cat之间存在继承关系，所以没报错
x.catchMouse(); // 就可以了
```

### 向下转型有风险吗

分析以下程序

```java
Animal a6 = new Bird();
Cat y = (Cat)a6; // 运行阶段会报错
y.catchMouse();
```

此代码编译阶段不会报错，但是在运行阶段，堆内存实际创建的对象是Bird对象，在实际运行过程中，拿着Bird对象转换成Cat对象就不行了，因为Bird和Cat之间没有继承关系。

运行时出现异常，这个异常和空指针异常一样非常重要，也非常经典

```java
java.lang.ClassCastException //类型转换异常
java.lang.NullPointerException //空指针异常
```

运气好的时候，强制类型转换成的类型和new的对象的类型恰好是一个类型，就可以使用

### 如何避免ClassCastException异常的发生

> 新的运算符 instanceof（运行阶段动态判断）

1. instanceof运算符可以在运行阶段动态地判断引用指向地对象的类型

2. instanceof的语法

   (引用 instanceof 类型)

3. instanceof运算符的运算结果只能是`true\false`

4. c是一个引用，c变量保存了内存地址指向了堆中的对象

   假设(c instanceof Cat) 为true表示：c引用指向的堆内存中的java对象是一个Cat

   假设(c instanceof Cat) 为false表示：c引用指向的堆内存中的java对象不是一个Cat

   ```java
   Animal a6 = new Bird();
   if(a6 instanceof Cat){ // 如果a6是一只猫，再进行强制类型转换
       Cat y = (Cat)a6;
       y.catchMouse;
   }
   // 养成这个好习惯，任何时候任何地点，对类型进行向下转型时，一定要使用instanceof运算符进行判断，这是java规范中要求的，这样可以很好地避免ClassCastException错误
   ```

### 疑问

肉眼可以观察到a到底是bird还是cat，我们为什么还要进行instanceof的判断呢？

原因：以后可能肉眼看不到

```java
public class Test03{
    public static void main(String[] args){ // main方法是程序员a负责编写
        
    }
}
class AnimalTest{
    public voidd test(Animal a){ // test方法是程序员B负责编写
           // 你写的这个方法别人会去调用
           // 别人调用的时候可能给你传过来一个Bird，也可能给你传过来一个Cat
           // 但是对于我来说，我不知道你调用的时候给我传过来一个什么
    }
}
```

## 多态在开发中有什么作用

> 降低程序的耦合度，提高程序的扩展力

主人一开始只喜欢养狗狗，喂养的方法为`feed(Dog d){}`,随着时间的推移，主人又喜欢养猫咪。==在实际的开发中这就表示客户产生了新的需求==。在不使用多态机制的前提下，目前我们只能在Master类中添加一个新的方法，（当然猫咪的新的对象是一定要生成的）。由于新的需求产生，我们不得不去修改Master类当中的方法，再加一个方法，参数为`feed(Cat c)}{}`,

思考：修改Master这个类，有什么问题？    在软件的扩展过程当中，修改的越少越好。修改的越多，系统的稳定性越难以保证，未知的风险就越多。==这里涉及到软件开发的七大原则==，其中最基本的原则是**`OCP(开闭原则)`**，对扩展开放，对修改关闭。 即在软件的扩展当中，修改的越少越好.

要考虑软件的扩展性---高手

例如在主人喂养宠物的类里，为了保证扩展性，应该在实参中传入父类，而不是单独写成Cat或者Dog写死了（相当于内存条和主板焊接在一起了），而是要写一个上层抽象类型（最好不要写具体的宠物类型，这样会影响程序的扩展性）

==**面向抽象编程**==



## 注意事项

1. 方法覆盖只是针对于方法，和属性无关

2. 私有方法无法覆盖

3. 构造方法不能被继承，所以构造方法也不能被覆盖

4. 方法覆盖只是针对于**实例方法**，**静态方法覆盖**没有意义，一般我们说静态方法不存在方法覆盖。我们不探讨。因为静态方法的执行不需要对象。

   因为静态方法和对象无关

   ```java
   // doSome是Animal中的静态方法，在子类Cat中进行了重写
   Animal a = new Cat();
   a.doSome();
   // 此时执行的还是Animal.doSome(),与实例中重写的方法无关
   ```

   



讲解：

1. 方法覆盖需要和多态机制联合起来使用才有意义。没有多态机制的话，方法覆盖可有可无。如果有新的需求，父类的方法无法满足子类的业务需求的时候，子类完全可以定义一个全新的方法。





# is a , has a, like a

`is a`  cat is a(n) Animal     继承关系

​		A extends B

`has a` I has a pen.  关联关系，通常以属性的形式存在

​		A{

 		B b;

}

`like a`  Cook is like a FoodMenu.（厨师像一个菜单一样，功能）  实现关系，通常是类实现接口    如：司机像导航

​		A implements B;







# java进阶

# API

相当于把C语言里的库，主要是给**客户**用的

javaAPI是给java开发人员用的，若有API，就应当有对应的API文档

相当于在开发过程中方便程序员操作的一些方法，他封装成了一个类，统称为API



## Object类中的方法

五种常用的方法

1. protected Object clone()
2. int hashCode()
3. boolean equals(Object obj)
4. String toString()
5. protected void finalize()

### toString()

```java
    public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
//默认输出该类的名称，一个@号，加该字符串的信息的内存地址的十六进制表示
//这不是我们想要的，所以要重写
```

建议每个类都重写此方法   重写规则：越简单越好

**注意**：输出引用的时候，会自动调用该引用的toString方法

### equals

初衷：利用equals方法判断两个**对象**是否相等     判断两个基本数据类型是否相等，可以直接使用==，但对象不能

但若是两个对象==，这时**判断的是两个对象的内存地址**是否相等，若是new的两个对象，则一定是false

```java
public boolean equals(Object obj) {
        return (this == obj);
    }
// 但在object中默认采用的是==判断两个java对象是否相等，不够用
// 所以还要重写
```

老祖宗的equals()方法不够用，子类当中要重写equals()

重写规则：自己定，主要看什么和什么相等时，表示两个对象相等。==**重写equals一定要彻底**==，每写一个类，都要重写equals方法。

总结：

1. 基本数据类型判断相等，使用==
2. 引用数据类型判断相等，使用equals()，如比较两个字符串是否相等，要调用equals()方法

如果一个类的equals方法重写了，那么hashCode方法必须重写

并且equals方法如果返回的是true，hashCode方法返回的值必须一样。





### finalize()

> 了解即可，非重点

```java
    //源代码
	protected void finalize() throws Throwable { }
}
```

1. 这个方法不需要程序员调用，JVM的垃圾回收器负责调用这个方法，程序员只负责重写就可以了。GC负责调用
2. finalize()方法的调用时机：当一个java对象即将被垃圾回收器回收（对象即将被释放）的时候，垃圾回收器负责调用finalize()方法
3. finalize()方法实际上是SUN公司位java程序员准备的一个时机，垃圾销毁时机，如果希望在对象销毁时机执行一段代码的话，这段代码要写到finalize()方法当中。



```java
Person p = new Person();
// 把Person对象变成垃圾
p = null;
// 或者再new一个新的对象给p
p = new Person();
```

项目开发中，有这样的业务需求：所有对象在jvm中被释放的时候，请记录一下对象被释放的时间点：记录的代码写到finalize()方法中。

当垃圾回收器不启动的时候，finalize()方法不调用。垃圾太少，或者时间没到，种种条件下，有可能不启动。多造点垃圾，垃圾数量达到一定程度之后，就会启动垃圾回收器。老杜for循环到10000000，造垃圾，JDK13才启动。

有一段代码可以建议垃圾回收器启动（可能不听话，还不启动）

```java
System.gc();// 建议启动垃圾回收器，只是建议，也可能不启动，是一个静态方法
```



### hashCode()

```java
public native int hashCode();
```

这个方法不是抽象方法，带有native关键字，底层调用C++程序。

hashCode()方法返回的是哈希码，**实际上就是一个java对象的内存地址**，经过哈希算法，得出的一个值，所以hashCode()方法的执行结果可以等同看作一个java对象的内存地址。



### clone()

```java
protected native Object clone() throws CloneNotSupportedException;
```

深克隆，浅克隆？



## 匿名内部类

内部类：在类的内部又定义了一个新的类

new一个接口，或者说是一个抽象类，后面加一个大括号，里面要实现抽象类中所有的方法。一般在构造方法中使用。



## 数组

> 是一种引用数据类型

数组是一种容器，放数据的，是一种数据的集合，其中可以存储基本数据类型的数据，也可以存储引用数据类型，数组是存储在堆当中的。



## Scanner

String: next返回一个不带空格的字符串

nextLine: 返回一行字符串



int:  nextInt()

nextInt(radix,进制，默认为10进值)



## Number

数字的父类，Byte,Integer,Double, Float,Long,Short 都是Number类型的子类



## Math

其中的方法定义基本都是static，方便使用



## String

其中只有一个静态方法：

```java
String.valueOf();//将不是字符串的东西转换成字符串
//底层调用toString()方法
System.out.println();//打印输出的东西都是字符串，输出任何数据的时候，都会先转换成字符串
```



## 八个包装类

八种包装类属于引用数据类型，父类是Object

基本数据类型不能直接与包装数据类型（引用数据类型）进行大小比较



### Number

#### 装箱

构造方法进行包装，把基本数据类型抓换为引用数据类型，

```java
Integer i = new Integer(100);
Integer y = new Integer("100");//String 也能转换成Integer
```

例如，Integer中有两个构造方法

```java
Integer(int value);
Integer(String value);
```



#### 拆箱

将引用数据类型转换成基本数据类型

```java
intValue();
floatValue();
shortValue();
doubleValue();
longValue();
//抽象类Number中的抽象方法，拆箱方法

```

#### 自动装箱和自动拆箱

在jdk5之后，支持了

自动装箱int->Integer

自动拆箱Integer->int

有了自动装箱，拆箱之后，Number类中的方法就用不到了

**==永远比较的是对象的内存地址**，不会触发自动拆箱机制，之后加减乘除运算才会



##### 一段神奇的代码

```java
Integer a = 128;
Integer b = 128;
System.out.println(a == b);//false

Integer x = 127;
Integer y = 127;
System.out.println(x == y);//true
```

java中为了提高程序的执行效率，将-128到127之间所有的包装对象提前创建好，(在类加载阶段)放到方法区的**整数型常量池**中的（整数型常量池中已经有了很多对象），目的是，若用到这个区间的数据，不需要再new了，直接从整数型常量池中取出来。故`x`中保存的内存地址和`y`中保存的内存地址是同一个。



池就是缓存，优点效率高，缺点占用内存空间







# I/O流

## 流的四大家族

java.io.InputStream 字节输入流

java.io.OutputStream 字节输出流

java.io.Reader 字符输入流

java.io.Writer 字符输出流

字节流是万能的，字符流只能读取普通文本txt

## 实现的接口

所有的流都实现了java.io.Closeable接口，都有close()方法

但是只有输出流实现了java.io.Flushable接口，才有flush() 方法    养成一个好习惯，输出流在最终输出之后，一定要记得flush()刷新一下，表示将这个管道中剩余未输出的数据强行输出完，清空管道！



需要掌握的流

```java
// 文件专属
java.io.FileInputstream;
java.io.Fileoutputstream;
java.io.FileReader;
java.io.FileWriter;

//转换流，将字节流抓换成字符流
java.io.InputstreanReader;
java.io.outputstreamWriter;

//缓冲流专属
java.io.BufferedReader;
java.io.Bufferedwriter;
java.io.BufferedInputstream;
java.io.BufferedOutputstream;

//数据流专属
java.io.DataInputstream;
java.io.DataOutputstream;

//标准输出流
java.io.Printwriter;
java.io.Printstream;

// 对象专属流
java.io.objectInputstream;
java.io.objectoutputstream;

```



## FileInputStream

### read

1. 创建文件字节流对象

   ```java
   FileInputStream fis = new FileInputStream(文件绝对路径);
   //记得加try  catch
   //该文件中存了abcdef
   ```

2. 关闭的时候记得判断一下是否为空，若为空，则不需要关闭

3. 循环读取文件数据

   ```java
   while(true){
       int readDate = fis.read();
       if(readDate==-1){
           break;
       }
       System.out.println(readData);
   }
   
   //改造while循环
   int readData = 0;
   while((readData = fis.read())!=-1){
       System.out.println(readData);
   }
   //这样读效率太低，与硬盘交互的时间太多
   
   //一次最多读取数组.length 个字节
   byte[] bytes = new byte[4];//准备一个四个长度的byte数组，一次最多读取4个字节
   int readCount = fis.read(bytes);// 这个方法返回的是读到的字节的数量，不是字节本身
   System.out.println(new String(bytes));//使用构造方法把bytes数组转换成String
   //但这种方法是把字节数组bytes全部都转换成字符串，但是不应该全部都转，而应该是读到多少个转多少个
   System.out.println(new String(bytes,0,readCount));//数组名，起始位置，读取的长度
   
   
   readCount = fis.read(bytes);//第二次再读取，返回的是2，而且会把之前读的ab覆盖掉
   System.out.println(new String(bytes,0,readCount));//数组名，起始位置，读取的长度
   
   
   readCount = fis.read(bytes);//若第三次读取，一个字节都没有读到，返回-1
   System.out.println(new String(bytes,0,readCount));//数组名，起始位置，读取的长度
   ```

4. 接下来用while循环改造FileInputStream最终版(在idea中要加异常)

   ```java
   FileInputStream fis = new FileInputStream(文件路径名);
   byte[] bytes = new byte[4];
   while(true){
       int readCount = fis.read(bytes);
       if(readCount == -1) break;
       System.out.print(new String(bytes,0,readCount));
   }//这样文件中有什么都可以读出来，换行和回车也可以
   //改进while循环
   
   int readCount = 0;
   while((readCount = fis.read(bytes))!=-1){
       System.out.print(new String(bytes,0,readCount));
   }
   ```

   

5. 若使用相对路径，则工程project当前路径下的**根**，就是默认的当前路径



### available

> 返回流当中剩余的没有读到的字节数量

可以在一开始就fis.available()返回流当中的字节数量，然后创建一个等同大小的字节数组，这样就可以不用循环了。

```java
FileInputStream fis = new FileInputStream(文件路径);
byte[] bytes = new byte[fis.available()];
int readCount = fis.read(bytes);
System.out.println(new String(bytes));
//这种方式不太适合太大的文件，因为bytes数组不能太大
```



### skip

```java
fis.skip(要跳过的字节数);
```





## FileOutputStream

写完之后一定记得要刷新

```java
fos.flush();
```



### write()

参数可以传byte数组，也可以传byte数组的开始下标和需要读取的长度

没有文件会新建，并且会把原文件清空。

```java
FileOutputStream fos = new FileOutputStream(文件路径,true/false);//后一个参数为append,若为true，则以追加到方式在文件末尾写入，不会清空之前写过的东西
byte[] bytes = {97,98,99,100};
fos.write(bytes);
fos.write(bytes,0,2);
fos.flush();
```



# 集合

## 集合中存储

集合中存储对象的内存地址，也可以说存储引用

集合**不能存基本数据类型**，也不能存**对象**



## 不同集合对应不同的数据结构



使用不同的集合等同于使用不同的数据结构，往不同的集合中放置元素相当于往不同的数据结构中放置元素

使用不同的数据结构时，只需要new不同的对象即可

```java
new ArrayList();//创建一个集合，底层是数组，非线程安全的
new Vector();// 底层是数组，线程安全的，效率比较低，所有的方法都有synchronized，现在保证线程安全有别的方案，所以vector使用较少
new LinkList():// 创建一个集合，底层是链表
```



## java.util.*

所有的集合类和集合接口，都在这个包下



## 集合分为两大类

- 单个方式存储元素：超级父接口：java.util.Collection
  一个一个挨着存
- 以键值对的方式存储元素：超级父接口java.util.Map;
  一对一对存，key  value



## 集合类之间的转换：通过构造方法

特别的，Map转换成Set集合通过keySet方法





- add：与迭代器的位置有关，加入位置在迭代器的左侧
- remove：与迭代器的状态有关，删除的元素是迭代器上一次访问的对象，该方法必须紧跟在访问一个对象之后执行，不能连续两次执行remove方法

add方法只依赖于迭代器的位置，而remove方法依赖于迭代器的状态。



如果迭代器发现它的集合被另一个迭代器修改了，就会抛出异常CurrentModificationException, 要遵循以下简单规则：可以根据需要给容器附加许多迭代器，但是这些迭代器只能读取列表。另外再单独附加一个既能读又能写的迭代器。





## 集合的继承关系

### Collection接口的实现关系

![image-20210817093244873](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210817093244873.png)



放在SortSet集合中的元素可以自动排序，无序不可重复

List有序可重复

### Map接口继承关系

![image-20210817100445027](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210817100445027.png)    



最上面的是Map



### 总结：

- ArrayList：底层是数组
- LinkedList：底层是双向链表
- Vector：底层是数组，线程安全的，效率较低，使用较少
- HashSet：底层是HashMap，放到HashSet集合中的元素等同于放到HashMap集合key部分了
- TreeSet：底层是TreeMap，放到TreeSet集合中的元素等同于放到TreeMap集合key部分了
- HashMap：底层是哈希表
- Hashtable：底层也是哈希表，只不过是线程安全的，效率较低，使用较少
- Properties：是线程安全的，并且key和value只能存储字符串String
- TreeMap：底层是二叉树，TreeMap集合的key可以自动按照大小顺序排序



- List集合存储元素的特点

  - 有序可重复
  - 无序，存进去的顺序和取出的顺序相同，每一个元素都有下标
  - 可重复，存进去1，可以再存储一个1

- Set集合存储元素的特点

  - 无序不可重复
  - 无序，存进去的顺序和取出来的顺序不一定相同，另外Set集合中元素没有下标
  - 不可重复，存进去1，就不能再存储1了

- SortedSet集合存储元素特点

  - 首先是无序不可重复的，但是SortedSet集合中的元素是可排序的
  - 无序，存进去的顺序和取出来的顺序不一定相同，另外Set集合中元素没有下标
  - 不可重复，存进去1，就不能再存储1了

- Map集合的key，就是一个Set集合

  往Set集合中放数据，实际上放到了Map集合的key部分



## Collection

没有使用泛型之前，Collection中可以存储Object的所有子类型，使用了泛型之后，Collection 中只能存储某一个特定的类型

```java
public class assembleTest01 {
    public static void main(String[] args) {
        //Collection c = new Collection();// 接口不能new对象
        // 多态
        Collection c = new ArrayList();
        // 测试Collection接口中的常用方法
        c.add(1200); // 自动装箱，实际上是放进去了一个对象的内存地址。Integer x = new Integer(1200); 放进去的是x，是内存地址
        c.add(3.14);
        c.add("sdfs");
        c.add(new String());
        Iterator it = c.iterator();
        while(it.hasNext()){
            System.out.println(it.next());
        }

        Collection c2 = new HashSet();
        c2.add(100);
        c2.add(200);
        c2.add(300);
        c2.add(300);
        c2.add(300);
        c2.add(50);
        c2.add(60);
        Iterator it2 = c2.iterator();
        while(it2.hasNext()){
            Object obj2 = it2.next();
            System.out.println(obj2);
        }
    }
}
```

### iterator

存进去是什么类型，输出还是什么类型，

HashSet无序不可重复，存进去和取出的数据不一定相同。存进去100，不能再存储100

#### 迭代器的通用代码

```java
        Iterator it2 = c2.iterator();
        while(it2.hasNext()){
            Object obj2 = it2.next();
            System.out.println(obj2);
        }
```

**集合结构只要发生改变，迭代器就要重新获取**，好像一个**快照** 



#### remove

在迭代集合元素的过程中，不能调用集合对象的c2.remove方法，否则集合结构改变，会出现异常
而应该使用迭代器的remove方法

it2.remove();

获取的迭代器对象，迭代器用来遍历集合，此时相当于对当前集合的状态拍了一个快照，迭代器迭代的时候会参照这个快照进行迭代。每次迭代的时候会与快照进行比较，若不一样，则报异常。

使用it2.remove()  迭代器的remove方法，也会删除快照中的元素



### contains方法深入理解

判断包含不包含，底层会调用**equals方法**，不管是不是一个对象，只要equals方法返回true，就表明包含这个元素

放在集合中的类型，使用contains方法时，要重写equals方法，否则会调用Object中的equals方法，比较的是内存地址，不符合我们的预期。



## List

是Collection的子接口，有其特定方法

```java
void add(int index, E element);
E get(int index);
int indexOf(Object o);
```

## 泛型

若使用泛型，则next方法返回一个<E>中表示的类型，后续过程中不用强转了，否则next返回类型为object类型

运行阶段泛型没用，泛型只是在编译阶段起作用

好处：

1. 集合中存储的元素类型统一了
2. 从集合中去除的元素类型是泛型指定的类型，不需要进行大量的强制类型转换（向下转型）

缺点：导致集合中存储的元素缺乏多样性

大多数业务中，集合中元素的类型是统一的，所以泛型这种特性被广泛应用



若只需要调用Animal中的方法，则泛型的优势显现出来，若需要调用cat，bird类中特有的方法，还是避免不了向下转型。





## Set

**HashSet和TreeSet都是无序不可重复**，无序指的是，存进去的顺序和取出的顺序不同，没有下标

**所以HashSet只是不保证有序，并不是保证无序**

允许使用null元素，但是只能有一个null元素

TreeSet自动排序,想改变排序规则，在构造方法中传入比较器

```java
Set<String> set = new TreeSet<>(new Comparetor<String>(){
    public int compare(String o1,String o2){
        return o2-o1;//此规则为逆序
    }
});//这里使用了匿名内部类，直接new一个接口
Comparable接口实现compareTo方法;
Comparetor接口，比较器实现compare方法
```

**比较器也要有泛型**

HashSet不排序



## Map

java.utiL.Map接口中常用的方法:
1、Map和coLlection没有继承关系。
2、Map集合以key和value的方式存储数据:键值对
key和value都是引用数据类型。
key和vaLue都是存储对象的内存地址。
key起到主导的地位，value是key的一个附属品。



### Map接口中常用方法:

```java
void clear()
boolean containsKey( object key );
booLean containsValue(object value);
V get(object key );//通过key取value
booLean isEmpty();
Set<K> keySet();//可以拿到所有的key，得到一个Set集合
V put(K key, v value);
V remove( object key )int size();
collection<V> values( );
Set<Map.Entry<K, V>> entrySet();//调用这个方法可以把一个Map集合转换成一个Set集合，Set集合中元素的类型是Map.Entry
```



### 遍历Map集合

注意Map没有迭代器iterator的概念，Collection中才有iterator

1. 拿到所有的key（这是一个set集合），遍历key，通过key获取value

   ```java
   Map<String,Integer> map = new HashMap<>();
   Set<String> keys = map.keySet();
   for(String key:keys){
       key + map.get(s);
   }
   
   // 或者将Map集合转换成Set集合
   Set<Map.Entry<String,Integer>> entrys = map.entrySet();//nodes
   for(Map.Entry<String,Integer> entry:entrys) {
       entry.getKey()   +   entry.getValue();
   }
   
   ```

   

2. 把Map集合直接全部转换成set集合

   ```java
   Set<Map.Entry<Integer,String>> set = map.entrySet();
   ```

   这个Map.entrySet类中的对象叫Node对象，其中有key和value属性(但是还有别的属性)

   遍历Set集合，每一次取出一个Node

   ```java
   Iterator<Map.Entry<Integer,String>> it2 = set.iterator();
   while(it2.hasNext()){
       Map.Entry<Integer,String> node = it2.next();
       Integer key = node.getKey();
       String value = node.getValue();
       System.out.println(key + "=" + value);
   }
   
   
   //foreach
   foreach(Set,Entry<Integer,String> node : set){
       System.out.println(node.getKey() + "=" + node.getValue());
   }
   ```

第二种方法效率较高，因为第一种方法使用了hash映射



### HashSet

HashSet初始化容量是16，初始化容量必须是2的次方，扩容后是原容量的二倍

允许使用null元素，但是只能有一个null元素



### HashMap

> 无序不可重复

HashMap集合默认初始化容量为16，若不是16，也必须是2的次方

#### map.put(k,v)实现原理:

第一步:先将k v封装到Node对象当中。
第二步:底层会调用k的hashCode0方法得出hash值，然后通过哈希函数/哈希算法，将hash值转换成数组的下标，下标位置上如果没有任何元素，就把Node添加到这个位置上了。如果说下标对应的位置上有链表，此时会拿着k和链表上每一个节点中的k进行equals ，如果所有的equals方法返回都是false，那么这个新节点将会被添加到链表的末尾。如果其中有一个equals返回了true，那么这个节点的value将会被**覆盖**。

#### v = map.get(k)实现原理∶

先调用k的hasHlCode(方法得出哈希值，通过哈希算法转换成数组下标，通过数组下标快速定位到某个位置上，如果这个位置上什么也没有，返回null。如果这个位置上有单向链表，那么会拿着参数k和单向链表上的每个节点中的k进行equals ,如果所有equals方法返回false ，那么get方法返回null，只要其中有一个节点的k和参数k equals的时候返回true，那么此时这个节点的value就是我们要找的value , get方法最终返回这个要找的value。

**注意**﹔同—个单向链表上所有节点的hash相同,因为他们的数组下标是样的。
但同—个链表上k和k的equals方法肯定返回的是false ,都不相等。



#### HashMap集合的key部分特点:

无序，不可重复。
为什么无序?因为不一定挂到哪个单向链表上。
不可重复是怎么保证的? equals方法来保证HashMap集合的key不可重复。如果key重复了，value会覆盖。
放在HashMap集合key部分的元素其实就是故到HashSet集合中了。
所以HashSet集合中的元素也需要同时重写hashCode( )+equals()方法。



#### 哈希表HashMap使用不当时无法发挥性能!

假设将所有的hashCode()方法返回值固定为某个值，那么会导致底层哈希表变成了纯单向链表。这种情况我们成为∶散列分布不均匀。
什么是散列分布均匀?
假设有100个元素，10个单向链表，那么每个单向链表上有10个节点，这是最好的，是散列分布均与的。
假设将所有的hashCode()方法返回值都设定为不一样的值，可以吗，有什么问题?
不行，因为这样的话导致底层哈希表就成为一维数组了，没有链表的概念了。也是散列分布不均匀。
散列分布均匀需要你重写hashCode()方法时有一定的技巧。



向Map集合中存，以及从Nap集合中取，都是**先**调用key的hashCode方法，然后**再**调用equals方法!equals方法有可能调用，也有可能不调用。所以必须要同时重写hashcode方法和equals方法

如果一个类的equals方法重写了，hashcode方法也必须重写。两个对象如果equals方法返回true，则hashcode方法的返回值应该相同



#### HashMap集合的key值可以为null

也相当于一个key值，但是Hashtable的key值和value值都不能为空

Hashtable初始化容量11，hashtable扩容 原始容量*2+1



### TreeMap可以按key值自动排序

对自定义的类型来说，TreeSet可以排序吗?
以下程序中对于Person类型来说，无法排序。因为没有指定Person对象之间的比较规则。谁大谁小并没有说明啊。
以下程序运行的时候出现了这个异常:
java.Lang.CLasscastException:
cLass com. bjpowernode .javase.colLection .Personcannot be cast to class java.Lang . ComparabLe
出现这个异常的原因是:
Person类没有实现java .Lang. Comparable接口。



#### TreeSet集合中存放的类要实现comparable接口（可排序的第一种方式）

若想要放在TreeSet集合中的元素是可排序的，则该元素所属的类（若是自定义的）要implement Comparable接口，并且重写compareTo方法，在compareTo方法中实现比较规则，才能进行比较，注意，新加入的元素为c，TreeSet集合中本来就有的元素分别为c1,c2,c3,c4，则c分别与c1,c2,c3,c4进行比较，即c.compareTo(c1),c.compareTo(c2),c.compareTo(c3),c.compareTo(c4)，

比如，若比较规则是按照Person的年龄来排序，则

```java
class Person implements Comparable<Person>{
    public int compareTo(Person p){
        return this.age-p.age;//升序排列
    }
}
```

TreeSet集合/TreeMap集合采用的是:中序遍历方式。
lterator迭代器采用的是中序遍历方式。
左根右。



#### TreeSet集合中元素可排序的第二种方式:使用比较器的方式

比较器实现java.util .Comparator接口。(Comparable是java.lang包下的。Comparator是java.util包下的

在创建TreeSet集合的时候，往构造方法中传一个比较器（new 一个比较器对象）

也可以采用匿名内部类的方式，此时可以new接口





#### 最终的结论:

放到TreeSet或者TreeMap集合key部分的元素要想做到排序,包括两种方式:
第一种:放在集合中的元素实现java .lang.Comparable接口。
第二种:在构造TreeSet或者TreeNap集合的时候给它传一个比较器对象。
Comparable和Comparator怎么选择呢?
当比较规则不会发生改变的时候，或者说当比较规则只有1个的时候，建议实现comparable接口。如果比较规则有多个，并且需要多个比较规则之间频繁切换，建议使用Comparator接口。
Comparator接口的设计符合oCP原则。|





## Collections工具类

方法：

```java
Collections.synchronizedList(list);
collections.sort(list) ;

```

ArrayList集合不是线程安全的，变成线程安全的

```java
List<String> list = new ArrayList<>();
Collections.synchronizedList(list);
```

若想对Set集合进行排序，则必须要将Set集合转变为List集合，利用构造方法转换，才能使用Collections工具类

```java
Set<String> set = new HashSet<>();
List<String> myList = new ArrayList<>(set);//把set集合传进来，封装成一个list集合
Collections.sort(myList);
```



## 遍历方式总结

1. List集合有下标，可以使用get(i)来取元素

2. 采用迭代器的方式
   若想利用迭代器采用从后往前的方式遍历，由于迭代器创建时默认是在开始，所以要先把迭代器循环到最后一个位置，什么操作也不做，然后再往前迭代，进行操作，实现逆序遍历

   ```java
   Iterator<String> it = list.iterator();
   while(it.hasNext());//list.next()
   while(it.hasPrevious){
       //dosome...
       // list.previous()
   }
   ```

   

3. 采用foreach







## 类型自动推断机制





# 多线程

**进程有独立的地址空间**，一个进程崩溃后，在保护模式下不会对别的进程产生影响，而线程只是一个进程中的不同执行路径。线程有自己的堆栈和局部变量，拥有独立的执行序列。**但线程之间没有单独的地址空间**，一个线程死掉就相当于整个进程死掉。所以多进程的程序要比多线程的程序健壮。     但在进程切换时，花费资源较大

**但对于一些要求同时进行并且又要共享某些变量的并发操作，只能用线程，不能用进程。**

多个线程共享内存



1. **简而言之,一个程序至少有一个进程,一个进程至少有一个线程.**

2.  线程的划分尺度小于进程，使得多线程程序的并发性高。

3. 另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。

4. 线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。**但是线程不能够独立执行，**必须依存在应用程序中，由应用程序提供多个线程执行控制。

5. 从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。**这就是进程和线程的重要区别。**



==多任务操作系统的原理==

多任务操作系统(如Windows)的基本原理是:操作系统将CPU的时间片分配给多个线程,每个线程在操作系统指定的时间片内完成(注意,这里的多个线程是分属于不同进程的).操作系统不断的从一个线程的执行切换到另一个线程的执行,如此往复,宏观上看来,就好像是多个线程在一起执行.由于这多个线程分属于不同的进程,因此在我们看来,就好像是多个进程在同时执行,这样就实现了多任务.

注意并发与并行的区别 ，并发是分时间片执行

假设一个应用程序占据一个进程，对于一个应用程序的某个共享变量操作。



## 多线程操作

使用Thread类

### 实现线程的第一种方式

自己创建一个线程，创建一个类，继承Thread类，并重写run方法

定义线程类，创建线程对象，启动线程

![image-20210728121133157](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210728121133157.png)

主函数也相当于一个线程，主线程

调用start方法，默认执行run方法

run与start的区别：

- start()方法的任务是开辟一个新的栈空间，称为分支栈，只要开完这个方法就结束，线程就启动成功了。然后由jvm直接自动调度run()方法，并且run方法在分支栈的栈底部（压栈）。

  此时，run方法在分支栈的栈底部，main方法在主栈的栈底部，run和main是平级的。

- run()方法是一直压栈，不会启动线程，不会分配新的分支栈（这种方式就是单线程）

### 第二种方式

编写一个类，实现java.lang.Runnable接口，实现run方法

```java
// 创建一个可运行的对象
myThread mythread = new myThread();
//将可运行的对象封装成一个线程对象
Thread t = new Thread(mythread);
// 启动线程
t.start();

public class myThread implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 999; i++) {
            System.out.println("fenzhi....thread...");
        }
    }
}
```



### 第三种方式

> 实现Callable接口，JDK8新特性

这种方式实现线程可以获取线程的返回值

之前讲解的那两种方式无法获得线程的返回值，因为run方法返回void

```java
package com.google;

import java.util.concurrent.Callable;
import java.util.concurrent.FutureTask;

public class ThreadTest05 {
    public static void main(String[] args) throws Exception {
        // 第一步创建一个“未来任务对象”
        FutureTask task = new FutureTask(new Callable() {
            @Override
            public Object call() throws Exception {

                System.out.println("call....begin");
                Thread.sleep(1000 * 5);
                System.out.println("call....end");
                int a = 100;
                int b = 200;
                return a + b;
            }
        });

        // 创建线程对象
        Thread t = new Thread(task);

        // 启动线程
        t.start();

        // 在主线程中获取t线程的返回结果
        // get方法的执行会导致当前线程阻塞
        Object obj = task.get();

        // main方法这里的程序想要执行必须等待get()方法的结束
        // 而get()方法可能需要很久、因为get()方法只为了拿另一个线程的执行结果
        // 而另一个线程的执行是需要时间的
        System.out.println("hello world");

    }
}

```



## 线程的生命周期

五个状态

![image-20210728151754255](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210728151754255.png)



## 获取线程对象和名字

1. 获取当前线程？

   new出来一个myThread extends Thread

   **static** Thread currentThread()   这是一个静态方法

   ```java
   Thread t = Thread.currentThread();//这个代码出现在哪，当前线程就是啥。代码出现在main方法中，当前线程就是主线程
   ```

   

2. 设置线程的名字？

   ```java
   myThread t = new myThread();
   t.setName("...");
   ```

3. 获取线程的名字

   ```java
   t.getName();
   ```

   线程默认的名字

   Thread-0

   Thread-1

   Thread-2

   ...

## sleep方法

让当前线程休眠

1. **静态方法** Thread.sleep(1000)

   跟对象没关系，即使是这样

   ```java
   Thread t = new Thread();
   t.sleep();//即使用引用去调，最终还是转化为类名调用
   ```

   还是跟对象t没有关系，只是让当前线程进入休眠状态

2. 参数是毫秒

3. 作用：让当前线程进入休眠，进入“阻塞状态”，放弃占有的CPU时间片，让给其他线程使用。

   这行代码出现在A线程中，A线程就会进入休眠。

4. Thread.sleep()方法，可以做到这种效果：

   间隔特定的时间，去执行一段特定的代码，每隔多久执行一次。



#### 中止线程的睡眠？

```java
t.interrupt();//利用的是异常机制
```

#### 强行中止线程的执行

```java
t.stop()//已过时，不推荐，相当于任务管理器中的结束进程，可能丢失数据
```

#### 合理中止线程的执行

myThread类创建一个myThread对象，在myThread类中增加一个布尔类型的属性run=true，for循环时，if(run),再执行后面的语句

什么时候想中止，就在main方法中将myThread.run改为false即可。



## 线程调度

### 常见的线程调度模型

1. 抢占式调度模型

   哪个线程的优先级比较高，抢到的CPU时间片的概率就要高一些，java采用的就是这个抢占式。

2. 均分式调度模型

   平均分配cpu时间片，每个线程占有的cpu时间片长度一样，有一些编程语言采用的是这个



### java中提供的与线程调度有关的方法

> 优先级，yield让位，join合并

```java
void setPriority(int newPriority);// 设置线程的优先级，对线程对象设置优先级

int getPriority(int newPriority); //获取线程的优先级

static void yield(); // 让位方法，暂停当前正在执行的线程对象，并执行其他线程
// yield方法不是阻塞方法，让当前线程让位，让给其他线程使用，yield方法的执行会让当前线程从运行状态回到就绪状态。   让位，回到就绪状态之后，可能再次抢到时间片。
```

最高优先级是10，最低优先级是1，默认优先级是5

==优先级比较高的获取CPU时间片可能会多一些（但也不全完是）==，指的是处于运行状态的时间多一些，不是指抢占执行权的概率大一些。



```java
void join();// 合并线程，实例方法
// 不是两个栈合并成一个栈了，而是两个栈之间发生了等待关系。

class MyThread1 extends Thread{
    public void doSome(){
        MyThread2 t = new MyThread2();
        t.join(); // 当前线程进入阻塞，t线程执行，直到t线程结束，当前线程才可以开始执行，插队，加入了我们
    }
}
class MyThread2 extends Thread{
    
}
```



## 线程安全问题

关于多线程并发环境下，数据的安全问题

为什么这个是重点?   因为之前的写线程的程序，在服务器中已经会自动实现。以后在开发中，我们的项目都是运行在服务器中，而服务器已经将线程的定义，线程对象的创建，线程的启动等，都已经实现完了。这些代码我们都不需要编写。

**最重要的是，我们要知道，我编写的程序需要放到一个多线程的环境下运行，我更需要关注的是这些数据在多线程并发的环境下是否是安全的。**



### 什么时候会发生线程安全问题？

例子：多线程并发对同一个账户进行取款。

三个条件：

1. 多线程并发
2. 有共享数据
3. 共享数据有修改的行为。

满足这三个条件就会存在线程安全问题。



### 如何解决线程安全问题？

线程排队执行，不能并发。用排队执行。这种机制被称为“**线程同步机制**”。就是线程排队。

线程同步机制会牺牲一部分效率，数据安全第一位。



### 同步编程模型

同步就是排队

### 异步编程模型

异步就是并发

线程t1和线程t2，各自执行各自的，t1不管t2，t2不管t1，谁也不需要等谁，其实就是多线程并发，效率较高





## lock类

可以替代synchronized的东西,  叫同步锁

即synchronized操作的是对象，ReentrantLock操作的是线程

```java
Lock reentrantLock = new ReentrantLock();
// 在本应该synchronized的地方，用大括号括住的地方，使用
reentrantLock.lock();
//...
reentrantLock.unlock();
```



### synchronized线程同步机制

```java
synchronized(/*写需要排队的线程的共享对象*/){ // 括号里面只要是共享对象就行
    // 线程同步代码块
}
// synchronized 后面小括号中传的这个“数据”是相当关键的。这个数据必须是多线程共享的数据，才能达到多线程排队的目的。

synchronized(){
    double before = this.getBalance();
    double after = before - money;
    try{
        Thread.sleep(1000);
    } catch(InterruptedException e){
        e.printStackTrace();
    }
    this.setBalance(after);
}
```

()中写什么，那要看你想让哪些线程同步。

假设t1,t2,t3,t4,t5有五个线程

你只希望t1 t2 t3排队，t4 t5不需要排队，怎么办？

你一定要在()中写一个t1 t2 t3共享的对象，而这个对象对于t4 t5来说不是共享的

而对于银行账户存款这个例子，银行账户是共享的，也就是==this==是共享的。



在java中，任何一个对象都有一把锁，其实这把锁就是一个标记。100个对象100把锁。

以下代码的执行原理：

```java
synchronized (this){
            // 获得现在余额
            double before = this.getBalance();
            // 取钱
            double after = before - money;
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            // 保存剩余余额
            this.setBalance(after);
        }
```

1. 假设t1 t2线程并发，开始执行以下代码的时候，肯定有一个先一个后。
2. 假设t1先执行了，遇到了synchronized，这个时候自动找到“后面共享对象“的对象锁，找到之后，并占有这把锁，然后执行同步代码块中的程序。在程序执行过程中一直都是占有这把锁的。直到同步代码块代码结束，这把锁才会释放。
3. 假设t1已经占有了这把锁，此时t2也遇到了synchorinized关键字，也会去占有后面共享对象的这把锁，结果这把锁被t1占有，t2只能在同步代码块外面等待t1的结束，直到t1把同步代码块执行结束了，t1会归还这把锁，此时t2终于等到这把锁。t2占有这把锁之后，进入同步代码块执行程序。

这样就达到了线程排队执行。

这里需要注意的是，这个共享对象一定要选好了。这个共享对象一定是你需要排队执行的线程所共享的。

线程进入锁池找共享对象的对象锁的时候，会释放之前占有的cpu时间片

1. 没找到，就在锁池(lockpool)中等待
2. 找到了，会进入就绪状态继续抢夺cpu时间片

进入锁池，可以理解为一种阻塞状态。



### java三大变量中，局部变量不共享

> 局部变量和常量不会有线程安全问题（常量不会变），成员变量会有线程安全问题

实例变量：在堆中  堆区只有一个

静态变量：在方法区   方法区只有一个

局部变量：在栈中

局部变量永远不会存在线程安全问题，因为局部变量在栈中，所以局部变量永远都不会共享。实例变量在堆中，堆只有一个，静态变量在方法区中，方法区只有一个，堆和方法区是线程共享的，所以可能存在线程安全问题。

上面的是在withdraw方法中使用synchronized方法，下面的是直接把withdraw方法synchronized起来，扩大了同步范围。

```java
synchronized(act){
    act.withdraw(money);
}// 这样效率更低了
```



### synchronized出现在实例方法上，锁的一定是this

```java
public synchronized void withdraw(double money){
    
}
```

缺点：

1. 锁的一定是this，没得挑，只能是this，不能是其他的对象了，所以这种方式不灵活。
2. synchronized出现在方法体上，表示整个方法体都要同步，可能会无故扩大同步的范围，导致程序执行效率降低，所以这种方式不常用。

优点：

代码写的少，节俭了。如果共享的对象就是this，而且整个方法体都需要同步，推荐使用这种方法



如果使用局部变量，建议使用StringBuilder，局部变量不存在线程安全问题，StringBuffer效率比较低。

ArrayList是非线程安全的。

Vector是线程安全的

HashMap HashSet是非线程安全的

Hashtable是线程安全的





### 总结：synchronized有三种写法

1. ```java
   synchronized(线程共享对象){
       同步代码块;
   }
   ```

2. ```java
   在实例方法上使用synchronized，表示共享对象一定是this
       并且同步代码块是整个方法体。
   ```

3. 在静态方法上使用synchronized，表示找类锁，类锁永远只有一把，就算创建了100个对象，那类锁也只有一把。类锁是为了保证静态变量的安全。



上面讲的都是**排他锁**，后面还会有互斥锁。



### 死锁

不出现异常，也不出现错误，程序一直僵持在那里，这种错误最难调试。

synchronized在开发中最好不要嵌套使用，一不小心就会导致死锁现象的发生。

死锁的代码：

```java
public class DeadLock {
    public static void main(String[] args) {
        Object o1 = new Object();
        Object o2 = new Object();
        MyThread1 MyThread1 = new MyThread1(o1,o2);
        MyThread2 MyThread2 = new MyThread2(o1,o2);

        MyThread1.start();
        MyThread2.start();
    }
}


class MyThread1 extends Thread {
    Object o1;
    Object o2;

    public MyThread1(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }
    public void run(){
        synchronized (o1){
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o2){

            }
        }
    }
}

class MyThread2 extends Thread {
    Object o1;
    Object o2;

    public MyThread2(Object o1, Object o2) {
        this.o1 = o1;
        this.o2 = o2;
    }
    public void run(){
        synchronized (o2){
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            synchronized (o1){

            }
        }
    }
}
```



### 开发中如何解决线程安全问题

是一上来就选择线程同步吗？

不是，synchronized会让程序的执行效率降低，用户体验不好，系统的用户吞吐量（并发量）降低，在不得已的情况下再选择线程同步机制。

1. 尽量使用局部变量代替实例变量和静态变量。
2. 如果必须是实例变量，那么可以考虑创建多个对象，这样实例变量的内存就不共享了。（一个线程对应一个对象，100个线程对应100个对象，对象不共享，就没有数据安全问题了）
3. 如果不能使用局部变量，对象也不能创建多个，这个时候只能选择synchronized了，线程同步机制。



## 守护线程

> 就是后台线程，java就两种线程：用户线程，守护线程

```java
DamonThread damonThread = new DamonThread();

Thread dThread = new Thread(damonThread);
dThread.setDaemon(true);
Dthread.start();
System.out.println(dThread.isDaemon());
```

守护线程（后台线程）从一开始就开始运行，比当前线程开始运行的时间早。比如抢鞋的例子，100双鞋抢完了，守护线程就会打印消息：鞋已抢完，并中止当前线程的执行，不再抢鞋。



### 代表性的：垃圾回收线程

特点

1. 一般守护线程是一个死循环
2. 所有的用户线程只要结束，守护线程自动结束。

使用的地方：

每天00：00的时候，系统数据自动备份，这个需要使用定时器，并且我们可以将定时器设置为守护线程，一直在那里看着，每到00：00自动备份一次。所有的用户线程如果结束了，守护线程自动退出



## 定时器

作用：间隔特定的时间，执行特定的程序

每周要进行银行账户的总账操作，每天要进行数据的备份操作。

三种方式实现：

1. 使用sleep方法（太low了）
2. 使用java.util.Timer
3. 使用SpringTask框架



Timer类中的方法举例

```java
// schedule
    public void schedule(TimerTask task, Date firstTime, long period) {
        if (period <= 0)
            throw new IllegalArgumentException("Non-positive period.");
        sched(task, firstTime.getTime(), -period);
    }
```



## Object中的wait和notify方法

这两个方法不是线程对象的方法，是java中任何一个对象都有的方法

```java
// 会让当前线程(在o上活动的线程)进入等待状态，直到被唤醒
Object o = new Object();
o.wait();

// 唤醒o对象上正在等待的线程
o.notify();

// 唤醒o对象上正在等待的所有线程
o.notifyAll();
```



## 生产者和消费者模式

在这个模式中，wait方法和notify方法的使用是建立在synchronized方法的基础之上。

o.wait()方法会释放o对象的锁，notify()方法只会通知，不会释放锁

![image-20210805175354785](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210805175354785.png)

o.wait()方法的作用：让正在o对象上活动的线程t进入等待状态，并且释放掉t线程之前占有的o对象的锁。

o.notify()方法的作用：让正在o对象上等待的线程唤醒，只是通知，不会释放o对象上之前占有的锁。

notifyAll()方法：如果有多个生产者，就会唤醒其他所有的生产者。



为什么我的程序打印取出的obj是空呢？





java并发编程的艺术，书



# 反射机制

通过java语言中的反射机制，**可以操作字节码文件**，有点类似于黑客（可以读和修改字节码文件）。通过反射机制可以操作代码片段（class文件）

反射机制可以让程序更加灵活

相关类在java.lang.relfect，其相关类有

- java.lang.Class   代表字节码文件
- java.lang.reflect.Method   代表字节码中的方法字节码
- java.lang.reflect.Constructor   代表字节码中的构造方法字节码
- java.lang.reflect.Field   代表字节码中的属性字节码



## 获得Class的三种方式

要操作一个类的字节码，首先要获得（拿到）它。如何获取Class实例？

### Class.forName()

> `Class c =Class.forName("完整类名带包名") `

1. 静态方法
2. 方法中的参数是一个字符串
3. 字符串需要的是一个完整类名
4. 完整类名必须带有包名，java.lang包也不能省略

![image-20210806135734412](C:\Users\s'c\AppData\Roaming\Typora\typora-user-images\image-20210806135734412.png)



forName还有一个用处，就是只执行类中的静态代码块，不执行别的内容



### getClass()

> `Class c = 对象.getClass()`

java种任何一个对象都有一个方法：getClass()

```java
String s = "abc";
Class x = s.getClass();// x代表String.class字节码文件
```

字节码文件装载到JVM中的时候，只装载一份。

```java
Date time = new Date();
Class y = time.getClass();
System.out.println(c2==y);// true   c2和y两个变量中保存的内存地址都是一样的，都指向方法区中的字节码文件
```



### .class属性

> 第三种方式，java语言中任何一种类型，包括基本数据类型，它都有.class属性

```java
Class z = String.class;
Class k = Date.class;
Class f = int.class;

System.out.println(c1==z);// true
System.out.println(c2==k);// true
System.out.println(c3==f);// true
// 它们都指向方法区中的同一个class文件
```



## 通过反射实例化对象

使用.newInstance()方法   已过时

```java
public class reflectTest01 {
    public static void main(String[] args) throws Exception {
        Class c = Class.forName("ThreadSafe.Account");

        // 创建新的对象，实例化
        // newInstance()这个方法会调用API这个类的无参数构造方法，完成对象的创建
        // 注意此时，若在API中没有写无参数的构造方法，但是写了有参数的构造方法，就会报错InstantiationException
        Object obj = c.newInstance();
        System.out.println(obj);
    }
}
```

重点是：newInstance()方法会调用无参数构造方法，必须保证无参数构造方法是存在的。



## 通过读属性文件实例化对象

java代码写一遍，在不改变java源代码的基础之上，可以做到不同对象的实例化，非常灵活，符合OCP开发原则，开闭原则，对扩展开放，对修改关闭 。

**只需要修改配置文件就好了**

后期要学习高级框架  ssh  ssm  Spring  MyBatis  SpingMVC   Hibernate

这些高级框架的底层原理，都采用了反射机制，学习反射机制有利于理解剖析底层的源代码





## *关于路径的问题

以上通过反射机制实例化对象的缺点是，移植性差，在IDEA中默认的当前路径是project的根。这个代码假设离开了IDEA，换到了其他位置，可能当前路径就不是project的根了，这是这个路径就无效了。

```java
FileReader reader = new FileReader("chapter25/classinfo2.properties");
```

介绍一种通用的方式，即使代码换位置了，仍然是可以的

**前提：这个文件必须在类路径src下，src是类的根路径**（严格意义上来说不是的，out才是class的根路径，src是java源文件的路径）

```java
String path =Thread.currentThread().getContextClassLoader().getResource("参数").getPath();
// Thread.currentThread()当前线程对象
// getContextClassLoader()线程对象的方法，可以获取到当前线程的类加载器对象
// 分为启动类加载器，应用，扩展类加载器
// getResource()  （获取资源） 类加载器对象的方法，当前线程的类加载器默认从类的根路径下加载资源


String path = Thread.currentThread().getContextClassLoader().getResource("classinfo2.properties").getPath();
        System.out.println(path);
// 拿到了classinfo2.properties文件的绝对路径
// getResource()方法的起点是根路径

// /E:/project/Java/demo/out/production/demo/classinfo2.properties
```

==**getResource()方法的起点是根路径**==

若配置文件没有放在类的根目录src下，就会出现NullPointerException空指针异常。放在包里也要加上包的相对路径

```java
String path = Thread.currentThread().getContextClassLoader().getResource("reflect/classinfo3.properties").getPath();
        System.out.println(path);
```



#### 通过流返回配置文件中的内容

```java
public class AboutPath {
    public static void main(String[] args) throws Exception{

        String path = Thread.currentThread().getContextClassLoader().getResource("reflect/classinfo3.properties").getPath();
        System.out.println(path);

        // 获得配置文件中的内容
        FileReader reader = new FileReader(path);
        // 创建属性类对象Map
        Properties pro = new Properties();
        // 加载
        pro.load(reader);
        // 关闭流
        reader.close();

        String className = pro.getProperty("className");
        System.out.println(className);
    }
}
```

#### 也可以直接以流的形式返回

```java
public class AboutPath {
    public static void main(String[] args) throws Exception{

        InputStream reader = Thread.currentThread().getContextClassLoader().getResourceAsStream("reflect/classinfo3.properties");

        // 创建属性类对象Map
        Properties pro = new Properties();
        // 加载
        pro.load(reader);
        // 关闭流
        reader.close();

        String className = pro.getProperty("className");
        System.out.println(className);
    }
}
```



## 资源绑定器

1. 只能绑定xxx.properties文件，并且这个文件必须在类路径下
2. 并且在写路径的时候，路径后面的扩展名不能写

```java
public class ResourceBundleTest {
    public static void main(String[] args) {

        // 资源绑定器，只能绑定xxx.properties文件，并且这个文件必须在类路径下
        //并且在写路径的时候，路径后面的扩展名不能写
        ResourceBundle bundle = ResourceBundle.getBundle("classinfo2");
        String className = bundle.getString("className");
        System.out.println(className);
    }
}
```

以后在写配置文件的时候，属性配置文件直接放到src下，类路径下，若放到src的包下，则需要使用com/.../.../xxx.properties



## 类加载器

专门负责加载类的命令/工具 ClassLoader

JDK中自带了三个类加载器

1. 启动类加载器（父加载器）
2. 扩展类加载器（母加载器）    双亲委派机制
3. 应用类加载器

假设有这样一段代码

```java
String s = "abd";
```

程序在开始执行之前，会将所需要的类全部加载到**JVM**当中，通过类加载器加载，看到以上代码类加载器会找到String.class文件，找到就加载，那么是怎么进行加载的呢？

1. 首先通过“启动类加载器”加载

   注意：启动类加载器专门加载`rt.jar`,其中都是JDK中最核心的类库。

2. 如果通过启动类加载器加载不到的时候，会通过扩展类加载器加载，注意：扩展类加载器专门加载ext\*.jar

3. 如果扩展类加载器没有加载到，那么会通过应用类加载器加载
   注意：应用类加载器专门加载classpath中的类。



java中为了保证类加载的安全，使用了双亲委派机制，优先从启动类加载器中加载，称为“父”，父无法加载到再从扩展类加载器中加载，称为“母”。如果都加载不到，才会考虑从应用类加载器加载，直到加载到为止。





## ==获取类的Field==

```java
package reflect;

import java.lang.reflect.Field;
import java.lang.reflect.Modifier;

public class reflectTest03 {
    public static void main(String[] args) throws Exception {
        Class c = Class.forName("bean.Student");
        // getFields()方法获取所有公开public的属性
        Field[] fields = c.getFields();
        System.out.println(fields.length);

        // 获取完整类名
        System.out.println(c.getName());
        // 获取简单类名
        System.out.println(c.getSimpleName());

        Field field = fields[0];
        String fieldName = field.getName();
        System.out.println(fieldName);

        // 获取所有的Field
        Field[] fs = c.getDeclaredFields();
        System.out.println(fs.length);

        // 遍历
        for (Field field1 : fs) {
            // 获取属性的修饰符列表
            int i = field1.getModifiers();// 返回的修饰符是一个数字，每个数字是修饰符的代号
            System.out.println(i);
            // 可以将这个代号数字转化成字符串么？
            String modifierString = Modifier.toString(i);
            System.out.println(modifierString);

            // 获取属性的类型
            Class fieldType;
            fieldType = field1.getType();
            System.out.println(fieldType.getSimpleName());
            // System.out.println(field1.getType());

            // 获取属性的名字
            System.out.println(field1.getName());
        }
    }
}
```



## 利用反射机制进行反编译

有一个class文件，得到其中的java源代码

```java
package reflect;

// 通过反射机制进行反编译
// 给我一个class文件，我可以拿到java源码

import java.lang.reflect.Field;
import java.lang.reflect.Modifier;

public class reflectTest04 {
    public static void main(String[] args) throws Exception {
        Class c = Class.forName("bean.Student");
        StringBuilder s = new StringBuilder();

        s.append(Modifier.toString(c.getModifiers()) + " class " + c.getSimpleName() + "{\n");
        Field[] fields = c.getDeclaredFields();
        for(Field field:fields){
            s.append("\t");
            s.append(Modifier.toString(field.getModifiers()));
            s.append(" ");
            s.append(field.getType().getSimpleName());
            s.append(" ");
            s.append(field.getName());
            s.append(";\n");
        }

        System.out.println(s);
    }
}
```





## 通过反射机制访问对象的属性

```java
/*
 * 怎么通过反射机制访问一个java对象的属性？
 *       给属性赋值set
 *       获取属性的值get
 * */
public class reflectTest07 {
    public static void main(String[] args) throws Exception {
        // 获取类
        Class c = Class.forName("bean.Student");
        // 首先要把对象new出来
        Object obj = c.newInstance();
        // 这两步就相当于Student obj = new Student();这一行代码

        // 获取类中的属性，属性与属性之间依靠名字来区分
        Field numberfield = c.getDeclaredField("number");

        // 给obj对象（student对象）的number属性赋值
        numberfield.set(obj, 2222);// 类似于obj.number=2222;
        // 要素1：对象s
        // 要素2：number属性
        // 要素3：2222这个值

        // 获取对象的属性的值
        // 两个要素
        // 要素1：对象obj
        // 要素2：
        System.out.println(numberfield.get(obj));

        // 可以访问私有的属性吗？
        Field nameField = c.getDeclaredField("name");

        // 此时若想访问，则需要打破封装
        nameField.setAccessible(true);// 反射机制的缺点，打破封装，可能会给不法分子留下机会
        // 这样设置完之后，在外部也可以访问private

        nameField.set(obj,"jackson");
        System.out.println(nameField.get(obj));// 私有权限无法访问

    }
}
```





## 可变长度参数

```java
package reflect;
/*
* 可变长度参数
*       int... args
*       类型...(一定是三个点)
*   1. 要求的参数个数是0-n个
*   2. 可变长度参数在参数列表中必须在最后一个位置上，而且可变长度参数只能有一个
*   3. 可变长度参数可以当作一个数组来看待
* */
public class ArgsTest {
    public static void main(String[] args) {
//        m();
//        m(10);
//        m(10,20,30,40);
//
//        m2(100);
//        m2(100,"asdf");
//        m2(100,"asdf","sdfsdf");
//        m2(100,"asdf","sdfsdf","sdasdf");

        m3("我","是","中","国","人");
        // 也可以直接传一个数组进去
        String[] strs = {"a","b","c"};
        m3(strs);
        // 也可以这样，类似匿名内部类
        m3(new String[]{"a","b","c"});

    }

    public static void m(int... args){
        System.out.println("m方法执行了...");
    }

    public static void m2(int a,String... args1){
        System.out.println("m2方法执行了...");
    }

    public static void m3(String... args){
        // args有length属性
        // 可以把它当成一个数组来看待
        for(int i=0;i<args.length;i++){
            System.out.println(args[i]);
        }
    }
}
```



## 反射Method和反编译Method

这个代码写的是反编译Method

```java
package reflect;


import javax.management.modelmbean.ModelMBean;
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;

public class reflectTest08 {
    public static void main(String[] args) throws Exception{
        Class UserServiceClass = Class.forName("java.util.Date");
        Method[] methods = UserServiceClass.getDeclaredMethods();
        System.out.println(methods.length);


        // 遍历其中的方法
        for(Method method:methods){
            StringBuilder s = new StringBuilder();
            // 获取修饰符
            s.append(Modifier.toString(method.getModifiers()));
            s.append(" ");
            // 获取返回值类型
            s.append(method.getReturnType().getSimpleName());
            s.append(" ");
            // 获取方法名
            s.append(method.getName());
            s.append("(");
            // 获取方法的参数类型列表
            Class[] parameterTypes = method.getParameterTypes();
            if(parameterTypes.length==0){
                s.append("("); // 为了处理删去最后一个,之后产生的格式问题
            }
            for(Class parameter:parameterTypes){
                s.append(parameter.getSimpleName());
                s.append(",");
            }

            s.deleteCharAt(s.length()-1);

            s.append("){}");
            System.out.println(s);

        }

    }
}

```





## ==通过反射机制调用对象的方法==

```java
package reflect;

import java.lang.reflect.Method;

/**
 * 通过反射机制怎么调用一个对象的方法
 *
 * 以后只需要写配置文件，更改配置文件里面的内容，java代码不需要做任何改动
 * 十分具有通用性
 */
public class reflectTest10 {
    public static void main(String[] args) throws Exception {
        Class userServiceClass = Class.forName("service.UserService");
        Object obj = userServiceClass.newInstance();

        // java中区分方法：依靠方法名和形参
        // 获取Method
        Method loginMethod = userServiceClass.getDeclaredMethod("login", String.class, String.class);
        // 调用方法
        // 有几个要素?
        // 要素一：对象   obj
        // 要素二：login方法名    loginMethod
        // 要素三：实参列表   "admin"  "123"
        // 要素四：返回值      retValue

        // loginMethod.调用(对象，传入的参数...);
        Object retValue = loginMethod.invoke(obj, "admin", "123");// 方法的形参列表处是两个String,所以此处也传入两个String
        System.out.println(retValue);

    }
}
```



## 使用反射机制反编译Constructor

```java
package reflect;

import bean.Vip;

import java.lang.reflect.Constructor;
import java.lang.reflect.Modifier;

/**
 * 反编译一个类的Constructor构造方法
 */
public class reflectTest11 {
    public static void main(String[] args) throws Exception {
        StringBuilder s = new StringBuilder();
        Class VipClass = Class.forName("java.util.Date");
        s.append(Modifier.toString(VipClass.getModifiers()));
        s.append(" class ");
        s.append(VipClass.getSimpleName());

        s.append("{\n");

        // 拼接构造方法
        Constructor[] constructors = VipClass.getDeclaredConstructors();
        for (Constructor constructor : constructors) {
            s.append("\t");
            // public Vip(int no, String name, String birth) {
            s.append(Modifier.toString(VipClass.getModifiers()));
            s.append(" ");
            s.append(VipClass.getSimpleName());
            s.append(" (");
            // 拼接参数
            Class[] parameterTypes = constructor.getParameterTypes();
            for (Class parameterType : parameterTypes) {
                s.append(parameterType.getSimpleName());
                s.append(",");
            }
            if (parameterTypes.length > 0) {
                s.deleteCharAt(s.length()-1);
            }
            s.append("){}\n");
        }

        s.append("}");
        System.out.println(s);
    }
}

```





## 使用反射机制获取一个类的父类和它实现的接口

```java
package reflect;

/**
 * 给你一个类，如何获取这个类的父类，以及它实现的接口
 */
public class reflectTest13 {
    public static void main(String[] args) throws Exception {
        Class stringClass = Class.forName("java.lang.String");
        // 获取它的父类
        Class superclass = stringClass.getSuperclass();
        System.out.println(superclass.getSimpleName());

        // 获取String类实现的所有接口，一个类可以实现多个接口
        Class[] interfaces = stringClass.getInterfaces();
        for(Class in:interfaces){
            System.out.println(in.getName());
        }
    }
}
```





# 注解

 注解，或者叫做注释
 Annotation是一种引用数据类型，编译之后也是生成class文件
 自定义注解：
     [修饰符列表]@interface 注解类型名{

​     }

 注解使用：

@注解名称



默认情况下注解可以出现在任意位置

常见的四种注解形式，后两种是元注解

```java
Override; // 标注方法被重写
Deprecated (since="9"); // 标注方法已过时
Target;
Retention;
```



## 元注解

> 用来标注“注解类型”的“注解”，称为元注解

常见的元注解有哪些？ 

- Target：这是一个元注解，用来标注“被标注的注解”可以出现在哪些位置上

  ```java
  @Target(ElementType.METHOD)// 表示“被标注的注解”只能出现在方法上
  ```

  

- Retention：用来标注“被标注的注解”最终保存在哪里。

  ```java
  @Retention(RetentionPolicy.SOURCE)// 表示该注解只被保留在java源文件中
  @Retention(RetentionPolicy.CLASS)// 该注解被保存在class文件中
  @Retention(RetentionPolicy.RUNTIME)// 表示该注解被保存在class文件中，并且可以被反射机制获取
  ```

  

```java
public class AnnotationTest01 {

    // 报错的原因：如果一个注解当中有属性，必须给属性赋值，除非该属性使用default给定了默认值。
    // @MyAnnotation()
    @MyAnnotation(name = "shenchen", color = "blue")
    // 指定name属性的值就好了
    // 若有默认值，则不用重新指定
    public void doSome() {

    }

    public static void main(String[] args) {

    }
}



package com.java.annotation;
// 注解当中可以指定属性，可以使用default给定默认值
public @interface MyAnnotation {
    /**
     * 我们通常在注解当中可以定义属性，以下这个是MyAnnotation的name属性
     * 看着像一个方法，但实际上我们称之为属性name
     *
     * @return
     */
    String name();

    String color();

    int age() default 20;// 属性指定默认值
}

```



## value属性名称的省略

```java
// 当注解中的属性名为value，并且只有一个属性的话，在使用时，该属性名可以省略
// 
    @MyAnnotation2("haha")
    public void doOther(){

    }
}
public @interface MyAnnotation2 {
    String value();
}
```





定义一个注解，其实是定义一个注解类，使用注解的时候，其实是使用了注解对象？？

自己定义的注解MyAnnotation是Annotation的子类？？





## 反射注解

```java
package com.java.annotation.ReflectAnnotation;

import java.lang.annotation.Annotation;

public class AnnotationTest01 {
    public static void main(String[] args) throws Exception {
        // 获取类
        Class c = Class.forName("com.java.annotation.ReflectAnnotation.AnnotationTest");
        // 判断类上面是否有@MyAnnotation
        System.out.println(c.isAnnotationPresent(MyAnnotation.class));
        if (c.isAnnotationPresent(MyAnnotation.class)) {
            // 获取该注解对象
            // 这一行转型的没看懂
            MyAnnotation myAnnotation = (MyAnnotation) c.getAnnotation(MyAnnotation.class);

            // 获取注解中的属性
            String value = myAnnotation.value();
            
            System.out.println(value);

        }

        // 判断String类上是否有这个注解
        Class StringClass = Class.forName("java.lang.String");
        System.out.println(StringClass.isAnnotationPresent(MyAnnotation.class));

    }
}

```





## 注解的作用

注解在程序当中等同于一种标记， 如果这个元素上有这个注解怎么办，没有这个注解怎么办





# 异常

程序执行中的不正常情况叫做异常

## 异常的作用

java把异常信息打印输出到控制台，供程序员参考，程序员看到异常信息之后，可以对城西进行修改，让程序更加健壮。

程序执行，控制台出现了异常信息：

```java
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at com.demo.exception.ExceptionTest01.main(ExceptionTest01.java:7)
```

这是JVM打印的



## 异常在java中以类和对象的形式存在

小声bb：输出一个引用类型的对象，会自动调用toString()

1. 异常在java中以类的形式存在，每一个异常类都可以创建异常对象
2. java在执行到不正常的代码时，JVM会创建一个异常对象，然后把这个异常对象抛出去了，打印输出信息到控制台。比如除数是0的那个异常，字符串就传了“/ by zero”         **异常只要发生，就有对象存在**

类是模板，对象是实际存在的个体

可能不是同一个异常，但是同一类的异常，比如算数异常，除数为0









# Javaweb



## 相关方法

```java
Socket(); //创建一个还未被链接的套接字
void connect(SocketAddress address);//将该套接字连接到给定的地址
void connect(SocketAddress address,int timeoutInMilliseconds);//将套接字连接到给定的地址，如果在给定的时间内没有响应，则返回
```



### 打开一个套接字

```java
Socket s = new Socket("time-a.nist.gov",13);
```

### 获取流对象

```java
InputStream inStream = s.getInputStream();
```



### 设置超时时间

```java
s.setSoTimeout(10000);//10s 之后超时
```

