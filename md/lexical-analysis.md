# 词法分析

[TOC]

## 编译器阶段

![](img/lexical-analysis-pic0.png)


前端：
![](img/lexical-analysis-pic1.png)

## 词法分析器

### 从字符流到记号流

一段c源程序如下

```cpp
if (x > 5) //这里有\n回车
	y = "hello";
else
	z = 1; //EOF
```

词法分析器将这段c源程序切分为一个个单词，空格被扔掉。
这里，字符串`"hello"`作为一个整体，两个引号和hello不会被切分。
切分之后得到记号/单词流

```bash
if lparen ident(x) gt int(5) rparen
	ident(y) assign string("hello") semicolon
else
	ident(z) assign int(1) semicolon eof
```

从字符流到记号流有两个重要问题要解决：

1. 记号数据结构的定义
2. 字符流转化为记号流的算法

### 记号的数据结构定义

如用C实现

```cpp
enum kind {IF, LPAREN, ID, INTLIT, ...}; //一个名为kind的枚举类型
//从IF开始，所有类型的值被编码为一个整型数0,1,2,3...是对词法分析器所能实现的所有类型的值的分类
struct token{
	enum kind k;
	char *lexeme; //所识别出的单词的具体的值,如果为0代表未赋任何值
};

```

例如, `if (x > 5)`,所对应的token的伪代码是

```cpp
token{k=IF, lexeme=0};
token{k=LPAREN, lexeme=0};
token{k=ID, lexeme="x"};
...
```

## 词法分析器的手工编码实现

### 两种实现方法
1. 手工编码 (gcc, LLVM ...)
2. 词法分析器的生成器(可快速原型, 代码量较少； 但较难控制细节)

### 转移图

如有关系运算符: <=, <>, <, =, >=, >
数字n代表n号状态，*代表字符回滚
![](img/lexical-analysis-pic2.png)

转移图算法如下

```cpp
token nextToke(){
	c = getChar();
	switch(c){
		case '<' : {
			c = getChar();
			switch(c){
				case '=' : return LE;
				case '>' : return NE;
				default : {rollback(); return LT;}
			}
			case '=' : return EQ;
			case '>' : ...//similar
		}
	}
}
```

标识符(ID)的转移图/算法类似
![](img/lexical-analysis-pic3.png)

***
标识符和关键字？
很多语言中，标识符和关键字有交集。从词法分析的角度看，关键字是标识符的一部分。

如，以c语言为例，关键字也满足标识符的词法规则<font color="grey">以字母或下划线开头，后跟0个或多个字母，下划线或数字</font>。
所以，识别关键字可以在识别标识符的基础上增添特殊情况。
![](img/lexical-analysis-pic4.png)

关键字识别还有一种算法：关键字表算法

1. 对给定语言中所有的关键字，构造关键字构成的哈希表H <font color="grey">关键字是有限的，确定的</font>
2. 对所有的标识符和关键字，先按统一标识符的转移图进行识别
3. 识别完成后，进一步查表H看是否是关键字

哈希表的作用是，让查表操作快速完成。通过合理地构造哈希表(完美哈希)，可以在O(1)时间完成。
***

## 词法分析器自动生成

声明式的规范 -> 自动生成工具(如lex, flex, jlex) -> 词法分析器

这样，就把写代码的工作化简为写声明式的规范，即正则表达式。

### 正则表达式RE
定义：
![](img/lexical-analysis-pic5.png)
字符集取决于要编译的语言，如c语言，字符集为ascii; java, 字符集为unicode.
闭包(Kleene 闭包)是一元算符，MM用了连接。

例子：用正则表达式表示c语言中的标识符
`(a|b|c|...|A|B|...|Z|_)(a|b|c|...|A|B|...|Z|_|0|1|...|9)*`

***
**语法糖 Syntactic sugar**
引入*语法糖*，简化构造

```
[c1-cn] == c1|c2|...|cn
e+ == 一个或多个e
e? == 零个或一个e
"a*" == a*自身，不是a的Kleen闭包
e{i,j} == i到j个e的连接
. == 除'\n'外的任意字符

实际上，所有的运算都可用**赋值**和**跳转**完成(汇编)。高级语言的语法实际上都是语法糖。是对这两种运算的不同封装，以方便代码的开发和维护。
```

***

### 有限状态自动机FA

用来描述生成的状态。

输入的字符串 -> FA -> {Yes, No}
是否能识别输入的字符串，若能，输出Yes; 否则，输出No

可用五元组M描述有限状态自动机FA
![](img/lexical-analysis-pic6.png)
字母表是能识别的字符的集合。
状态集指有FA的状态。
转移函数描述了自动机在给定串的驱动下是如何工作的。(wiki: 转移函数是用来拟合或描述黑箱模型（系统）的输入与输出之间关系的数学表示。)

一个确定有限状态自动机**DFA**(<font color="green">对所有状态，对于给定字符，状态转移是单元素的集合</font>)的例子
![](img/lexical-analysis-pic7.png)

Σ = {a, b}
S = {0, 1, 2}
q0 = 0 <font color="green">起始状态，图上有单项箭头指向的状态</font>
F =  {2} <font color="green">终结/接受状态，是集合，图上有双圈的状态</font>

转移函数：

```
{(q0,a)->q1, (q0,b)->q0,
(q1,a)->q2, (q1,b)->q1,
(q2,a)->q2,(q2,b)->q2}
```

一个非确定有限状态自动机的例子**NFA**
![](img/lexical-analysis-pic8.png)
转移函数：

```
{(q0,a)->{q0,q1},
(q0,b)->{q1},
(q1,b)->{q0,q1}}
```

对于NFA来说，对于给定的串，只要某一中走法能到终结状态，就说该串能被**接受**。
所以在NFA上是否能接受，需要遍历的过程。所以，经常把NFA转化为与其等价的DFA，方便判断。
词法分析器是DFA

RE -(Thompson算法)-> NFA -(子集构造算法)-> DFA -(Hopcroft最小优化算法)-> 词法分析器代码

### RE -> NFA: Thompson算法

**Thompson算法**

Thompson算法是基于归纳的算法：

- 对于基本的RE(2种)直接构造
- 对于符合的RE(3种)递归构造

RE:(5种)

```
(1) e -> ε
(2) -> c
(3) -> e1 e2
(4) -> e1 | e2
(5) -> e1*
```
![](img/lexical-analysis-pic9.png)

例子：`((ab)|c)*`

![](img/lexical-analysis-pic10.png)

### NFA -> DFA: 子集构造算法

`a(b|c)*`

对应的NFA：
![](img/lexical-analysis-pic11.png)

要构造与其等价的**DFA**(不包括ε边)：


> 1. n0 -(a)->n1</br> n0 -(a)->n1,n2,n3,n4,n6,n9 </br><font color="green">n0读入字符a，所能走到的所有节点。将其记为集合q1:{n1,n2,n3,n4,n6,n9}。由于读入a后，可以走到这些节点，所以把q1叫做一个边界。将n0记为q0.</font>
>2. q1 -(b <font color="green">考虑q1中所有节点是否可以接受b</font>)->n5  <font color="blue">在原来的NFA上看接受一个字符b后能做到哪些节点，该操作记为delta(q)</font> </br> q1 -(b)-> q2:{n5,n8,n9,n3,n4,n6} <font color="blue">在进行了delta(q)操作后，对与每个元素求ε边界，该过程称为ε-闭包</font>
>3. q2 -> {...}
> <font color="green">由于原NFA中n9为接受状态，所以在新的DFA中，有n9的都是接受状态。</font>

子集构造算法是**不动点算法(fixed point algorithm)**。
时间复杂度最坏情况

$ J_\alpha(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha} \text {，行内公式示例} $

