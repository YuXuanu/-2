# 关于java语言中的package和import机制

## 为什么要使用package？

​	package是java中包机制，方便程序的管理，不同功能的类分别放在不同的包下。

## package怎么用？

​	package是一个关键字，后面加包名，例如：

```java
package com.bjpowernode.javase.chapter17;
```

​	**注意**：package语句只允许出现在java源代码的第一行

## 包名的命名规范

​	一般采用公司域名倒叙的方式（因为公司域名具有全球唯一性），即：公司域名倒叙+项目名+模块名+功能名

## 对于带有package的java程序怎么编译和运行？

​	当使用了包机制后，类名将会改变。例如原类名为HelloWorld，现在则变成了：com.bjpowernode.javase.chapter17.HelloWorld。因此采用之前的编译和运行不行了。

​	编译：  javac -d . HelloWorld.java
​	解释一下：
​		-d  带包编译
​		.  代表编译之后生成的东西放到当前目录下（点 代表当前目录）

​	运行：java com.bjpowernode.javase.chapter17.HelloWorld
​	**注意**：此名字要求全部写进去，不能切换到javase或者chapter17等目录下再直接HelloWorld运行。

## 关于import的使用

​	不在同一个包下的时候，我们会使用import导包以简化程序。
​	import语句只能出现在package语句之下，class声明语句之上。
​	例如：

```java
import com.bjpowernode.javase.chapter17.HelloWorld
//或者
import com.bjpowernode.javase.chapter17.*
```

