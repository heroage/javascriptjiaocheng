# 入门篇

## 导论

### 1. 什么是 JavaScript 语言

> JavaScript 是一种轻量级的脚本语言。所谓“脚本语言”（script language），指的是它不具备开发操作系统的能力，而是只用来编写控制其他大型应用程序（比如浏览器）的“脚本”。
>
> JavaScript 也是一种嵌入式（embedded）语言。它本身提供的核心语法不算很多，只能用来做一些数学和逻辑运算。JavaScript 本身不提供任何与 I/O（输入/输出）相关的 API，都要靠宿主环境（host）提供，所以 JavaScript 只合适嵌入更大型的应用程序环境，去调用宿主环境提供的底层 API。
>
> 目前，已经嵌入 JavaScript 的宿主环境有多种，最常见的环境就是浏览器，另外还有服务器环境，也就是 Node 项目。
>
> JavaScript 的核心语法部分相当精简，只包括两个部分：基本的语法构造（比如操作符、控制结构、语句）和标准库（就是一系列具有各种功能的对象比如`Array`、`Date`、`Math`等）。除此之外，各种宿主环境提供额外的 API（即只能在该环境使用的接口），以便 JavaScript 调用。以浏览器为例，它提供的额外 API 可以分成三大类。
>
> * 浏览器控制类：操作浏览器
> * DOM 类：操作网页的各种元素
> * Web 类：实现互联网的各种功能
>
> 如果宿主环境是服务器，则会提供各种操作系统的 API，比如文件操作 API、网络通信 API等等。这些你都可以在 Node 环境中找到。
>
> 本书主要介绍 JavaScript 核心语法和浏览器网页开发的基本知识，不涉及 Node。全书可以分成以下四大部分。
>
> * 基本语法
> * 标准库
> * 浏览器 API
> * DOM
>
> 略

## 

## JavaScript 语言的历史

### 3. JavaScript 与 ECMAScript 的关系

> ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现。在日常场合，这两个词是可以互换的。ECMAScript 只用来标准化 JavaScript 这种语言的基本语法结构，与部署环境相关的标准都由其他标准规定，比如 DOM 的标准就是由 W3C组织（World Wide Web Consortium）制定的。

## 

## JavaScript 的基本语法

### 1. 语句

> JavaScript 程序的执行单位为行（line），也就是一行一行地执行。一般情况下，每一行就是一个语句。
>
> 下面都是合法的语句:
>
> ```
> var a = 1 + 3;
> var a = 1 + 3 ; var b = 'abc';
> ;;;
> 1 + 3;
> 'abc';
> ```

### 2. 变量

#### 2.1 概念

> 变量是对“值”的具名引用。变量就是为“值”起名，引用这个名字，就等同于引用这个值。变量的名字就是变量名。

#### 2.2 变量的提升

> JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。
>
> ```
> console.log(a);
> var a = 1;
> ```
>
> 上面代码首先使用console.log方法，在控制台（console）显示变量a的值。这时变量a还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码。
>
> ```
> var a;
> console.log(a);
> a = 1;
> ```
>
> 最后的结果是显示 **undefined**，表示变量 **a 已声明**，但还**未赋值**。

### 3. 标识符

> 标识符（identifier）指的是用来识别各种值的合法名称。最常见的标识符就是变量名，以及后面要提到的函数名。JavaScript 语言的标识符对大小写敏感，所以 a 和 A 是两个不同的标识符。
>
> 标识符有一套命名规则，不符合规则的就是非法标识符。JavaScript 引擎遇到非法标识符，就会报错。
>
> 简单说，标识符命名规则如下:
>
> * 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（$）和下划线（\_）。
> * 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字0-9。
>
> 下面这些都是合法的标识符:
>
> ```
> arg0
> _tmp
> $elem
> π
> ```
>
> 下面这些都是不合法的标识符:
>
> ```
> 1a  // 第一个字符不能是数字
> 23  // 同上
> ***  // 标识符不能包含星号
> a+b  // 标识符不能包含加号
> -d  // 标识符不能包含减号或连词线
> ```
>
> 中文是合法的标识符，可以用作变量名:
>
> ```
> var 临时变量 = 1;
> ```
>
> 另外，JavaScript 有一些保留字不能用作标识符:
>
> > arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。

### 4. 注释

> 源码中被 JavaScript 引擎忽略的部分就叫做注释，它的作用是对代码进行解释。JavaScript 提供两种注释的写法：一种是单行注释，用//起头；另一种是多行注释，放在/\*和\*/之间。
>
> ```
> // 这是单行注释
>
> /*
>  这是
>  多行
>  注释
> */
> ```
>
> 此外，由于历史上 JavaScript 可以兼容 HTML 代码的注释，所以&lt;!--和--&gt;也被视为合法的单行注释。
>
> ```
> x = 1; <!-- x = 2;
> --> x = 3;
> ```
>
> 上面代码中，只有`x = 1`会执行，其他的部分都被注释掉了。
>
> 需要注意的是，`-->`只有在行首，才会被当成单行注释，否则会当作正常的运算。
>
> ```
> function countdown(n) {
>   while (n --> 0) console.log(n);
> }
> countdown(3)
> // 2
> // 1
> // 0
> ```
>
> 上面代码中，n --&gt; 0实际上会当作n-- &gt; 0，因此输出2、1、0。

### 5. 区块

> JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。
>
> 对于var命令来说，JavaScript 的区块不构成单独的作用域（scope）。
>
> ```
> {
>   var a = 1;
> }
>
> a // 1
> ```
>
> 上面代码在区块内部，使用var命令声明并赋值了变量a，然后在区块外部，变量a依然有效，区块对于var命令不构成单独的作用域，与不使用区块的情况没有任何区别。在 JavaScript 语言中，单独使用区块并不常见，区块往往用来构成其他更复杂的语法结构，比如for、if、while、function等。

### 6. 条件语句

#### 6.1 if 结构

> JavaScript 提供if结构和switch结构，完成条件判断，即只有满足预设的条件，才会执行相应的语句。
>
> ```
> if (m === 3)
>   m = m + 1;
>
>
> if (m === 3) {
>   m += 1;
> }
>
>
> var x = 1;
> var y = 2;
> if (x = y) {
>   console.log(x);
> }
> // "2"
>
>
> if (x = 2) { // 不报错
> if (2 = x) { // 报错
> ```

#### 6.2 if...else 结构

> ```
> var m = 1;
> var n = 2;
>
> if (m !== 1)
> if (n === 2) console.log('hello');
> else console.log('world');
>
>
> if (m !== 1) {
>   if (n === 2) {
>     console.log('hello');
>   } else {
>     console.log('world');
>   }
> }
>
>
> if (m !== 1) {
>   if (n === 2) {
>     console.log('hello');
>   }
> } else {
>   console.log('world');
> }
> // world
> ```

#### 6.3 switch 结构

> ```
> var x = 1;
>
> switch (x) {
>   case 1:
>     console.log('x 等于1');
>   case 2:
>     console.log('x 等于2');
>   default:
>     console.log('x 等于其他值');
> }
> // x等于1
> // x等于2
> // x等于其他值
>
>
> switch (x) {
>   case 1:
>     console.log('x 等于1');
>     break;
>   case 2:
>     console.log('x 等于2');
>     break;
>   default:
>     console.log('x 等于其他值');
> }
>
>
> switch (1 + 3) {
>   case 2 + 2:
>     f();
>     break;
>   default:
>     neverHappens();
> }
> ```
>
> 需要注意的是，switch语句后面的表达式，与case语句后面的表示式比较运行结果时，采用的是严格相等运算符（===），而不是相等运算符（==），这意味着比较时不会发生类型转换。
>
> ```
> var x = 1;
>
> switch (x) {
>   case true:
>     console.log('x 发生类型转换');
>     break;
>   default:
>     console.log('x 没有发生类型转换');
> }
> // x 没有发生类型转换
> ```

#### 6.4 三元运算符 ?:

> 三元运算符可以被视为if...else...的简写形式，因此可以用于多种场合。

### 7. 循环语句

#### 7.1 while 循环

> ```
> var i = 0;
>
> while (i < 100) {
>   console.log('i 当前为：' + i);
>   i = i + 1;
> }
>
>
>
> while (true) {
>   console.log('Hello, world');
> }
> ```

#### 7.2 for 循环

> ```
> var x = 3;
> for (var i = 0; i < x; i++) {
>   console.log(i);
> }
> // 0
> // 1
> // 2
>
>
> for ( ; ; ){
>   console.log('Hello World');
> }
> ```

#### 7.3 do ... while 循环

> ```
> var x = 3;
> var i = 0;
>
> do {
>   console.log(i);
>   i++;
> } while(i < x);
> ```

#### 7.4 break 和 continue 语句

> break语句和continue语句都具有跳转作用，可以让代码不按既有的顺序执行。
>
> break语句用于跳出代码块或循环。
>
> ```
> var i = 0;
>
> while(i < 100) {
>   console.log('i 当前为：' + i);
>   i++;
>   if (i === 10) break;
> }
>
>
>
> for (var i = 0; i < 5; i++) {
>   console.log(i);
>   if (i === 3)
>     break;
> }
> // 0
> // 1
> // 2
> // 3
> ```
>
> continue语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。
>
> ```
> var i = 0;
>
> while (i < 100){
>   i++;
>   if (i % 2 === 0) continue;
>   console.log('i 当前为：' + i);
> }
> ```
>
> 如果存在多重循环，不带参数的break语句和continue语句都只针对最内层循环。

### 7.5 标签\(label\)

> JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置。标签可以是任意的标识符，但不能是保留字，语句部分可以是任意语句。标签通常与break语句和continue语句配合使用，跳出特定的循环。
>
> ```
> top:
>   for (var i = 0; i < 3; i++){
>     for (var j = 0; j < 3; j++){
>       if (i === 1 && j === 1) break top;
>       console.log('i=' + i + ', j=' + j);
>     }
>   }
> // i=0, j=0
> // i=0, j=1
> // i=0, j=2
> // i=1, j=0
> ```
>
> 上面代码为一个双重循环区块，break命令后面加上了top标签（注意，top不用加引号），满足条件时，直接跳出双层循环。如果break语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。
>
> 标签也可以用于跳出代码块。
>
> ```
> foo: {
>   console.log(1);
>   break foo;
>   console.log('本行不会输出');
> }
> console.log(2);
> // 1
> // 2
> ```
>
> 上面代码执行到break foo，就会跳出区块。
>
> continue语句也可以与标签配合使用。
>
> ```
> top:
>   for (var i = 0; i < 3; i++){
>     for (var j = 0; j < 3; j++){
>       if (i === 1 && j === 1) continue top;
>       console.log('i=' + i + ', j=' + j);
>     }
>   }
> // i=0, j=0
> // i=0, j=1
> // i=0, j=2
> // i=1, j=0
> // i=2, j=0
> // i=2, j=1
> // i=2, j=2
> ```
>
> 上面代码中，continue命令后面有一个标签名，满足条件时，会跳过当前循环，直接进入下一轮外层循环。如果continue语句后面不使用标签，则只能进入下一轮的内层循环。



