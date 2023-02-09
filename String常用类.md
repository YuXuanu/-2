# String常用类

## String的创建原理

​	先看看一下两行代码：

```java
String s1 = "abcdef";
String s2 = "abcdef"+"xy";
String s3 = new String("xy");
String s4 = "abcdef";
```

![image-20230208141839425](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230208141839425.png)

​	上图是上面代码的内存示意图。
​	所有**带双引号的字符串**自出生起就**不可变**了，因为它们会**在字符串常量池创建对象**，而String类型变量s1和s2中存储的是那些**字符串在常量池中的内存地址**。而且字符串常量池中的字符串**不可重复**，例如上面的**s4和s1将会指向同一个对象**，也就是说它们**保存的内存地址将会是相同的**。

​	而s3与s1，2，4都不相同，它是通过new对象的方式获取的。**凡是new出来的对象都会在堆内存中有一份**。那么**s3中存的就是堆内存中String对象的内存地址**，而堆内存中的对象又会存字符串常量池中的内存地址，所以**归根结底都会在字符串常量池中有一份**。

​	正因为String类型中往往存储的都是内存地址，当我们在比较String类型时要注意不要使用“==”，因为根本没有意义。而要调用equals方法或者是compareTo方法。举例如下：

```java
String s1 = "hello";
Stirng s2 = "hello";
//"hello"存储在字符串常量池中
System.out.println(s1==s2);		//true,因为二者的内存地址相同,双等号只能够比较内存地址。

String x = new String("xyz");
String y = new String("xyz");
System.out.println(x==y);		//false,因为二者存储的是堆内存中不同对象的内存地址。

//所以真正在比较字符串时往往要调用equals()方法
System.out.println(x.equals(y));	//true,因为java里面Stirnig类重写了equals方法，比较的是String底层的Byte数组。

//补充：
String k = new String("testString");
//能不能直接用"testString"这个字符串后面加"."呢？
//可以，因为"testString"是一个字符串对象，只要是对象都能调用方法。
System.out.println("testString".equals(k));		//更建议使用这种方式，因为这个可以避免空指针异常
System.out.println(k.equals("testString"));		//存在空指针异常的风险，不建议这样写
```

## String类中的构造方法

![image-20230208144515683](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20230208144515683.png)

## String类中的实例方法

```java
//1.char charAt(int index)
char c = "中国人".charAt(1);		//传下标，反字符。
System.out.println(c);		//国

//2.int	compareTo(String anotherString)
int result = "abc".compareTo("abc");		//传字符串
System.out.println(c);		//0，表示相等。前面大就是1，前面小就是-1。而且是拿着第一个字母和后面字符串的第一个字母比较，能							//分出胜负就不再比较了。
System.out.println("xyz".compareTo("zyx"));		//-1

//boolean contains(CharSequence s)	是否包含xxx	
System.out.println("HelloWorld.java".contains("World"));	//true

//boolean endsWith(String suffix)	是否以xxx结尾
System.out.println("Test.txt".endsWith(".java"));	//false
System.out.println("Test.txt".endsWith(".txt"));	//true

//boolean equals(Object anObject)	比较两个字符串
System.out.println("abc".equals("abc"));	//true

//boolean equalsIgnoreCase(String anotherString)	比较两个字符串并忽略大小写
System.out.println("ABc".equals("abC"));	//true

//byte[] getBytes()		将字符串对象转换成字节数组
byte[] bytes = "abcdef".getBytes();
for(int i = 0;i < bytes.length;i++){
    System.out.println(bytes[i]);
}

//int indexOf(String str)	返回指定子字符串在字符串内第一次出现处的索引（下标）。
System.out.println("oraclephppythonjavac++mysqlJdbc".indexOf("java"));		//15

//int lastIndexOf(String str)  或  int lastIndexOf(String str, int fromIndex)	返回指定子字符串在字符串内最后一次出现处的索引（下标），fromInt是从什么位置开始检索。

//boolean startsWith(String prefix)		判断是否以xxx开头
//

//String substring(int beginIndex)		通过下标截取字符串
System.out.println("http://www.baidu.com".substring(7));	//www.baidu.com
//String substring(int beginIndex, int endIndex)	有起始位置（包括）和结束位置（不包括）
System.out.println("http://www.baidu.com".substring(7,10));	//www

//boolean isEmpty()		判断某个字符串是否为空串

//int length()		返回其长度

//String replace(char oldChar, char newChar)	替换字符串
String newStirng2 = "name=zhangsan&password=123&age=20".replace("=",":");
System.out.println(newString2);

//String[]	split(String regex)		传分隔符，进行字符串拆分
String[] ymd = "1980-10-11".split("=");
for(int i = 0;i < ymd.length;i++){
    System.out.println(ymd[i]);
}

//char[] toCharArray()		将字符串转换为char数组
char[] chars = "我是中国人".toCharArray();
for(int i = 0;i < ymd.length;i++){
    System.out.println(ymd[i]);
}

//String toLowerCase()		转换为小写
//String toUpperCase()		转换为大写

//String trim()		去除字符串前后空白

//static String	valueOf(boolean b)		唯一一个静态的方法，不需要new对象。里面可以传boolean，int，long，float，double等多种类型，都会将非字符串转换为字符串。
String s1 = String.ValueOf(true);
String s1 = String.ValueOf(100);
String s1 = String.ValueOf(3.14);

String s1 = String.ValueOf(new Customer());		//会自动调用该对象的同String()方法，如果没有重写则会打印此对象的内存地											//址。
											//正如println()方法，在输出一个引用的时候，也会自动调用toString()方法。

```

## StringBuffer和StringBuilder

如果以后需要进行大量的字符串拼接操作，建议使用**java.lang.StringBuffer/StringBuilder类** 。
这样会减少内存空间的浪费。
以下举例：

```java
StringBuffer stringBuffer = new StringBuffer();
stringBuffer.append("a");
stringBuffer.append("b");
stringBuffer.append("c");
stringBuffer.append(3.14);
stringBuffer.append(true);
stringBuffer.append(100L);
System.out.println(stringBuffer.toString());	//这里的toStirng方法会自动调用，可以省略。
```



















