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
> 精度最多只能到53个二进制位，这意味着，绝对值小于2的53次方的整数，即$$-2^{53}$$到$$2^{53}$$，都可以精确表示。
>
> ```
> Math.pow(2, 53)
> // 9007199254740992
>
> Math.pow(2, 53) + 1
> // 9007199254740992
>
> Math.pow(2, 53) + 2
> // 9007199254740994
>
> Math.pow(2, 53) + 3
> // 9007199254740996
>
> Math.pow(2, 53) + 4
> // 9007199254740996
> ```
>
> 上面代码中，大于2的53次方以后，整数运算的结果开始出现错误。所以，大于2的53次方的数值，都无法保持精度。由于2的53次方是一个16位的十进制数值，所以简单的法则就是，JavaScript 对15位的十进制数都可以精确处理。
>
> ```
> Math.pow(2, 53)
> // 9007199254740992
>
> // 多出的三个有效数字，将无法保存
> 9007199254740992111
> // 9007199254740992000
> ```
>
> 上面示例表明，大于2的53次方以后，多出来的有效数字（最后三位的`111`）都会无法保存，变成0。

#### 1.3 数值范围

> 根据标准，64位浮点数的指数部分的长度是11个二进制位，意味着指数部分的最大值是2047（2的11次方减1）。也就是说，64位浮点数的指数部分的值最大为2047，分出一半表示负数，则 JavaScript 能够表示的数值范围为$$x = y$$到$$2^{-1023}$$（开区间），超出这个范围的数无法表示。
>
> 如果一个数大于等于2的1024次方，那么就会发生“正向溢出”，即 JavaScript 无法表示这么大的数，这时就会返回Infinity。如果一个数小于等于2的-1075次方（指数部分最小值-1023，再加上小数部分的52位），那么就会发生为“负向溢出”，即 JavaScript 无法表示这么小的数，这时会直接返回0。
>
> ```
> Math.pow(2, 1024) // Infinity
> Math.pow(2, -1075) // 0
> ```
>
> 下面是一个实际的例子:
>
> ```
> var x = 0.5;
>
> for(var i = 0; i < 25; i++) {
>   x = x * x;
> }
>
> x // 0
> ```
>
> 上面代码中，对`0.5`连续做25次平方，由于最后结果太接近0，超出了可表示的范围，JavaScript 就直接将其转为0。
>
> JavaScript 提供`Number`对象的`MAX_VALUE`和`MIN_VALUE`属性，返回可以表示的具体的最大值和最小值。
>
> ```
> Number.MAX_VALUE // 1.7976931348623157e+308
> Number.MIN_VALUE // 5e-324
> ```

### 2. 数值的表示方法

> JavaScript 的数值有多种表示方法，可以用字面形式直接表示，比如`35`（十进制）和`0xFF`（十六进制）。
>
> 数值也可以采用科学计数法表示，下面是几个科学计数法的例子:
>
> 1. 小数点前的数字多于21位
> 2. 小数点后的零多于5个
>
> ```
> 1234567890123456789012
> // 1.2345678901234568e+21
>
> 123456789012345678901
> // 123456789012345680000
>
>
> // 小数点后紧跟5个以上的零，
> // 就自动转为科学计数法
> 0.0000003 // 3e-7
>
> // 否则，就保持原来的字面形式
> 0.000003 // 0.000003
> ```

### 3. 数值的进制

> 使用字面量（literal）直接表示一个数值时，JavaScript 对整数提供四种进制的表示方法：十进制、十六进制、八进制、二进制:
>
> * 十进制：没有前导0的数值。
> * 八进制：有前缀0o或0O的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。
> * 十六进制：有前缀0x或0X的数值。
> * 二进制：有前缀0b或0B的数值。
>
> 默认情况下，JavaScript 内部会自动将八进制、十六进制、二进制转为十进制，通常来说，有前导0的数值会被视为八进制，但是如果前导0后面有数字8和9，则该数值被视为十进制。下面是一些例子:
>
> ```
> 0xff // 255
> 0o377 // 255
> 0b11 // 3
>
> 0xzz // 报错
> 0o88 // 报错
> 0b22 // 报错
>
> 0888 // 虽然有前导0，但仍自动转为十进制，888
> 0777 // 虽然有前导0，但仍自动转为十进制，511
> ```
>
> 前导0表示八进制，处理时很容易造成混乱。ES5 的严格模式和 ES6，已经废除了这种表示法，但是浏览器为了兼容以前的代码，目前还继续支持这种表示法。

### 4. 特殊数值

#### 4.1 正零和负零

> 前面说过，JavaScript 的64位浮点数之中，有一个二进制位是符号位。这意味着，任何一个数都有一个对应的负值，就连`0`也不例外。
>
> JavaScript 内部实际上存在2个`0`：一个是`+0`，一个是`-0`，区别就是64位浮点数表示法的符号位不同。它们是等价的。几乎所有场合，正零和负零都会被当作正常的`0`。唯一有区别的场合是，`+0`或`-0`当作分母，返回的值是不相等的。
>
> ```
> -0 === +0 // true
> 0 === -0 // true
> 0 === +0 // true
>
>
> +0 // 0
> -0 // 0
> (-0).toString() // '0'
> (+0).toString() // '0'
>
>
> (1 / +0) === (1 / -0) // false
> ```
>
> 上面的代码之所以出现这样结果，是因为除以正零得到`+Infinity`，除以负零得到`-Infinity`，这两者是不相等的（关于`Infinity`详见下文）。

#### 4.2 NaN

##### \(1\) 含义

> `NaN`是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。另外，一些没有数学意义数学函数的运算结果会出现`NaN`。
>
> ```
> 5 - 'x' // NaN
>
> Math.acos(2) // NaN
> Math.log(-1) // NaN
> Math.sqrt(-1) // NaN
>
> 0 / 0 // NaN
> ```
>
> 需要注意的是，`NaN`不是独立的数据类型，而是一个特殊数值，它的数据类型依然属于`Number`，使用`typeof`运算符可以看得很清楚。
>
> ```
> typeof NaN // 'number'
> ```

##### \(2\) 运算规则

> `NaN`不等于任何值，包括它本身。
>
> ```
> NaN === NaN // false
> ```
>
> 数组的`indexOf`方法内部使用的是严格相等运算符，所以该方法对`NaN`不成立。
>
> ```
> [NaN].indexOf(NaN) // -1
> ```
>
> `NaN`在布尔运算时被当作`false`。
>
> ```
> Boolean(NaN) // false
> ```
>
> `NaN`与任何数（包括它自己）的运算，得到的都是`NaN`。
>
> ```
> NaN + 32 // NaN
> NaN - 32 // NaN
> NaN * 32 // NaN
> NaN / 32 // NaN
> ```

#### 4.3 Infinity

##### \(1\) 含义

> `Infinity`表示“无穷”，用来表示两种场景。一种是一个正的数值太大，或一个负的数值太小，无法表示；另一种是非0数值除以0，得到`Infinity`。
>
> ```
> // 场景一
> Math.pow(2, 1024)
> // Infinity
>
> // 场景二
> 0 / 0 // NaN
> 1 / 0 // Infinity
> ```
>
> `Infinity`有正负之分，`Infinity`表示正的无穷，`-Infinity`表示负的无穷。
>
> ```
> Infinity === -Infinity // false
>
> 1 / -0 // -Infinity
> -1 / -0 // Infinity
> ```
>
> 由于数值正向溢出（overflow）、负向溢出（underflow）和被`0`除，JavaScript 都不报错，所以单纯的数学运算几乎没有可能抛出错误。
>
> `Infinity`大于一切数值（除了`NaN`），`-Infinity`小于一切数值（除了`NaN`）。`Infinity`与`NaN`比较，总是返回`false`。
>
> ```
> Infinity > 1000 // true
> -Infinity < -1000 // true
>
>
> Infinity > NaN // false
> -Infinity > NaN // false
>
> Infinity < NaN // false
> -Infinity < NaN // false
> ```

##### \(2\) 运算法则

> ```
> 5 * Infinity // Infinity
> 5 - Infinity // -Infinity
> Infinity / 5 // Infinity
> 5 / Infinity // 0
>
> 0 * Infinity // NaN
> 0 / Infinity // 0
> Infinity / 0 // Infinity
>
> Infinity + Infinity // Infinity
> Infinity * Infinity // Infinity
>
> Infinity - Infinity // NaN
> Infinity / Infinity // NaN
>
> null * Infinity // NaN
> null / Infinity // 0
> Infinity / null // Infinity
>
> undefined + Infinity // NaN
> undefined - Infinity // NaN
> undefined * Infinity // NaN
> undefined / Infinity // NaN
> Infinity / undefined // NaN
> ```

### 5. 与数值相关的全局方法

#### 5.1 parseInt\(\)

##### \(1\) 基本用法

> `parseInt`方法用于将字符串转为整数。
>
> ```
> parseInt('123') // 123
> parseInt('   81') // 81
> parseInt(1.23) // 1
> // 等同于
> parseInt('1.23') // 1
> ```
>
> 字符串转为整数的时候，是一个个字符依次转换，如果遇到不能转为数字的字符，就不再进行下去，返回已经转好的部分。
>
> ```
> parseInt('8a') // 8
> parseInt('12**') // 12
> parseInt('12.34') // 12
> parseInt('15e2') // 15
> parseInt('15px') // 15
> ```
>
> 上面代码中，`parseInt`的参数都是字符串，结果只返回字符串头部可以转为数字的部分。
>
> 如果字符串的第一个字符不能转化为数字（后面跟着数字的正负号除外），返回`NaN`。
>
> ```
> parseInt('abc') // NaN
> parseInt('.3') // NaN
> parseInt('') // NaN
> parseInt('+') // NaN
> parseInt('+1') // 1
> ```
>
> 所以，`parseInt`的返回值只有两种可能，要么是一个十进制整数，要么是`NaN`。
>
> 如果字符串以`0x`或`0X`开头，`parseInt`会将其按照十六进制数解析。如果字符串以
>
> `0`开头，将其按照10进制解析。
>
> ```
> parseInt('0x10') // 16
> parseInt('011') // 11
> ```
>
> 对于那些会自动转为科学计数法的数字，`parseInt`会将科学计数法的表示方法视为字符串，因此导致一些奇怪的结果。
>
> ```
> parseInt(1000000000000000000000.5) // 1
> // 等同于
> parseInt('1e+21') // 1
>
> parseInt(0.0000008) // 8
> // 等同于
> parseInt('8e-7') // 8
> ```

##### \(2\) 进制转换

> `parseInt`方法还可以接受第二个参数（2到36之间），表示被解析的值的进制，返回该值对应的十进制数。默认情况下，`parseInt`的第二个参数为10，即默认是十进制转十进制。如果第二个参数不是数值，会被自动转为一个整数。这个整数只有在2到36之间，才能得到有意义的结果，超出这个范围，则返回`NaN`。如果第二个参数是`0`、`undefined`和`null`，则直接忽略。如果字符串包含对于指定进制无意义的字符，则从最高位开始，只返回可以转换的数值。如果最高位无法转换，则直接返回`NaN`。
>
> ```
> parseInt('1000') // 1000
> // 等同于
> parseInt('1000', 10) // 1000
>
>
> parseInt('1000', 2) // 8
> parseInt('1000', 6) // 216
> parseInt('1000', 8) // 512
>
> parseInt('10', 37) // NaN
> parseInt('10', 1) // NaN
> parseInt('10', 0) // 10
> parseInt('10', null) // 10
> parseInt('10', undefined) // 10
>
> parseInt('1546', 2) // 1
> parseInt('546', 2) // NaN
> ```
>
> 前面说过，如果`parseInt`的第一个参数不是字符串，会被先转为字符串。这会导致一些令人意外的结果。
>
> ```
> String(0x11)    // 17
>
> parseInt(0x11, 36) // 43
> parseInt(0x11, 2) // 1
>
> // 等同于
> parseInt(String(0x11), 36)
> parseInt(String(0x11), 2)
>
> // 等同于
> parseInt('17', 36)
> parseInt('17', 2)
> ```
>
> 上面代码中，十六进制的`0x11`会被先转为十进制的17，再转为字符串。然后，再用36进制或二进制解读字符串`17`，最后返回结果`43`和`1`。
>
> 这种处理方式，对于八进制的前缀0，尤其需要注意。
>
> ```
> parseInt(011, 2) // NaN
>
> // 等同于
> parseInt(String(011), 2)
>
> // 等同于
> parseInt(String(9), 2)
> ```
>
> 上面代码中，第一行的`011`会被先转为字符串`9`，因为`9`不是二进制的有效字符，所以返回`NaN`。如果直接计算`parseInt('011', 2)`，`011`则是会被当作二进制处理，返回3。
>
> JavaScript 不再允许将带有前缀0的数字视为八进制数，而是要求忽略这个`0`。但是，为了保证兼容性，大部分浏览器并没有部署这一条规定。

#### 5.2 parseFloat\(\)

> `parseFloat`方法用于将一个字符串转为浮点数。
>
> ```
> parseFloat('3.14') // 3.14
> ```
>
> 如果字符串符合科学计数法，则会进行相应的转换。
>
> ```
> parseFloat('314e-2') // 3.14
> parseFloat('0.0314E+2') // 3.14
> ```
>
> 如果字符串包含不能转为浮点数的字符，则不再进行往后转换，返回已经转好的部分。
>
> ```
> parseFloat('3.14more non-digit characters') // 3.14
> ```
>
> `parseFloat`方法会自动过滤字符串前导的空格。
>
> ```
> parseFloat('\t\v\r12.34\n ') // 12.34
> ```
>
> 如果参数不是字符串，或者字符串的第一个字符不能转化为浮点数，则返回`NaN`。
>
> ```
> parseFloat([]) // NaN
> parseFloat('FF2') // NaN
> parseFloat('') // NaN
> ```
>
> 上面代码中，尤其值得注意，`parseFloat`会将空字符串转为`NaN`。
>
> 这些特点使得`parseFloat`的转换结果不同于`Number`函数。
>
> ```
> parseFloat(true)  // NaN
> Number(true) // 1
>
> parseFloat(null) // NaN
> Number(null) // 0
>
> parseFloat('') // NaN
> Number('') // 0
>
> parseFloat('123.45#') // 123.45
> Number('123.45#') // NaN
> ```

#### 5.3 isNaN\(\)

> `isNaN`方法可以用来判断一个值是否为`NaN`。但是，`isNaN`只对数值有效，如果传入其他值，会被先转成数值。比如，传入字符串的时候，字符串会被先转成`NaN`，所以最后返回`true`，这一点要特别引起注意。也就是说，`isNaN`为`true`的值，有可能不是`NaN`，而是一个字符串。出于同样的原因，对于对象和数组，`isNaN`也返回`true`。
>
> ```
> isNaN(NaN) // true
> isNaN(123) // false
>
> isNaN('Hello') // true
> // 相当于
> isNaN(Number('Hello')) // true
>
> isNaN({}) // true
> // 等同于
> isNaN(Number({})) // true
>
> isNaN(['xzy']) // true
> // 等同于
> isNaN(Number(['xzy'])) // true
> ```
>
> 但是，对于空数组和只有一个数值成员的数组，`isNaN`返回`false`。
>
> ```
> isNaN([]) // false
> isNaN([123]) // false
> isNaN(['123']) // false
> ```
>
> 上面代码之所以返回`false`，原因是这些数组能被`Number`函数转成数值，请参见《数据类型转换》一章。
>
> 因此，使用`isNaN`之前，最好判断一下数据类型。
>
> ```
> function myIsNaN(value) {
>   return typeof value === 'number' && isNaN(value);
> }
> ```
>
> 判断`NaN`更可靠的方法是，利用`NaN`为唯一不等于自身的值的这个特点，进行判断。
>
> ```
> function myIsNaN(value) {
>   return value !== value;
> }
> ```

#### 5.4 isFinite\(\)

> `isFinite`方法返回一个布尔值，表示某个值是否为正常的数值。
>
> ```
> isFinite(Infinity) // false
> isFinite(-Infinity) // false
> isFinite(NaN) // false
> isFinite(undefined) // false
> isFinite(null) // true
> isFinite(-1) // true
> ```

## 字符串

### 1. 概述

#### 1.1 定义

> 字符串就是零个或多个排在一起的字符，放在单引号或双引号之中。单引号字符串的内部，可以使用双引号。双引号字符串的内部，可以使用单引号。如果要在单引号字符串的内部，使用单引号，就必须在内部的单引号前面加上反斜杠，用来转义。双引号字符串内部使用双引号，也是如此。
>
> ```
> 'abc'
> "abc"
>
> 'key = "value"'
> "It's a long journey"
>
> 'Did she say \'Hello\'?'
> // "Did she say 'Hello'?"
>
> "Did she say \"Hello\"?"
> // "Did she say "Hello"?"
> ```
>
> 由于 HTML 语言的属性值使用双引号，所以很多项目约定 JavaScript 语言的字符串只使用单引号，本教程遵守这个约定。当然，只使用双引号也完全可以。重要的是坚持使用一种风格，不要一会使用单引号表示字符串，一会又使用双引号表示。
>
> 字符串默认只能写在一行内，分成多行将会报错。
>
> ```
> 'a
> b
> c'
> // SyntaxError: Unexpected token ILLEGAL
> ```
>
> 如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠。
>
> ```
> var longString = 'Long \
> long \
> long \
> string';
>
> longString
> // "Long long long string"
> ```
>
> 上面代码表示，加了反斜杠以后，原来写在一行的字符串，可以分成多行书写。但是，输出的时候还是单行，效果与写在同一行完全一样。注意，反斜杠的后面必须是换行符，而不能有其他字符（比如空格），否则会报错。
>
> 连接运算符（`+`）可以连接多个单行字符串，将长字符串拆成多行书写，输出的时候也是单行。
>
> ```
> var longString = 'Long '
>   + 'long '
>   + 'long '
>   + 'string';
> ```
>
> 如果想输出多行字符串，有一种利用多行注释的变通方法:
>
> ```
> (function () { /*
> line 1
> line 2
> line 3
> */}).toString().split('\n').slice(1, -1).join('\n')
> // "line 1
> // line 2
> // line 3"
> ```

#### 1.2 转义

> 反斜杠（\）在字符串内有特殊含义，用来表示一些特殊字符，所以又称为转义符。
>
> 需要用反斜杠转义的特殊字符，主要有下面这些:
>
> * \0 ：null（\u0000）
> * \b ：后退键（\u0008）
> * \f ：换页符（\u000C）
> * \n ：换行符（\u000A）
> * \r ：回车键（\u000D）
> * \t ：制表符（\u0009）
> * \v ：垂直制表符（\u000B）
> * \' ：单引号（\u0027）
> * \" ：双引号（\u0022）
> * \ ：反斜杠（\u005C）
>
> 反斜杠还有三种特殊用法。
>
> （1）`\HHH`
>
> 反斜杠后面紧跟三个八进制数（`000`到`377`），代表一个字符。`HHH`对应该字符的 Unicode 码点，比如`\251`表示版权符号。显然，这种方法只能输出256种字符。
>
> （2）`\xHH`
>
> `\x`后面紧跟两个十六进制数（`00`到`FF`），代表一个字符。`HH`对应该字符的 Unicode 码点，比如`\xA9`表示版权符号。这种方法也只能输出256种字符。
>
> （3）`\uXXXX`
>
> `\u`后面紧跟四个十六进制数（`0000`到`FFFF`），代表一个字符。`XXXX`对应该字符的 Unicode 码点，比如`\u00A9`表示版权符号。
>
> 下面是这三种字符特殊写法的例子:
>
> ```
> '\251' // "©"
> '\xA9' // "©"
> '\u00A9' // "©"
>
> '\172' === 'z' // true
> '\x7A' === 'z' // true
> '\u007A' === 'z' // true
> ```
>
> 如果在非特殊字符前面使用反斜杠，则反斜杠会被省略。如果字符串的正常内容之中，需要包含反斜杠，则反斜杠前面需要再加一个反斜杠，用来对自身转义。
>
> ```
> '\a'
> // "a"
>
> "Prev \\ Next"
> // "Prev \ Next"
> ```

#### 1.3 字符串与数组

> 字符串可以被视为字符数组，因此可以使用数组的方括号运算符，用来返回某个位置的字符（位置编号从0开始）。
>
> ```
> var s = 'hello';
> s[0] // "h"
> s[1] // "e"
> s[4] // "o"
>
> // 直接对字符串使用方括号运算符
> 'hello'[1] // "e"
> ```
>
> 如果方括号中的数字超过字符串的长度，或者方括号中根本不是数字，则返回`undefined`。
>
> ```
> 'abc'[3] // undefined
> 'abc'[-1] // undefined
> 'abc'['x'] // undefined
> ```
>
> 但是，字符串与数组的相似性仅此而已。实际上，无法改变字符串之中的单个字符。
>
> ```
> var s = 'hello';
>
> delete s[0];
> s // "hello"
>
> s[1] = 'a';
> s // "hello"
>
> s[5] = '!';
> s // "hello"
> ```

#### 1.4 length 属性

> `length`属性返回字符串的长度，该属性也是无法改变的。
>
> ```
> var s = 'hello';
> s.length // 5
>
> s.length = 3;
> s.length // 5
>
> s.length = 7;
> s.length // 5
> ```

### 2. 字符集

> JavaScript 使用 Unicode 字符集。JavaScript 引擎内部，所有字符都用 Unicode 表示。
>
> JavaScript 不仅以 Unicode 储存字符，还允许直接在程序中使用 Unicode 码点表示字符，即将字符写成`\uxxxx`的形式，其中`xxxx`代表该字符的 Unicode 码点。比如，`\u00A9`代表版权符号。
>
> ```
> var s = '\u00A9';
> s // "©"
> ```
>
> 解析代码的时候，JavaScript 会自动识别一个字符是字面形式表示，还是 Unicode 形式表示。输出给用户的时候，所有字符都会转成字面形式。
>
> ```
> var f\u006F\u006F = 'abc';
> foo // "abc"
> ```
>
> 上面代码中，第一行的变量名`foo`是 Unicode 形式表示，第二行是字面形式表示。JavaScript 会自动识别。
>
> 我们还需要知道，每个字符在 JavaScript 内部都是以16位（即2个字节）的 UTF-16 格式储存。也就是说，JavaScript 的单位字符长度固定为16位长度，即2个字节。
>
> 但是，UTF-16 有两种长度：对于码点在`U+0000`到`U+FFFF`之间的字符，长度为16位（即2个字节）；对于码点在`U+10000`到`U+10FFFF`之间的字符，长度为32位（即4个字节），而且前两个字节在`0xD800`到`0xDBFF`之间，后两个字节在`0xDC00`到`0xDFFF`之间。举例来说，码点`U+1D306`对应的字符为`𝌆，`它写成 UTF-16 就是`0xD834 0xDF06`。
>
> JavaScript 对 UTF-16 的支持是不完整的，由于历史原因，只支持两字节的字符，不支持四字节的字符。这是因为 JavaScript 第一版发布的时候，Unicode 的码点只编到`U+FFFF`，因此两字节足够表示了。后来，Unicode 纳入的字符越来越多，出现了四字节的编码。但是，JavaScript 的标准此时已经定型了，统一将字符长度限制在两字节，导致无法识别四字节的字符。上一节的那个四字节字符`𝌆`，浏览器会正确识别这是一个字符，但是 JavaScript 无法识别，会认为这是两个字符。
>
> ```
> '𝌆'.length // 2
> ```
>
> 上面代码中，JavaScript 认为`𝌆`的长度为2，而不是1。
>
> 总结一下，对于码点在`U+10000`到`U+10FFFF`之间的字符，JavaScript 总是认为它们是两个字符（`length`属性为2）。所以处理的时候，必须把这一点考虑在内，也就是说，JavaScript 返回的字符串长度可能是不正确的。

### 3. Base64 编码

> 有时，文本里面包含一些不可打印的符号，比如 ASCII 码0到31的符号都无法打印出来，这时可以使用 Base64 编码，将它们转成可以打印的字符。另一个场景是，有时需要以文本格式传递二进制数据，那么也可以使用 Base64 编码。
>
> 所谓 Base64 就是一种编码方法，可以将任意值转成 0～9、A～Z、a-z、`+`和`/`这64个字符组成的可打印字符。使用它的主要目的，不是为了加密，而是为了不出现特殊字符，简化程序的处理。
>
> JavaScript 原生提供两个 Base64 相关的方法。
>
> * `btoa()`：任意值转为 Base64 编码
> * `atob()`：Base64 编码转为原来的值
>
> ```
> var string = 'Hello World!';
> btoa(string) // "SGVsbG8gV29ybGQh"
> atob('SGVsbG8gV29ybGQh') // "Hello World!"
> ```
>
> 注意，这两个方法不适合非 ASCII 码的字符，会报错。
>
> ```
> btoa('你好') // 报错
> ```
>
> 要将非 ASCII 码字符转为 Base64 编码，必须中间插入一个转码环节，再使用这两个方法:
>
> ```
> function b64Encode(str) {
>   return btoa(encodeURIComponent(str));
> }
>
> function b64Decode(str) {
>   return decodeURIComponent(atob(str));
> }
>
> b64Encode('你好') // "JUU0JUJEJUEwJUU1JUE1JUJE"
> b64Decode('JUU0JUJEJUEwJUU1JUE1JUJE') // "你好"
> ```



