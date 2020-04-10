# java面试题

## 目录



### Java 面向对象

#### 1、super()与 this()的区别？


this() ：当前类的对象,super 父类对象。

super()：在子类访问父类的成员和行为,必须受类继承规则的约束而 this 他代表当前对象,当然所有的资源都可以访问。

在构造函数中,如果第一行没有写 super(),编译器会自动插入.但是如果父类没有不带参数的构造函数,或这个函数被私有化了(用 private 修饰).此时你必须加入对父类的实例化构造.而 this 就没有这个要求,因为它本身就进行实例化的构造.

而在方法中 super 和 this 使用的方法就差不多了.只不过 super 要考虑是否能访问其父类的资源.



#### 2、作用域 public,protected,private,以及不写时的区别？

public:不同包、同一包、类内都可用
private：类内
protected: 不同包的子类、同一包、类内都可用
不写时:同一包内、类内

#### 3、编程输出如下图形。

```java
*****
****
***
**
*    
```

代码如下：

```java
public class Print {
	public static void main(String[] args) { for (int i = 0; i < 5; i++){
		for (int j = 5; j > i; j--) {
			System. out.print("*");
		}
		System. out.println();
		}
	}
}
```

#### 4、JAVA 的事件委托机制和垃圾回收机制


java 事件委托机制的概念,一个源产生一个事件并将它送到一个或多个监听器那里。在这种方案中，监听器简单的等待，直到它收到一个事件。一旦事件被接受，监听器将处理这个事件，然后返回。

垃圾回收机制 垃圾收集是将分配给对象但不再使用的内存回收或释放的过程。如果一个对象没有指向它的引用或者其赋值为 null,则次对象适合进行垃圾回收



#### 5、在 JAVA 中，如何跳出当前的多重嵌套循环？


用 break; return 方法。

#### 6、什么是 java 序列化，如何实现 java 序列化？(写一个实例)


序列化:

可以将一个对象保存到一个文件，所以可以通过流的方式在网络上传输，可以将文件的内容读取，转化为一个对象。


处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进行读写操作时所引发的问题。
序列化的实现：

将需要被序列化的类实现 Serializable 接口，该接口没有需要实现的方法， implements Serializable 只是为了标注该对象是可被序列化的，然后使用一个输出流(如：FileOutputStream)来构造一个 ObjectOutputStream(对象流)对象，接着，使用 ObjectOutputStream 对象的 writeObject(Object obj)方法就可以将参数为 obj 的对象写出(即保存其状态)，要恢复的话则用输入流。



#### 7、一个".java"源文件中是否可以包括多个类（不是内部类）？有什么限制？


可以。如果这个类的修饰符是 public，其类名与文件名必须相同。

#### 8、排序都有哪几种方法？请列举。用 JAVA 实现一个快速排序？


排序的方法有：插入排序（直接插入排序、希尔排序），交换排序（冒泡排序、快速排序），选择排序（直接选择排序、堆排序），归并排序，分配排序（箱排序、基数排序）快速排序的伪代码。

#### 9、Overload 和 Override 的区别。Overloaded 的方法是否可以改变返回值的类型?


方法的

重写 Override，子类覆盖父类的方法，将子类传与父类的引用调用的还是子类的方法。

重载 Overloading 一个类多个方法，名称相同，参数个数类型不同。

两者都是 Java 多态性的不同表现。

Overloaded 的方法是可以改变返回值的类型。

#### 10、Final 类有什么特点？


属性常量

方法不可以 overridding

类不可以继承

#### 11、继承时候类的执行顺序问题,一般都是选择题,问你将会打印出什么?


父类：

```java
package test;

public class FatherClass{

    public FatherClass(){
        System.out.println("FatherClass Create");
    }

}
```



子类:

```java
package test;

import test.FatherClass;

public class ChildClass extends FatherClass{

    public ChildClass(){
    	System.out.println("ChildClass Create");
    }

    public static void main(String[] args){
        FatherClass fc = new FatherClass();
        ChildClass cc = new ChildClass();
    }

}
```

输出结果：

```dockerfile
C:>java test.ChildClass
FatherClass Create
FatherClass Create
ChildClass Create
```



#### 12、内部类的实现方式?


答：示例代码如下：

```java
package test;

public class OuterClass{

	private class InterClass{
		Public Interlass(){
			System.out.println("InterClass Create");
		}
	}

	public OuterClass(){
		InterClass ic = new InterClass();
        System.out.println("OuterClass Create");
	}

	public static void main(String[] args){
		OuterClass oc = new OuterClass();
	}

}
```





输出结果:

```do
C:>java test/OuterClass
InterClass Create
OuterClass Create
```



#### 13、用 JAVA 实现一种排序，JAVA 类实现序列化的方法(二种)？

#### 14、如在 COLLECTION 框架中，实现比较要实现什么样的接口？


Collection 框架中实现比较要实现 Comparable 接口和 Comparator 接口

#### 15、用插入法进行排序代码如下

```java
package test;
import java.util.*;

class InsertSort{

    ArrayList al;

    public InsertSort(int num,int mod) {
        al = new ArrayList(num);
        Random rand = new Random();
        System.out.println("The ArrayList Sort Before:");
        for (int i=0;i<num ;i++ ) {
        	al.add(new Integer(Math.abs(rand.nextInt()) % mod + 1));
            System.out.println("al["+i+"]="+al.get(i));
        }
    }

    public void SortIt(){
        Integer tempInt;
        int MaxSize=1;
        for(int i=1;i<al.size();i++) {
    		tempInt = (Integer)al.remove(i); 
            if(tempInt.intValue()>=((Integer)al.get(MaxSize-1)).intValue()) {
    			al.add(MaxSize,tempInt);
    			MaxSize++;
    			System.out.println(al.toString());
    		} else {

   				 for (int j=0;j<MaxSize ;j++ ) {
    				if(((Integer)al.get(j)).intValue()>=tempInt.intValue()){
                        al.add(j,tempInt);
                        MaxSize++;
                        System.out.println(al.toString());
                        break;
                    }
   			 	}
    		}
   		}

    	System.out.println("The ArrayList Sort After:"); 
        for(int i=0;i<al.size();i++) {
    		System.out.println("al["+i+"]="+al.get(i));
    	}
    }

    public static void main(String[] args){
    	InsertSort is = new InsertSort(10,100);
    	is.SortIt();
    }

}
```










JAVA 类实现序例化的方法是实现 java.io.Serializable 接口



#### 16、编程：编写一个截取字符串的函数，输入为一个字符串和字节数，输出为按字节截取的字符串。 但是要保证汉字不被截半个，如"我 ABC"4，应该截为"我 AB"，输入"我 ABC 汉 DEF"，6，应该输出为"我 ABC"而不是"我 ABC+汉的半个"。



```java
public static void split(String source,int num) throws Exception{
    int k=0;
    String temp="";
    for (int i = 0; i <source.length(); i++){
		byte[] b=(source.charAt(i)+"").getBytes();
		k=k+b.length;
		if(k>num){
			break;
		}
		temp=temp+source.charAt(i);
	}
	System.out.println(temp);
}
```



#### 15、Java 编程,打印昨天的当前时刻

```java
public class YesterdayCurrent{

	public void main(String[] args){
        Calendar cal = Calendar.getInstance();
        cal.add(Calendar.DATE, -1);
        System.out.println(cal.getTime());
    }

}
```

#### 16、文件读写,实现一个计数器

```java
public int getNum(){
	int i = -1;
	try{
		String stri="";
		BufferedReader in = new BufferedReader(new FileReader(f)); 	
        Swhile((stri=in.readLine())!=null){ 
            i = Integer.parseInt(stri.trim());
		}
		in.close();
	}catch(Exception e){
    	e.printStackTrace();
	}
	return i;
}

public void setNum(){
    int i = getNum();
    i++;
    try{

        PrintWriter out=new PrintWriter(new BufferedWriter(new FileWriter(f,false))); 
        out.write(String.valueOf(i)); //可能是编码的原因，如果直接写入 int 的话，将出现 java编码和 windows 编码的混乱，因此此处写入的是 String out.close() ;
    }catch(Exception e){
   		 e.printStackTrace();
    }
}
```



#### 17、指出下面程序的运行结果。

```java
class A{
    static{
    	System.out.print("1");
    }
    public A(){
    	System.out.print("2");
    }
}

class B extends A{
    static{
    	System.out.print("a");
    }
    public B(){
    	System.out.print("b");
    }
}

public class Hello{
    public static void main(String[] ars){
        A ab = new B(); //执行到此处,结果: 1a2b
        ab = new B(); //执行到此处,结果: 1a2b2b
    }
}

注:类的 static 代码段,可以看作是类首次加载(被虚拟机加载)执行的代码,而对于类的加载,首先要执行其基类的构造,再执行其本身的构造
```



#### 18、抽象类和接口的区别？

1. 接口可以被多重 implements,抽象类只能被单一 extends

2. 接口只有定义,抽象类可以有定义和实现

3. 接口的字段定义默认为:public static final, 抽象类字段默认是"friendly"(本包可见)

   当功能需要累积时用抽象类，不需要累积时用接口。

#### 19、什么是类的返射机制?


通过类(Class 对象)，可以得出当前类的 fields、method、construtor、interface、superClass、modified 等，同是可以通过类实例化一个实例、设置属性、唤醒方法。 Spring 中一切都是返射、struts、hibernate 都是通过类的返射进行开发的。

#### 20、类的返射机制中的包及核心类?

```java
java.lang.Class
java.lang.refrection.Method 
java.lang.refrection.Field
java.lang.refrection.Constructor
java.lang.refrection.Modifier
java.lang.refrection.Interface
```

#### 21、得到 Class 的三个过程是什么?

1. 
   对象.getClass()

2. 类.class 或 Integer.type(int)	Integer.class(java.lang.Integer)

3. Class.forName();


#### 22、如何唤起类中的一个方法？


产生一个 Class 数组，说明方法的参数

通过 Class 对象及方法参数得到 Method

通过 method.invoke(实例,参数值数组)唤醒方法

#### 23、如何将数值型字符转换为数字（Integer，Double）？

```java
Integer.parseInt(“1234”)
Double.parseDouble(“123.2”)
```



#### 24、如何将数字转换为字符？

```java
double dou1 = 2.333;

//第一种方式通过ToString() 方法, Double 就是一个包装类
String s1 = Double.toString(dou1);

//第二种方式是通过valueof() 方法, 本质上还是调用 toString() 方法
String s2 = String.valueOf(dou1);

//第三种没有借助包装类
String s3 =""+dou1;
```

#### 25、如何去小数点前两位，并四舍五入。

```java
double d=1256.22d;
d=d/100;
System.out.println(Math.round(d)*100);
```



#### 26、如何取得年月日，小时分秒？

```java
Calendar c=Calendar.getInstance();
c.set(Calendar.YEAR,2004);
c.set(Calendar.MONTH,0);
c.set(Calendar.DAY_OF_MONTH,31);
System.out.println(c.get(Calendar.YEAR)+" "+(c.get(Calendar.MONTH)+1)+"	"+c.get(Calendar.DAY_OF_MONTH));
```



#### 27、如何取得从 1970 年到现在的毫秒数

```java
Java.util.Date dat=new Date();
long now=dat.getTime();
```



#### 28、如何获取某个日期是当月的最后一天？


当前日期加一天，若当前日期与结果的月份不相同，就是最后一天。

取下一个月的第一天，下一个月的第一天-1

```java
public static void main(String[] args){

    Calendar c=Calendar.getInstance(); 
    c.set(Calendar.YEAR,2004);
    c.set(Calendar.MONTH,0); 
    c.set(Calendar.DAY_OF_MONTH,30); 
    Calendar c1=(Calendar)c.clone();
    System.out.println(c.get(Calendar.YEAR)+" "+(c.get(Calendar.MONTH)+1)+" "+c.get(Calendar.DAY_OF_MONTH));
	c.add(Calendar.DAY_OF_MONTH,1);
    if(c.get(Calendar.MONTH)!=c1.get(Calendar.MONTH)) {
    	System.out.println("是最后一天");
    }else{
    	System.out.println("不是取后一天");
    }
}
```



#### 29、如何格式化日期？

```java
Import java.text.SimpleDateFormat;

SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
Date dat=new Date();

//把日期转化为字符串
String str=sdf.format(dat);

System.out.println(str);

//将字符串转化为日期
Java.util.Date d1=sdf.parse(“yyyy-mm-dd”);
```



#### 30、编码转换，怎样实现将 GB2312 编码的字符串转换为 ISO-8859-1 编码的字符串。

```java
String a=new String("中".getBytes("gb2312"),"iso-8859-1");
String a=new String("中".getBytes("iso-8859-1"));
```



#### 32、String s = new String("xyz");创建了几个 String Object?


New 了一个,”XYZ”本来又是一个

两个

#### 33、float 型 float f=3.4 是否正确?

- 
  报错，应当是 float f=3.4f

- 如果是 float f=3(整数)正确


#### 35、说出一些常用的类，包，接口，请各举 5 个		

常用的类： BufferedReader   BufferedWriter	FileReader	FileWirter   String
Integer				
常用的 包： java.lang	java.awt	java.io	java.util	java.sql  javax.xml
javax.sevlet javax.ejb.	java.net	javax.faces	
常用的接口：  List   Map	Document	NodeList EjbObject  EjbHome  SessionBean
EntityBean				

#### 36、java 中会存在内存泄漏吗，请简单描述。		

会。如：int i,i2;  return (i-i2);	//when i 为足够大的正数,i2 为足够大的负数。
结果会造成溢位，导致错误。			

#### 37、java 中实现多态的机制是什么？


静态的多态: 方法名相同，参数个数或类型不相同。(overloading)

动态的多态: 

子类覆盖父类的方法，将子类的实例传与父类的引用调用的是子类的方法实现接口的实例传与接口的引用调用的实现类的方法。

#### 38、垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？


动态内存   存放类实例

静态内存   类本身

垃圾收集主要针对的是动态内存，一般当内存不够用时会进行垃圾收集。

或通过 System.gc()手动收集，但不保证一定执行。

#### 39、静态变量和实例变量的区别？


static i = 10; //类变量，在类中的只有一个

class A a;	a.i =10;//实例变量

静态方法可以调用静态变量。

实现方法可以调用静态变量、实例变量

#### 41、是否可以从一个 static 方法内部发出对非 static 方法的调用？


不可以,如果其中包含对象的 method()；不能保证对象初始化.

#### 42、写 clone()方法时，通常都有一行代码，是什么？


Clone 有缺省行为，super.clone();他负责产生正确大小的空间，并逐位复制。



#### 43、JAVA 语言如何进行异常处理，关键字：throws,throw,try,catch,finally 分别代表什么意义？在 try 块中可以抛出异常吗？

- 
  try:执行部分，产生异常

- catch:捕捉异常

- finally:不管有没有异常都执行

- throws:在方法声明处声明要抛出的异常，调用者必须对其进行处理。

- throw:抛出一个异常


在 try 中可以抛出异常，一般与声明的异常相同。

自定义异常要继承于 Exception 或 Exception 的子类

#### 45、冒泡排序法

```java
//相邻两个数比较，将最小或最大的放到后面，最后面数的不参与比较
public class BubbleSort {

    private static int al[] = new int[10]; public BubbleSort() {
        al[0]=2;
        al[1]=3;
        al[2]=23;
        al[3]=45;
        al[4]=1;
        al[5]=67;
        al[6]=23;
        al[7]=80;
        al[8]=35;
        al[9]=72;
    }

    public static void main(String[] args) { 
        BubbleSort bs = new BubbleSort();
    	System. out.println("排序前：");
    	display(al);
    	for(int i=0;i< al.length;i++) {
    		for (int j = 0; j < al.length-i-1; j++) {
    			if(al[j]> al[j+1]) {
    				swap(j,j+1);
    			}
    		}
    	}
    	System. out.println();
    	System. out.println("排序后：");
    	display(al);
    }

    private static void display(int[] al2) { 
        for (int i = 0; i < al2.length; i++) {
    		System. out.print(al2[i]+"	");
   		}
    }

    private static void swap(int i, int j) {
        int temp = al[i];
        al[i]=  al[j];
        al[j] = temp;
    }

}
```



#### 46、String and StringBuffer 的区别？


String:长度给定不可变，当多个字符串联合时要先转为StringBuffer，再联合，速度慢。

StringBuffer:长度可变,可以将多个字符串值直接联合，效率高



#### 47、用 java 代码编写堆栈

```java
public class Stack {

    int[] data;
    int maxSize;
    int top;

	public Stack(int maxSize) {
		this.maxSize = maxSize;
		data = new int[maxSize];
		top = -1;
	}

    /**
    *	依次加入数据
    *	@param data 要加入的数据
    *	@return 添加是否成功
    */
    public boolean push(int data) { 
        if(top+1== maxSize) {
    		System. out.println("栈已满!"); 
            return false;
    	}
        this.data[++top] = data;
        return true;
	}

    /**
    *	从栈中取出数据
    *	@return 取出的数据
    */
    public int pop() throws Exception{

    	if(top==-1) {
    		throw new Exception("栈已空!");
    	}
    	return this.data[top--];
    }

    public static void main(String[] args) throws Exception { 
        Stack stack=new Stack(1000);
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);
        stack.push(5);
        while(stack.top>=0)
        {
        	System. out.println(stack.pop());
        }

    }

}
```



#### 48、集合的作用是什么?


数据的传送 增、删、改、查、constainsAll，可以存放不同类型的对象。

#### 49、集合的通用方法有那些?通用方法是什么?(操作)


集合 List 的遍历方法有：

Iterator:

Enumeration

For

Get

set

Collection 的通用方法有：

Iterator()

Add()

Clear();

remove()



#### 50、说出 ArrayList,Vector, LinkedList 的存储性能和特性 HashMap 和 Hashtable的区别


ArrayList Vector:以数组的方式存储，增、删慢，查、改快

ArrayList:线程不安全，速度快

Vector:线程安全，速度慢(synchoronized)

LikedList: 以单链表的方式存储，增、删快，查、改慢

HashMap 与 Hashtable 都实现的 Map 接口,HashTable 线程安全，HashMap 线程不安全。

#### 51、Collection 和 Collections 的区别。


Collection 是集合的根接口，其下有 set 及 list Collections 是集合的算法。

#### 52、Set 里的元素是不能重复的，那么用什么方法来区分重复与否呢? 是用==还是equals()? 它们有何区别?用 contains 来区分是否有重复的对象。还是都不用。



在比较时先调用 hashCode 方法，如果不相同，证明不相等。

如果相同，再调用 equals 方法，如果 equals 方法相同，证明相等，不相同，证明不相等。

==:主要用在基本数据类型及引用

equals:主要是对象或对象引用的比较。

集合中是否包含某一个元素用 contains 来判断。

#### 53、List, Set, Map 是否继承自 Collection 接口?


List,set 继承于 Collection

Map 没有继承于 Collection，其相对是独立的。

属于 Collection 类型的对象，可以通过构造函数将一个集合构造成另外一个集合。

#### 54、面向对象的特征有哪些方面


1.抽象：

找共性，将共有的属性、方法放到父类中

2.继承：

子类继承于父类，具有父类的所有属性与方法，可以重用，也可以覆盖。

3.封装：

一个类包括多个属性及方法。

4.	多态性：

动态:

静态:

#### 55、String 是最基本的数据类型吗?


基本数据类型包括 byte、int、char、long、float、double、boolean 和 short。


java.lang.String 类是 final 类型的，因此不可以继承这个类、不能修改这个类。为了提高效率节省空间，我们应该用 StringBuffer 类

#### 56、int 和 Integer 有什么区别？


Int 是基本数据类型，不是对象，占一个内存空间，没有方法。与其同类的有

long,char,doble

Integer 是封装类，具有方法及属性。与其同类的有 Long,Double.Float



#### 57、运行时异常与一般异常有何异同？


运行时异常:java JVM 抛出的异常，代码中不用处理。


一般异常:用户抛出的异常，如果用 throws 声明了，调用这个方法的代码必须对其处理。

#### 58、&和&&的区别？


&:与: 左边若为 false 右边还执行。

&&:短路与,左边若为 false 右边不执行。

#### 59、final, finally, finalize 的区别？


final 用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继

承。

finally 是异常处理语句结构的一部分，表示总是执行。

finalize 是 Object 类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源回收，例如关闭文件等。算符可以用来决定某对象的类是否实现了接口。

#### 62、heap 和 stack 有什么区别？


栈是一种线形集合，其添加和删除元素的操作应在同一段完成。栈按照后进先出的方式进行处理。

堆是栈的一个组成元素



#### 63、Static Nested Class 和 Inner Class 的不同？

Static Nested Class 是被声明为静态（static）的内部类，它可以不依赖于外部类实例被实例化。而通常的内部类需要在外部类实例化后才能实例化。

#### 64、什么时候用 assert？


assertion (断言)在软件开发中是一种常用的调试方式，很多开发语言中都支持这种机制。在实现中，assertion 就是在程序中的一条语句，它对一个 boolean 表达式进行检查，一个正确程序必须保证这个 boolean 表达式的值为 true；如果该值为 false，说明程序已经处于不正确的状态下，系统将给出警告或退出。一般来说，assertion 用于保证程序最基本、关键的正确性。assertion 检查通常在开发和测试时开启。为了提高性能，在软件发布后，assertion 检查通常是关闭的。

#### 65、GC 是什么? 为什么要有 GC?


GC 是垃圾收集的意思（Gabage Collection）,内存处理是编程人员容易出现问题的地方，忘记或者错误的内存回收会导致程序或系统的不稳定甚至崩溃，Java 提供的 GC 功能可以自动监测对象是否超过作用域从而达到自动回收内存的目的， Java 语言没有提供释放已分配内存的显示操作方法。

#### 66、short s1 = 1; s1 = s1 + 1;有什么错? short s1 = 1; s1 += 1;有什么错?


short s1 = 1; s1 = s1 + 1; （s1+1 运算结果是 int 型，需要强制转换类型） short s1 = 1; s1 += 1;（可以正确编译）

#### 67、Math.round(11.5)等於多少? Math.round(-11.5)等於多少?


Math.round(11.5)==12 Math.round(-11.5)==-11 round 方法返回与参数最接近的长整数，参数加 1/2 后求其 floor.



#### 68、Java 有没有 goto?


java 中的保留字，现在没有在 java 中使用。



#### 69、给我一个你最常见到的 runtime exception


ArithmeticException,	ArrayStoreException,	BufferOverflowException,

BufferUnderflowException,	CannotRedoException,	CannotUndoException,

ClassCastException,	CMMException,	ConcurrentModificationException,

DOMException,	EmptyStackException,	IllegalArgumentException,

IllegalMonitorStateException,	IllegalPathStateException,

IllegalStateException,	ImagingOpException,	IndexOutOfBoundsException,

MissingResourceException, NegativeArraySizeException, NoSuchElementException,

NullPointerException,	ProfileDataException,	ProviderException,

RasterFormatException,	SecurityException,	SystemException,

UndeclaredThrowableException,	UnmodifiableSetException,

UnsupportedOperationException

一般异常:

IOException

FileNotFoundException

SqlException



#### 70、接口是否可继承接口? 抽象类是否可实现(implements)接口? 抽象类是否可继承

实体类(concrete class)?


接口可以继承接口。抽象类可以实现(implements)接口，抽象类可继承实体类。

#### 71、abstract 的 method 是否可同时是 static,是否可同时是 native，是否可同时synchronized?


都不能

#### 72、数组有没有 length()这个方法? String 有没有 length()这个方法？


数组没有 length()这个方法,有 length 这个属性

String 有 length()这个方法.

#### 73、构造器 Constructor 是否可被 override?


构造器 Constructor 不能被继承，因此不能重写 Overriding ，但可以被重载Overloading。

#### 74、是否可以继承 String 类?


String 类是 final 类故不可以继承。

#### 75、swtich 是否能作用在 byte 上，是否能作用在 long 上，是否能作用在 String 上?

switch（expr1）中，expr1 是一个整数表达式。

Java 7 中加入了对String类型的支持。所以支持的有：char、byte、short、int 和 Character、Byte、Short、Integer 和 String。

Java 7 中加入了对String类型的支持，这个新特性是在编译器这个层次上实现的。而在Java虚拟机和字节码这个层次上还是只支持在switch语句中使用与整数类型兼容的类型。这么做的目的就是为了减少这个特性所影响的范围，以降低实现的代价。在编译器层次实现的含义是，虽然开发人员在Java源代码的switch语句中使用了字符串类型，但是在编译的过程中，编译器会根据源代码的含义进行转换，将字符串类型转换成与整数类型兼容的格式。不同的Java编译器可能采用不同的方式来转换，并采用不同的优化策略。比如：如果switch语句中只包含一个case语句，那么就可以简单的将其转换成一个if语句。如果包含一个case和一个default语句，就可以转换成if-else语句。而对于复杂的情况（多个case语句），也可以转换成Java 7 之前的switch语句，只不过使用字符串的哈希值作为switch语句表达式的值。经过转换，Java 虚拟机看到的仍然是与整数类型兼容的类型。这里要注意的是，在case字句中对应的语句块中仍然需要使用String的equals方法来进行字符串比较，这是因为哈希函数在映射的时候可能存在冲突，这样更加保险了。

#### 76、try {}里有一个 return 语句，那么紧跟在这个 try 后的 finally {}里的 code 会不会

被执行，什么时候被执行，在 return 前还是后?


会执行，在 return 前执行。

#### 77、编程题: 用最有效率的方法算出 2 乘以 8 等於几?


2 << 3



#### 78、两个对象值相同(x.equals(y) == true)，但却可有不同的 hash code，这句话对不对?

Java 对于eqauls 方法和 hashCode 方法是这样规定的：

(1)如果两个对象相同（equals 方法返回 true），那么它们的hashCode 值一定要相同；

(2)如果两个对象的 hashCode 相同，它们并不一定相同。

#### 79、当一个对象被当作参数传递到一个方法后，此方法可改变这个对象的属性，并可返回变化后的结果，那么这里到底是值传递还是引用传递?


是引用传递

基本数据类型:值

对象: 引用

#### 80、四种会话跟踪技术


Cookie

Session

Hidden

url 重写

#### 81、编程题: 写一个 Singleton 出来。


Singleton 模式主要作用是保证在 Java 应用程序中，一个类 Class 只有一个实例存在。

一般 Singleton 模式通常有几种种形式:

第一种形式: 定义一个类，它的构造函数为 private 的，它有一个 static 的 private 的该类变量，在类初始化时实例话，通过一个 public 的 getInstance 方法获取对它的引用,继而调用其中的方法。

public class Singleton {

private Singleton(){}

//在自己内部定义自己一个实例，是不是很奇怪？

//注意这是 private 只供内部调用

private static Singleton instance = new Singleton();
//这里提供了一个供外部访问本 class 的静态方法，可以直接访问 public static Singleton getInstance() {

return instance;

}

}

第二种形式:

public class Singleton {

private static Singleton instance = null;

public static synchronized Singleton getInstance() { //这个方法比上面有所改进，不用每次都进行生成对象，只是第一次//使用时生成实例，提高了效率！ if (instance==null)

instance＝new Singleton();

return instance;	}

}

其他形式:

定义一个类，它的构造函数为 private 的，所有方法为 static 的。

一般认为第一种形式要更加安全些

#### 83、Java 中的异常处理机制的简单原理和应用。


原理

有错直接转到异常处理部分或向上抛出。

应用:

JAVA 的异常就是错误，有两种一种是运行时，编码可以不用捕捉。一种是一般异常，如果 throws 声明了，必须进行处理。

#### 84、垃圾回收的优点和原理。并考虑 2 种回收机制。


优点:

程序员不用管内存，jvm 自动完成，开发方便。运行优先非常低，程序无法清楚实例什么时候被消毁。



#### 85、描述一下 JVM 加载 class 文件的原理机制?


JVM 中类的装载是由 ClassLoader 和它的子类来实现的,Java ClassLoader 是一个重要的 Java 运行时系统组件。它负责在运行时查找和装入类文件的类。

#### 86、char 型变量中能不能存贮一个中文汉字?为什么?


能够定义成为一个中文的，因为 java 中以 unicode 编码，一个 char 占 16 个字节，所以放一个中文是没问题的



#### 88、写一个程序，从文件（c:\test.txt）中查出字符串”mobnet”出现的次数？