## 异常机制

### 异常的概念

异常也称为例外，是在程序运行过程中发生的、会打断程序正常执行的事件。

### 异常的分类

#### Error

错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

#### Exception

checked Exception

最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。

runtime Exception

运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。

### 异常的处理方法

#### 捕获异常

try-catch-finally

```java
try{
    要检查的程序语句 ;
    ...
}catch( 异常类 对象名称){
    异常发生时的处理语句 ;
}finally{
    一定会执行到的程序代码 ;
}
```

执行顺序

1.try程序块若是有异常发生，程序的运行便中断，并抛出“异常类所产生的对象”。

2.抛出的对象如果属于catch()括号内欲捕获的异常类，catch()则会捕捉此异常，然后进到catch的块里继续运行。

3.无论try程序块是否捕捉到异常，或者捕捉到的异常是否与catch()括号里的异常相同，最后一定会运行finally块里的程序代码。

#### 声明和抛出异常

throws/throw

如果一个方法没有捕获到一个检查性异常，那么该方法必须使用 throws 关键字来声明。throws 关键字放在方法签名的尾部。

也可以使用 throw 关键字抛出一个异常，无论它是新实例化的还是刚捕获到的。

下面方法的声明抛出一个 RemoteException 异常：

```java
import java.io.*;
public class className{
  public void deposit(double amount) throws RemoteException {
    // Method implementation
    throw new RemoteException();
  }
  //Remainder of class definition
}
```

一个方法可以声明抛出多个异常，多个异常之间用逗号隔开。

### 自定义异常

在 Java 中你可以自定义异常。编写自己的异常类时需要记住下面的几点。

1.所有异常都必须是 Throwable 的子类。

2.如果希望写一个检查性异常类，则需要继承 Exception 类。

3.如果你想写一个运行时异常类，那么需要继承 RuntimeException 类。

```java
class MyException extends Exception{
}
```



## 常用类

### Scanner

import java.util.Scanner;

Scanner sc = new Scanner(System.in);

获取键盘输入的一个int数字： int num = sc.nextInt();  

获取键盘输入的一个字符串： String str = sc.next();

### 匿名对象

创建对象的标准格式：类名称 对象名 = new 类名称（）；

格式： new 类名称();

用法： new 类名称().属性=xxx；    new 类名称().方法();

```java
使用匿名对象输入： int num = new Scanner(System.in).nextInt();
```

```java
使用匿名对象传参：methodParam(new Scanner(System.in));
```

注意：匿名对象只能使用唯一的一次，下次再用不得不再创建一个新对象。

使用建议：如果确定一个对象只需要使用唯一的一次，就可以使用匿名对象。

### 基本数据类型的包装类

#### 包装的基本知识

所有的包装类**（Integer、Long、Byte、Double、Float、Short）**都是抽象类 Number 的子类。

如果想向ArrayList中存储基本数据类型，必须使用其对应的“包装类”。

#### 包装类的用法

| **包装类**       | Boolean | Byte | Short | Integer   | Long | Character  | Float | Double |
| ---------------- | ------- | ---- | ----- | --------- | ---- | ---------- | ----- | ------ |
| **基本数据类型** | boolean | byte | short | int(特殊) | long | char(特殊) | float | double |



```java
Integer a=123;
```

#### 自动拆箱和装箱

装箱就是自动将基本数据类型转换为包装器类型；

拆箱就是自动将包装器类型转换为基本数据类型。

大多数情况包装类的主要作用适用于，基本数据类型与字符串的相互转换。

parseInt（String s）解析

valueOf

除了char都有parseXXX方法

### 字符串相关类

#### Object

toString()：返回该对象的字符串表示，建议每个子类都重写.

equals(Object obj)： 指示其他某个对象是否与此对象“相等”。

boolean equals(Object obj)方法使用的是“==”，比较的是地址值，建议Object的子类都重写equals方法从而比较内容。

重写equals方法：

```java
@Override
public boolean equals(Object obj){
    	Student other=(Student)obj;
    	if(this.name.equals(other.name)
          		 &&this.age.equals(other.age)){
           return true;
              }
	return false;
}
```

**面试**：equals和==区别？

1.在Object类中，都是比较对象的地址

2.在其他子类中，一般都重写了equals，用于比较对象内容

3.equals是方法，==是运算符

#### Objects工具类

对两个对象进行比较，防止空指针异常。

```java
public static boolean equals(Object a, Object b) {
        return (a == b) || (a != null && a.equals(b));
    } 
```

#### String

1.字符串是常量，**内容永不可变。**“改变的是引用的地址值”
2.由于**字符串永不可变**，所以可以共享使用。
3.字符串效果上相当于是char[]字符数组，但底层原理是byte[]字节数组。

##### 比较

```java
public String trim()
```

滤空。返回字符串的副本，忽略前导空白和尾部空白。

```java
public boolean equalsIgnoreCase(String str)：忽略（只忽略英文的）大小写，比较内容。
```

```java
public boolean contains(CharSequence s)
```

判断字符串是否包含指定内容。

```java
public boolean equals(Object obj)：比较字符串内容，只有参数是一个字符串并且内容相同时才会给true，否则返回false。equals()具有对称性。
例如：str1.equals(str2);
```

ps：如果比较双方一个常量一个变量，推荐把常量字符串写在前面。

```java
public int compareTo(String anotherString)
```

按顺序比较两个字符串

```java
pbulic boolean isEmpty()
```

判断是否为空

##### 获取

```java
public String concat(String str)
```

将当前字符串和参数字符串拼接成为返回值新的字符串。

```java
public char charAt(int index)
```

获取指定索引位置的单个字符（索引从0开始）

```java
public int indexOf(String str)
```

查找参数字符串在本字符串当中**首次**出现的位置，如果没有，返回 -1 .



```java
public int length()
```

获取字符串中含有的字符个数，拿到字符串长度。

##### 截取

```java
public String substring(int index)
```

截取从参数位置一直到字符串末尾，返回新字符串。（用移动光标数位数）

```java
public String sunstring(int begin,int end)
```

截取从begin开始，一直到end结束，中间的字符串。【begin，end），包含左边，不包含右边。

**注意：Str**ing str = "Hello";**
        str = "Java";字符串内容没变，变的是地址值。**

##### 转换

```java
public char[ ] toCharArray()
```

将当前字符串拆分成字符数组作为返回值。

```java
public byte[ ] getBytes()
```

获得当前字符串地秤的字节数组。

```java
public String replace(CharSequence oldString,CharSequence new String)
```

将所有出现的老字符串替换成新的字符串，返回替换之后的结果新字符串。

例如：

```java
String str1="How do you do?";
String str2=str1.replace("o","*");
System.out.println(str1);//How do you do?
System.out.println(str2);//H*w d* y*u d*?
```

##### 分割

```java
public String[ ] split(String regex)
例如：String str="aaa,bbb,c";
String array=str.split
```

按照参数的规则，将字符串切分成为若干部分。

注意：split方法的参数其实是一个”正则表达式“，如果按照英文据点"."进行切分，必须写"\\ ."

##### 拼接

题目1：定义一个方法，把数组（1，2，3）按照指定格式拼接成一个字符串。[word1#word2#word3]

分析：
1.首先准备一个int[]数组，内容是：1，2，3
2.定义一个方法，用来将数组变成字符串
   三要素：返回值类型 ；String
          方法名：fromArrayToString
          参数列表：int[]
3.格式： [word1#word2#word3]
  用到：for循环、字符串拼接、每个数组元素之前都有一个word字样、分割使用的是#、区分一下是不是最后一个
4.调用方法，得到返回值，并打印结果字符串

```java
public static void main(String[] args) {
        int[] array={1,2,3};
        String result=fromArrayToString(array);
        System.out.println(result);
    }

    private static String fromArrayToString(int[] array) {
        String str="[";
        for (int i = 0; i < array.length; i++) {
            if(i==array.length-1){
                str+="word"+array[i]+"]";
            }else{
                str+="word"+array[i]+"#";
            }
            return str;
        }
    }
```

题目2：题目：键盘输入一个字符串，并且统计其中各种字符串出现的次数。、
种类有：大写字母，小写字母，数字，其他。

思路：
1.Scanner；
2.String str=sc.next();
3.定义四个变量，分别对应四种字符出现的次数。
4.需要对字符串逐字检查，String-->char[],方法就是toCharArray()
5.遍历char[]字符数组，对当前字符的种类进行判断。并且用四个变量++动作。
6.打印输出四个变量。

```java
public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        System.out.println("请输入一个字符串： ");
        String input=sc.next();

        int countUpper=0;
        int countLower=0;
        int countNumber=0;
        int countOther=0;
        char[] charArray=input.toCharArray();
        for (int i = 0; i < charArray.length; i++) {
            char ch=charArray[i];// 当前单个字符
            if('A'<=ch&&ch<='Z'){
                countUpper++;
            }else if('a'<=ch&&ch<='z'){
                countLower++;
            }else if('0'<=ch&&ch<='9'){
                countNumber++;
            }else{
                countOther++;
            }
        }
        System.out.println("大写字母有："+countUpper);
        System.out.println("小写字母有："+countLower);
        System.out.println("数字有："+countNumber);
        System.out.println("其他符号有："+countOther);
    }
```

#### StringBuffer和StringBuilder

##### StringBuffer

线程安全的**可变**字符序列

**同步**，效率低

```java
public StringBuffer append(String str)
```

 将指定的字符串追加到此字符序列。 

```java
public StringBuffer delete(int start,int end)
```

移除此序列的子字符串中的字符。

```java
public StringBuffer insert(int offset,Object obj)
```

将 `Object` 参数的字符串表示形式插入此字符序列中。

StringBuffer-->String

1.StringBuffer的toString()

2.new String(StringBuffer)

3.String.valueOf(StringBuffer)

##### StringBuilder

**不同步**，效率高

不保证线程安全的可变字符序列，与StringBuffer的APi完全一致.

StringBuffer 和 StringBuilder 类可以对字符串进行修改。

和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。

StringBuilder 更快（使用的多），StringBuffer是线程安全的。

面试：String、StringBuffer、StringBuilder异同？

#### 创建

##### 3种构造方法

public String()：创建一个空白字符串，不含有任何内容。 String str = new String();

public String(char[ ] array)：根据字符数组的内容，来创建对应的字符串。  String str = new String(charArray);

public String(byte[ ] array)：根据字节数组的内容，来创建对应的字符串。  String str = new String(byteArray);

##### 1种直接创建

String str = "Hello";

直接写上双引号" "，就是字符串对象。

### 字符串常量池

程序当中直接写上的双引号字符串，就在字符串常量池中。

对于基本数据来说，==是进行数值的比较。
对于引用数据来说，==是进行【地址值】的比较。

![image-20200716090939667](C:\Users\Z\AppData\Roaming\Typora\typora-user-images\image-20200716090939667.png)

### 时间处理相关类

#### Date时间类

##### 构造方法

Date类的空参构造方法：Date()  获取的是当前系统的日期和时间

Date类的有参构造方法：Date(long millisec)  传递毫秒值，把毫秒值转换为Date日期。millisec该参数是从1970年1月1日起的毫秒数。

##### 成员方法

long getTime()：返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。

```java
Date d1 = new Date();// 创建当前日期对象
// year-1900 month[0-11]
Date d2 = new Date(100,0,1);// 以指定年月日创建日期对象
Date d3 = new Date(31536000000L);// 以指定毫秒值创建日期对象System.out.println(d2.getTime());// 获得日期对象距 1970-01-01的毫秒值

```

#### DateFormat类&SimpleDateFormat类

java.text.DateFormat   是时间/日期格式化子类的抽象类

##### 成员方法

String **format**(Date date)     按照指定的模式，把Date日期，**格式化**(**日期->文本**）为符合模式的字符串

Date **parse**(String source)    把符合模式的字符串，**解析（文本->日期）**为Date日期。   只会解析默认pattern模板格式字符串。

```java
        Date d1 = new Date();
		System.out.println("格式化前 : "+d1);
		String pattern = "yyyy-MM-dd";
		SimpleDateFormat sdf = new SimpleDateFormat(pattern);
		String format = sdf.format(d1);
		System.out.println("格式化后 : "+format);
		System.out.println("----------");
		String birthday = "2000-01-01";

```

DateFormat类是一个**抽象类**，无法直接创建对象使用，可以使用其子类SimpleDateFormat。

#### Calandar类

抽象类，它为特定瞬间与一组诸如  `YEAR`、`MONTH`、`DAY_OF_MONTH`、`HOUR`  等 “日历字段”之间的转换提供了一些方法，并为操作日历字段（例如获得下星期的日期）提供了一些方法。瞬间可用毫秒值来表示，它是距*历元*（即格林威治标准时间 1970 年 1 月 1 日的 00:00:00.000，格里高利历）的偏移量。

```java
Calendar rightNow = Calendar.getInstance();
System.out.println(rightNow);
// 得到当前时间的某一字段值
System.out.println(rightNow.get(Calendar.YEAR));		System.out.println(rightNow.get(Calendar.MONTH)+1);
System.out.println(rightNow.get(Calendar.DATE));
// 日 一 二 .... 五 六		System.out.println(rightNow.get(Calendar.DAY_OF_WEEK));	System.out.println(rightNow.get(Calendar.HOUR_OF_DAY));
System.out.println(rightNow.get(Calendar.MINUTE));
System.out.println(rightNow.get(Calendar.SECOND));
// 重新设置值
rightNow.set(Calendar.YEAR, 2000);
// 设置时 0-11 代表1-12月
rightNow.set(Calendar.MONTH, 0);
rightNow.set(Calendar.DATE, 1);
System.out.println(rightNow.get(Calendar.YEAR));
// 得到时0-11 代表1-12月
System.out.println(rightNow.get(Calendar.MONTH));
System.out.println(rightNow.get(Calendar.DATE));
rightNow.add(Calendar.YEAR, 1);
rightNow.add(Calendar.DATE, 31);
System.out.println(rightNow.get(Calendar.YEAR));
System.out.println(rightNow.get(Calendar.MONTH)+1);
System.out.println(rightNow.get(Calendar.DATE));

```



### Math类

Math.PI     圆周率常量值

Math.E       e自然底数的对数

Math.abs(a)     取a的绝对值

Math.cbrt(a)      a的立方根

Math.sqrt(a)      a的平方根

Math.pow(double a,double b)   返回a的b次幂

Math.ceil(double a)         对a向上取整

Math.floor(double a)       对a向下取整

Math.round(double a)       对a四舍五入

Math.random()          返回[0.0,1.0)的double值

### System类

currentTimeMillis()      返回以毫秒值为单位的当前时间

exit(int status)           终止当前正在运行的Java虚拟机

gc()              运行垃圾回收机制

1970-01-01     1s=1000ms

### Random类

导包：import java.util.Random;

创建：Random r = new Random();

使用：int num = r.nextInt(int n);或者int num = r.next();

int的范围，有正负，Random(10)生成随机数的范围是0~9.常用int result = r.nextInt(n)+1;来取到1~n的值。

### File类



### 枚举类



## 集合ArrayList

特点：数组的长度可以随意变化。ArrayList有一个<E>代表泛型（装在集合中的所有元素都是同一类型）。泛型只能是引用数据类型。

Arraylist集合直接打印得到的是内容，不是地址值，如果内容为空，得到空的中括号：[ ]

ArrayList<String> list = new ArrayList<>();

public boolean add(E e)：向集合中添加元素，类型和泛型一致。

public E get(int index)：从集合中获取元素，参数是索引编号，返回值为对应位置的元素。

public E remove(int index)：从集合中删除元素，返回值为被删除的元素。

public int size()：获取集合的长度，返回值是集合包含元素的个数。

## 内部类

### 成员内部类（定义在类内部）

```java
修饰符 class 外部类名称{
    修饰符 class 内部类名称{
        //...
    }
    //...
}// 注意：内用外，随意访问；外用内，需要内部类对象。
```

调用方式：
1.间接方式：在外部类的方法中，使用内部类，然后main只是调用外部类的方法。
2.直接方式：公式：
外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称();

重名现象：外部类名称.this.外部类成员变量名

### 局部内部类（定义在方法内部）

只有当前所属的方法才能使用它，出了这个方法外面就不能用了。

如果接口的实现类（或是父类的子类）只使用唯一的一次，那么这种情况下就可以省略掉该类的定义，而改为使用【匿名内部类】

接口名称 对象名 = 接口名称(){
    //覆盖重写所有抽象方法
        };

```java
MyInterface obj = new Myinterface(){
    @Override
    public void method(){
        System.out.println("匿名内部类重写的方法");
    }
}；
```



## 容器

#### 容器的作用和概览



#### 容器的接口层次结构



#### Collection接口



#### List接口



#### Set接口



#### Map接口



#### Iterator接口



#### Collections工具类



#### Arrays工具类



#### Comparable接口



#### 泛型

## IO流

### 引入IO流的原因

### 基本概念

#### 数据源

#### 流的概念

### IO流的概念细分

### IO流的体系

### IO流对象

#### InputStream

#### OutputStream

#### FileInputStream

#### FileOutpuStream

#### ByteArrayInputStream

#### ByteArrayOutputStream

#### BufferedInputStream

#### BufferedOutputStream

#### DataInputStream

#### DataOutputStream

#### ObjectInputStream

#### ObjectOutputStream

#### PrintStream

#### Reader

#### Writer

#### FileReader

#### FileWriter

#### BufferReader

#### BufferWriter

#### InputStreamReader

#### OutputStreamWriter

### Java对象的序列化和反序列化

#### 为什么需要序列化和反序列化

#### 对象的序列化的用途

#### 序列化涉及的接口和类

#### 序列化和反序列化的使用

### IO的其他常用类

#### File类

#### RandomAccessFile

## 多线程

### 基本概念

#### 程序

#### 进程

#### 线程

#### 进程和线程的区别

#### 进程和程序的区别

### Java实现多线程

#### 继承Thread类

#### 实现Runnable接口

### 线程生命周期

#### 新生状态

#### 就绪状态

#### 运行状态

#### 死亡状态

#### 阻塞状态

### 线程的基本信息和优先级别

### 线程同步和死锁问题

### 死锁及解决方式

### 生产者/消费者模式

## 网络编程

### 基本概念

#### 计算机网络

#### 网络通信协议

#### 网络通信接口

#### 网络分层

#### 通信协议的分层规定

#### 数据封装

#### 数据拆封

#### IP

#### 端口

#### URL

### TCP和UDP

#### 区别

#### TCP协议

#### UDP协议

### Java网络编程

#### InetAddress

#### InetSocketAddress

#### URL类

#### 基于TCP协议的Socket编程和通信

#### UDP通信的实现

## NIO编程讲解

## JVM讲解 

## 数据结构

## 设计模式的讲解

## XML&正则表达式

