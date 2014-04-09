# JavaScript编码规范
----------


## 目标

> 编码规范对于程序员而言尤为重要，有以下几个原因：
> - 一个软件的生命周期中，80%的花费在于维护
> - 几乎没有任何一个软件，在其整个生命周期中，均由最初的开发人员来维护
> - 编码规范可以改善软件的可读性，可以让程序员尽快而彻底地理解新的代码
> - 如果你将源码作为产品发布，就需要确任它是否被很好的打包并且清晰无误，一如你已构建的其它任何产品

编码风格是编码规范中的一种，每个人都有自己的编码风格，形成符合编码规范的风格，有利于编写**易读**、**可维护**的JavaScript代码。


## JavaScript文件

- JavaScript程序应独立保存在后缀名为.js的文件中。
- JavaScript代码不应该被包含在HTML文件中，除非这是段特定只属于此部分的代码。在HTML中的JavaScript代码会明显增加文件大小，而且也不能对其进行缓存和压缩。
- 外部引入的js文件应尽量放到`body`的后面。这样可以减少因为载入脚本而造成其他页面内容载入也被延迟的问题。


## 缩进

缩进层级使用4个空格组成，当使用`Tab`键时，在软件中定义将`Tab`转化为4个空格。由此产生的多余空格将在代码压缩时消除。

    if (boolean) {
        do();
    }


## 换行

- 避免每行超过80个字符。当一条语句一行写不下时，应当换行。
- 在运算符号后换行。
- 下一行应该缩进8个空格.


    func(arg1, arg2, arg3,
            arg4, arg5)

    var table = row1 + row2 + row3 +
            row4 + row5;


## 注释

代码应当具备说明性注释，出现以下情况时必须使用注释：

- 代码晦涩难懂。
- 可能会被误认为错误的代码。
- 针对某种特殊情况的处理。
- 对象、方法、属性等文档注释（需按规范使用恰当的文档注释）。

### 单行注释

当注释时只有一行时，使用独占一行的单行注释，并与上一行代码间隔一行。注释与文字说明或代码间隔一空格。

    // XX条件判断
    if (condition) {
        
        // 如果检查通过，do something
        doSomething();
    }

当注释同一代码块的多行代码时，使用连续的多行注释。

    // 目前不需要的代码
    // if (condition) {
    //     doSomething();
    // }

### 多行注释

当注释需要多行时，使用多行注释，并与其所描述的代码行保持相同的缩进，多行注释至少包含如下三行：

1. 首行仅包含`/*`，不含其它内容；如果是文档注释，使用`/**`。
2. 第二行开始以`*`开头，并与首行的`*`号对齐，后面开始书写文字。
3. 最后一行以`*\`结束，不含其它内容，同样保持`*`号对齐。


    /*
     * 条件判断
     */
    if (condition) {
        
        /*
         * 如果检查通过，do something
         */
        doSomething();
    }

当注释多个连续代码块时，使用头尾注释形式的多行注释。

### 注释声明

使用注释声明额外的信息，使用大写单词并紧跟一个冒号，可用于单行或多行注释。

- TODO —— 表示代码未完成，需要完善。
- HACK —— 表示临时性措施，可能需要寻找更好的解决方法。
- XXX —— 表示代码存在问题，急需处理。
- FIXME —— 表示存在问题需要修复。
- REVIEW —— 表示代码需要评审。


    // TODO: 需要换种方案
    if (condition) {
        
        /*
         * HACK: 如果是IE，do something
         */
        doSomething();
    }


## 严格模式

在函数内部使用严格模式，不要在全局使用严格模式。

    function doSomething() {
        "use strict"

        statements；
    }


## `undefined`的比较

避免使用`undefined`，判断变量是否定义，使用`typeof`。

    typeof variable === "undefined"


## `null`的使用

- 初始化一个将被赋值为对象的变量。
- 与一个已经初始化的变量比较。
- 当函数期望的参数是对象时，作为参数传入。
- 当函数期望的返回值是对象时，作为返回值传出。


    var foo = null;

    function getFoo(obj) {
        if ( obj !== null) {
            return new Foo();
        } else {
            return null;
        }
    }
    
    getFoo(null);


## 变量声明

所有的变量必须在使用前进行声明。JavaScript并不强制必须这么做，但是这么做可以让程序易于阅读，且也容易发现那些没声明的变量(它们会被编译成全局变量)。

采用单一var声明，并将var语句放在函数的顶部。

每个变量的声明语句单独放到一行，初始化变量写在未初始化变量之前，变量名左对齐，统一缩进。


    //建议写法
    var current = 10,
        level = 1,
        size;


`if`,`for`,`while`等语句块不会产生新的局部作用域，避免在非函数语句块里声明变量。

    //不建议的写法
    for (...) {
        var x = 'foo';
    }

    //建议的写法
    var x;
    for (...) {
        x = 'foo';
    }


## 函数声明

函数应当在使用前提前定义。内函数的定义跟在var语句的后面。

函数名与`(`(左括号)之间不应该有空格。`)`(右括号)与函数体的`{`(左花括号)之间可以插入一个空格。函数体每一层级应缩进四个空格。`}`(右花括号)与function关键字左对齐。参数名之间在逗号后保留一个空格。

    function outer(c, d) {
        var e = c + d;
        function inner(a, b) {
            return (e + a) + b;
        }
        return inner(0, 1);
    }

使用函数定义格式创建函数，而不是表达式或Function构造器。

    //建议使用
    function foo() {
        doSomething();
    }

匿名函数或函数表达式的function关键字和`(`(左括号)之间不要有空格。

    //函数表达式
    var foo = function() {
        return;
    };
    
    //对象方法使用匿名函数
    obj = {
        method: function() {
            return this;
        }
    };

立即调用函数应该在最外层使用圆括号包裹。

    var foo = (function() {
        return 'bar';
    }());

函数不应该在`if`,`for`,`while`等语句块中定义，避免被当成表达式而不是函数定义，带来潜在的bug。

不单独使用全局函数。


## 命名

变量名应由26个大小写字母，10个数字(0-9)，和`_`(下划线)组成。

普通变量以小写的英文名词开头，采用驼峰式命名。

    var currentNumber = 0；

常量命名使用下划线分隔不同单词，所有单词大写。

    var MAX_NUMBER = 100;

私有变量或私有函数以下划线开头。

    var _step = 5;

函数命名以小写的英文动词开头，采用驼峰式命名，不应该在函数名中出现下划线。

    function getNumber() {
        return currentNumber;
    }

构造函数或命名空间以首字母大写的非动词开头，采用驼峰式命名。

    function MyCalc(number) {
        this.currentNumber = number;
    }

    var MyNameSpace = {};


## 对象直接量

对象直接量使用如下格式。

- 起始左花括号应当同表达式保持同一行，作为参数时与函数名保持在同一行。
- 每个属性名值对保持一层缩进，其后紧跟冒号，然后是空格，最后是属性值。
- 如果属性是函数类型，函数体应当另起一行，并且属性前后保留一个空行。
- 一组相关的属性前后可以插入空行以提升代码可读性。
- 结束的右花括号应当独占一行。


## 语句

### 简单语句

一行一语句，始终以`;`(分号)结尾。
JavaScript可以把任何表达式当作一条语句。这很容易隐藏一些错误，特别是误加分号的错误。只有在赋值和调用时，表达式才应被当作一条单独的语句。

    //一行一条语句
    count++;
    doCount();

### return 语句

一条有返回值的return语句不要使用`( )`(括号)包裹返回值，除非在某种情况下可以让返回值更易理解。

    return MyCalc.getNumber();
    return (number > 10 ? currentNumber : MAX_NUMBER);

### 复合语句

复合语句是用`{ }`(花括号)包裹起来的语句序列。

- 花括号里的语句要多缩进一个层级。
- `{`(左花括号)应在复合语句起始行的末尾。
- `}`(右花括号)独占一行并与起始行左对齐。
- 所有复合语句，如`if`，`for`，都不能省略花括号，即使只有一条语句。


    if (condition) {
        statements
    }

### if 语句

if语句应如以下格式:

    if (condition){
        statements
    }
    
    if (condition) {
        statements
    } else {
        statements
    }
    
    if (condition) {
        statements
    } else if (condition) {
        statements
    } else {
        statements
    }

### for 语句

for语句应如以下格式:

    for (initialization; condition; update) {
        statements
    }

    for (variable in object) {
        statements
    }

第一种形式的循环用于已经知道相关参数的数组循环。

第二种形式应用于对象中。object原型中的成员将会被包含在迭代器中。通过hasOwnProperty方法来区分真正的object自有成员:

    for (variable in object) {
        if (object.hasOwnProperty(variable)){
            statements
    }

for语句的初始化部分不应当有变量声明。

    //建议写法
    var i,
        len;
    for (i = 0, len = 10; i < len; i++) {
        statements;
    }

### while 语句

while语句应如以下格式:

    while (condition){
        statements
    }

### do 语句

do语句应如以下格式:

    do {
        statements
    } while (condition);

注意do语句总是以`;`(分号)结尾。

### switch 语句

switch语句应如以下格式:

    switch (expression) {
        case expression:
            statements
            break;

        default:
            statements
    }
- 每一组`case`都保持一个缩进层级，每组`case`之间空一行
- 每一组statements，除了`default`应以 `break`，`return`，或者`throw`结尾，或者使用一行注释表示非无意的跳过。
- 对不包含`default`的情况，应当用注释代替，并注明原因。


    switch (value) {
        case 1:
            //pass

        case 2:
            doSomething();
            break;

        case 3:
            return true;

        case 4:
            throw new Error('value error');

        //没有default            
    }

### try 语句

try语句应如以下格式:

    try {
        statements
    } catch (error) {
        statements
    }

    try {
        statements
    } catch (error) {
        statements
    } finally {
        statements
    }


## 空白

用空行来将逻辑相关的代码块分割开可以提高程序的可读性。

在以下情况使用空行分隔。

- 方法直接。
- 方法中局部变量和第一行语句直接。
- 注释之前。
- 逻辑代码块直接用于提升可读性的地方。
- 类和接口定义直接。

在以下情况使用空格分隔。

- 关键词后跟括号时。
- 所有的二元操作符与操作数之间，除了`.`(点)、递增`++`、递减`--`。
- 赋值运算符和逻辑运算符之间。
- `for`语句中的表达式之间。
- 每个`,`(逗号)之后。


    for (i = 0, j = 10; i < j; i++) {
        if (i > 5 && typeof console !== 'undefined') {
            console.log(i);
        }
    }


## ===和!==操作符。

使用`===`和`!==`操作符。`==`和`!=`操作符会进行类型强制转换。特别是，不要将`==`用于与错值比较(`false`，`null`，`undefined`，`""`，`0`，`NaN`)。


## 赋值

赋值表达式右侧含有比较语句时，需要使用圆括号包裹。

    var foo = (i < 10);


## 需要避免的

- 不用使用`eval`。
- 不要使用`Function`构造函数。不要给`setTimeout`或者`setInterval`传递字符串参数。
- 不用使用像`String`一类的原始包装类创建新的对象，使用`''`代替`new String()`，使用`{}`代替`new Object()`。使用`[]`代替`new Array()`。
- 不要使用with语句。
- 避免在`if`和`while`语句的条件部分进行赋值。
