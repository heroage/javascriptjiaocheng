# 数据类型

## 数据类型概述

### 1. 简介

> JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值，本教程不涉及。）
>
> * 数值（number）：整数和小数（比如1和3.14）
> * 字符串（string）：文本（比如Hello World）。
> * 布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）
> * undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
> * null：表示空值，即此处的值为空。
> * 对象（object）：各种值组成的集合。
>
> 通常，**数值**、**字符串**、**布尔值**这三种类型，合称为**原始类型**（primitive type）的值，即它们是最基本的数据类型，不能再细分了。对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于 undefined 和 null，一般将它们看成两个特殊值。
>
> 对象是最复杂的数据类型，又可以分成三个子类型:
>
> * 狭义的对象（object）
> * 数组（array）
> * 函数（function）
>
> 狭义的对象和数组是两种不同的数据组合方式，除非特别声明，本教程的“对象”都特指狭义的对象。函数其实是处理数据的方法，JavaScript 把它当成一种数据类型，可以赋值给变量，这为编程带来了很大的灵活性，也为 JavaScript 的“函数式编程”奠定了基础。

### 2. typeof 运算符

> JavaScript 有三种方法确定值的类型:
>
> * typeof运算符
> * instanceof运算符
> * Object.prototype.toString方法
>
> 这里介绍先 typeof 运算符，typeof 运算符可以返回一个值的数据类型。数值、字符串、布尔值、函数、unidefined、null 分别返回 number、string、boolean、function、undefined、object。
>
> ```
> typeof 123 // "number"
> typeof '123' // "string"
> typeof false // "boolean"
>
> function f() {}
> typeof f
> // "function"
>
> typeof undefined
> // "undefined"
>
> typeof null // "object"
> ```
>
> 由此，typeof 可以用来检查一个没有声明的变量，而不报错。
>
> ```
>  v
> // ReferenceError: v is not defined
>
> typeof v
> // "undefined"
> ```
>
> 上面代码中，变量v没有用var命令声明，直接使用就会报错。但是，放在typeof后面，就不报错了，而是返回undefined。
>
> 实际编程中，这个特点通常用在判断语句:
>
> ```
> // 错误的写法
> if (v) {
>   // ...
> }
> // ReferenceError: v is not defined
>
>
> // 正确的写法
> if (typeof v === "undefined") {
>   // ...
> }
> ```
>
> 几个实例:
>
> ```
> typeof window // "object"
> typeof {} // "object"
> typeof [] // "object"
> ```
>
> 上面代码中，空数组（\[\]）的类型也是object，这表示在 JavaScript 内部，数组本质上只是一种特殊的对象。这里顺便提一下，instanceof运算符可以区分数组和对象。instanceof运算符的详细解释，请见《面向对象编程》一章。
>
> ```
> var o = {};
> var a = [];
>
> o instanceof Array // false
> a instanceof Array // true
> ```

# null, undefined 和布尔值

### 1. null 和 undefined

> null与undefined都可以表示“没有”，含义非常相似。将一个变量赋值为undefined或null，语法效果几乎没区别。
>
> ```
> var a = undefined;
> // 或者
> var a = null;
> ```
>
> 上面代码中，变量a分别被赋值为undefined和null，这两种写法的效果几乎等价。在if语句中，它们都会被自动转为false，相等运算符（==）甚至直接报告两者相等。
>
> 区别:
>
> ```
> Number(null) // 0
> 5 + null // 5
>
> Number(undefined) // NaN
> 5 + undefined // NaN
> ```

#### 1.2 用法和含义

> 对于null和undefined，大致可以像下面这样理解:
>
> null表示空值，即该处的值现在为空。调用函数时，某个参数未设置任何值，这时就可以传入null，表示该参数为空。比如，某个函数接受引擎抛出的错误作为参数，如果运行过程中未出错，那么这个参数就会传入null，表示未发生错误。
>
> undefined表示“未定义”，下面是返回undefined的典型场景:
>
> ```
> // 变量声明了，但没有赋值
> var i;
> i // undefined
>
> // 调用函数时，应该提供的参数没有提供，该参数等于 undefined
> function f(x) {
>   return x;
> }
> f() // undefined
>
> // 对象没有赋值的属性
> var  o = new Object();
> o.p // undefined
>
> // 函数没有返回值时，默认返回 undefined
> function f() {}
> f() // undefined
> ```

### 2. 布尔值

> 布尔值代表“真”和“假”两个状态。“真”用关键字true表示，“假”用关键字false表示，布尔值只有这两个值。
>
> 下列运算符会返回布尔值：
>
> * 前置逻辑运算符： ! \(Not\)
> * 相等运算符：===，!==，==，!=
> * 比较运算符：&gt;，&gt;=，&lt;，&lt;=
>
> 如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为false，其他值都视为true:
>
> * undefined
> * null
> * false
> * 0
> * NaN
> * ""或''（空字符串）
>
> 布尔值往往用于程序流程的控制，请看一个例子:
>
> ```
> if ('') {
>   console.log('true');
> }
> // 没有任何输出
> ```
>
> 布尔值往往用于程序流程的控制，请看以下几个例子:
>
> ```
> if ('') {
>   console.log('true');
> }
> // 没有任何输出
>
>
> if ([]) {
>   console.log('true');
> }
> // true
>
> if ({}) {
>   console.log('true');
> }
> // true
> ```

## 数值

### 1. 概述

#### 1.1 整数和浮点数

> JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。
>
> ```
> 1 === 1.0 // true
> ```
>
> 这就是说，JavaScript 语言的底层根本没有整数，所有数字都是小数（64位浮点数）。容易造成混淆的是，某些运算只有整数才能完成，此时 JavaScript 会自动把64位浮点数，转成32位整数，然后再进行运算，参见《运算符》一章的“位运算”部分。
>
> 由于浮点数不是精确的值，所以涉及小数的比较和运算要特别小心:
>
> ```
> 0.1 + 0.2 === 0.3
> // false
>
> 0.3 / 0.1
> // 2.9999999999999996
>
> (0.3 - 0.2) === (0.2 - 0.1)
> // false
> ```

#### 1.2 数值精度

> 根据国际标准 IEEE 754，JavaScript 浮点数的64个二进制位，从最左边开始，是这样组成的:
>
> * 第1位：符号位，0表示正数，1表示负数
> * 第2位到第12位（共11位）：指数部分
> * 第13位到第64位（共52位）：小数部分（即有效数字）
>
> 符号位决定了一个数的正负，指数部分决定了数值的大小，小数部分决定了数值的精度。  
> 指数部分一共有11个二进制位，因此大小范围就是0到2047。IEEE 754 规定，如果指数部分的值在0到2047之间（不含两个端点），那么有效数字的第一位默认总是1，不保存在64位浮点数之中。也就是说，有效数字这时总是1.xx...xx的形式，其中xx..xx的部分保存在64位浮点数之中，最长可能为52位。因此，JavaScript 提供的有效数字最长为53个二进制位。
>
> 一个数字在 JavaScript 内部实际的表示形式如下:
>
> ```
> (-1)^符号位 * 1.xx...xx * 2^指数部分
> ```
>