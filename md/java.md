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
`javac -d classes src/xxx.java`
`-d`参数后跟class文件的输出目录，如果没有-d参数会在当前目录下生成class文件，而且没有根据包名建立相应的目录

如果主类中import了工具类，需要同时编译，比如
`javac -d classes src/*.java`

----
- javac: Java compiler
- java: Java Virtual Machine
----

Linux下为UTF-8编码，javac编译gbk编码的java文件时，容易出现“错误: 编码UTF8的不可映射字符”

解决方法是添加encoding 参数：`javac -encoding gbk WordCount.java`

### 运行class文件

`java -classpath classes test.ant.HelloWorld`
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

## java makefile



这是来自https://www.cnblogs.com/jiqingwu/archive/2012/06/13/java_makefile.html的一份通用makefile

'''bash
 # A general java project makefile
# Author: Wu Jiqing (jiqingwu@gmail.com)
# create: 2012-06-12
# update: 2012-06-13
# version: 0.7

# 设置你要生成的jar包的文件名
# Set the file name of your jar package:
JAR_PKG = a.jar
# 设置你的项目的入口点
# Set your entry point of your java app:
ENTRY_POINT = test.A
# 是否需要res目录，如果你的程序有图片、文档等，
# 最好放入res目录中。
# yes: 需要；no：不需要
RES_DIR = yes
# 设置你项目包含的源文件
# 如果你使用了package，请自己在src下建立相应的目录层次，
# 并将源文件放在对应的目录中。
# 如你要生成的一个类是 com.game.A，
# 那么你的源文件应该是 com/game/A.java。
# 多个类之间用空格间隔，如果一行太长，用'\'换行，
# 建议一行一个。
# 另外注意顺序，如果class A 引用 class B，那么B.java应该放在A.java前。
SOURCE_FILES = \
test/B.java \
test/A.java

# 设置你的java编译器
# Set your java compiler here:
JAVAC = javac
# 设置你的编译选项
JFLAGS = -encoding UTF-8

# 用法：
# make new: 在你的工程目录下生成src, bin, res子目录。
# 如果你定义的类包含在某个包里：请自己在src下建立相应的目录层次。
# 最终的目录结构如下：
# ├── a.jar
# ├── bin
# │     └── test
# │             ├── A.class
# │             └── B.class
# ├── makefile
# ├── res
# │     └── doc
# │            └── readme.txt
# └── src
#        └── test
#                ├── A.java
#                └── B.java

# make build: 编译，在bin目录下生成 java classes。
# make clean: 清理编译结果，以便重新编译
# make rebuild: 清理编译结果，重新编译。
# make run: make 之后，可以通过make run查看运行结果。
# make jar: 生成可执行的jar包。

#############下面的内容建议不要修改####################

vpath %.class bin
vpath %.java src

# show help message by default
Default:
    @echo "make new: new project, create src, bin, res dirs."
    @echo "make build: build project."
    @echo "make clean: clear classes generated."
    @echo "make rebuild: rebuild project."
    @echo "make run: run your app."
    @echo "make jar: package your project into a executable jar."

build: $(SOURCE_FILES:.java=.class)

# pattern rule
# 不能处理两个类互相引用的情况，尽量避免
%.class: %.java
    $(JAVAC) -cp bin -d bin $(JFLAGS) $<

rebuild: clean build

.PHONY: new clean run jar

new:
ifeq ($(RES_DIR),yes)
    mkdir -pv src bin res
else
    mkdir -pv src bin
endif

clean:
    rm -frv bin/*

run:
    java -cp bin $(ENTRY_POINT)

jar:
ifeq ($(RES_DIR),yes)
    jar cvfe $(JAR_PKG) $(ENTRY_POINT)  -C bin . res
else
    jar cvfe $(JAR_PKG) $(ENTRY_POINT) -C bin .
endif
'''

make new: 新建工程，在当前目录下生成src, bin, res（如果 RES_DIR = yes）子目录，类似Eclipse项目的目录层次。java源文件放 在src目录下，生成的class放在bin目录下。
make build: 编译工程。
make clean: 清除生成的class，以便重新编译。
make rebuild: 重新编译工程，相当于make clean; make build。
make run: 运行编译生成的应用。
make jar: 生成可执行的jar包。
make: 显示帮助信息。

## java中的xml

1. xml作为数据储存(很少)
2. 存放配置信息

IDEA的maven项目中，默认源代码目录下（src/main/java目录）的xml等资源文件并不会在编译的时候一块打包进classes文件夹，而是直接舍弃掉。如果使用的是Eclipse，Eclipse的src目录下的xml等资源文件在编译的时候会自动打包进输出到classes文件夹。

