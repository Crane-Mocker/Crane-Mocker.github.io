# 杂七杂八的java笔记


<!-- vim-markdown-toc GFM -->

* [reference](#reference)
* [脱离IDE编译java](#脱离ide编译java)
	* [工程目录](#工程目录)
	* [编译](#编译)
* [- java: Java Virtual Machine](#--java-java-virtual-machine)
	* [运行class文件](#运行class文件)
	* [打包jar](#打包jar)
	* [运行jar](#运行jar)
* [java中的xml](#java中的xml)

<!-- vim-markdown-toc -->

## reference

> https://blog.csdn.net/lvshaorong/article/details/73881568
> https://blog.csdn.net/yeqiuBOke/article/details/80897611
> https://users.soe.ucsc.edu/~eaugusti/archive/102-winter16/misc/howToCompileAndRunFromCommandLine.html
> https://www.cnblogs.com/by-1075324834/p/5558035.html

## 脱离IDE编译java

### 工程目录

`根目录/`下
- `src/` 存放源代码
-  `classes/`存放编译好的class

### 编译

简单地在同一path下编译：
- 单个文件: `javac file.java`
- 多个文件: `javac YourSourceFile.java`
- 该dir中所有java files: `javac *.java`
- 使用compiler flags: `javac -Xlint:unchecked SourceFile.java` (多文件和通配符也可使用该参数)


编译单个文件：
`javac -d ./classes ./src/xxx.java`
`-d`参数后跟class文件的输出目录，如果没有-d参数会在当前目录下生成class文件，而且没有根据包名建立相应的目录

如果主类中import了工具类，需要同时编译，比如
`javac -d ./classes ./src/*.java`

----
- javac: Java compiler
- java: Java Virtual Machine
----

### 运行class文件

`java -classpath .\classes test.ant.HelloWorld`
-classpath参数规定class文件的搜索范围，并指明程序主入口

不使用: -classpath
`java ClassName`
the file name specified must be a .class file that contains a main method

运行类时，不用加.class。
比如有一个类Hello.class，运行命令是`java Hello`而不是`java Hello.class` 。运行机制中是寻找类，而不是像编译的时候那样找到某个文件。

### 打包jar

`cd classes`
使jar包打出来之后最外层文件夹是属于包名的，不然会报错找不到类
`jar -cvf xxx.jar ./*`

打开这个jar,除了`META-INF`之外的木以要是属于包名的目录

### 运行jar

java -jar xxx.jar

## java中的xml

1. xml作为数据储存(很少)
2. 存放配置信息

IDEA的maven项目中，默认源代码目录下（src/main/java目录）的xml等资源文件并不会在编译的时候一块打包进classes文件夹，而是直接舍弃掉。如果使用的是Eclipse，Eclipse的src目录下的xml等资源文件在编译的时候会自动打包进输出到classes文件夹。

