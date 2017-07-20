# 一、JavaScript入门
JavaScript是一种为网页交互而设计的交互语言，由以下三部分组成：
1. ECMAScript：核心语言功能
2. 文档对象模型（DOM）：访问操作网页内容
3. 浏览器对象模型（BOM）：与浏览器交互

## < script >标签的六个参数
- src:外部文件路径
- type：一般默认为text/javascript
- async：脚本是否立即下载（异步不保证先后顺序）
- defer：脚本是否延迟到文档完全被解析后再执行（按照先后顺序）
- charset：编码
- language：已废弃
---
# 二、JavaScript基本语法
## 语法
- 一切变量、函数和操作符**区分大小写**
- 标识符不可以以**数字**开头
- 起名格式最佳实践**驼峰大小写**
- 单行注释// 多行注释/**/
- 严格模式“use strict”：
  - 区别：严格模式是浏览器根据规范去显示页面；混杂模式是以一种向后兼容的方式去显示；
  - 意义：决定浏览器如何渲染网站；
  - 触发：浏览器根据doctype是否存在（严格）和使用的是那种dtd来决定。

## 变量
- 初始化变量var xxx，初始保存值为undefined；
- 定义在函数中的是局部变量，省略var则为全局变量；
- 可以但不推荐在修改变量值的同时修改变量数据类型；
- 一条语句同时声明多个变量的方式：
```var message = "hi", found = false, age = 29```

## 数据类型
**1. Undefined**
只有一个值，只声明未赋值的变量初始值都是undefined。

**2. Null**
只有一个值，是一个空对象指针，变量定义时如果将要用于保存对象，可将其初始化为null。

**3.Boolean**
有两个值true和false，转型函数Boolean()。

数据类型 | 转换为true | 转换为false
-|-|-
Boolean | true | false
String | 所有非空字符串 | ""
Number | 所有非零数值 | 0和NaN
Object | 所有对象 | null
Undefined | N/A | undefined

**4. Number**
- 八进制的第一位必须是0，十六进制的第一位必须是0x。
- NaN即非数值（Not a Number），用于表示一个本来要返回数值的操作数未返回数值的情况，与任何值都不相等。isNaN()用于判断参数是否“不是数值”。
- 数值转换：Number()、parseInt()、parseFloat()
```javascript
var num1 = Number("javascript");	//NaN
var num2 = Number("");	//0
var num3 = Number("0911");	//911
var num4 = Number(true);	//1

var num1 = parseInt("123javascript");	//123
var num2 = parseInt("");	//NaN
var num3 = parseInt(22.5);	//22
var num4 = parseInt(70);	//70
var num5 = parseInt(070);	//56 八进制
var num6 = parseInt(0xf);	//15 十六进制

var num1 = parseFloat("123javascript");	//123
var num2 = parseFloat("0xA");	//0 始终忽略前导零
var num3 = parseFloat(22.5);	//22.5
var num4 = parseFloat(22.34.5);	//22.34
var num5 = parseFloat(070.5);	//70.5
var num6 = parseFloat(3.125e7);	//31250000
```

**5. String**

- 可以由单引号或双引号表示，完全相同。
- x.toSting(y)，x代表将要转换为String类型的变量，y表示x是什么进制的数。

**6. Object**

- 创建自定义对象：```var o = new Object()```
- Object类型是其他所有实例的基础，它所有的属性和方法都被具体对象所继承：
 - constructor：构造函数
 - hasOwnProperty(propertyName)：检查给定属性在当前对象实例中是否存在
 -  propertyIsEnumerable(propertyName)：检查给定属性能否使用for-in语句来枚举
 - isPrototypeOf(object)：原型链
 - toLocaleString()：返回对象与执行环境地区对应的字符串表示
 - toString()：返回对象的字符串表示
 - valueOf()：返回对象的字符串、数值或布尔值表示，通常与前者相同
 ---
 # 三、操作符

**1. 一元操作符**
1)递增和递减操作符（++/--）：前置在被求值之前执行，后置在之后
2) 一元加和减操作符

**2. 位操作符**
1) 按位非（~）
2) 按位与（&）
3) 按位或（|）
4) 按位异或（^）:同为0异为1
5) 左移（<<）
6) 右移（>>）
```javascript
var old = 2;	//等于二进制的10
var new = old << 5;		//等于二进制的1000000，十进制的64
```

**3. 布尔操作符**
1) 逻辑与（&&）:如果第一个操作数可以决定结果，则不会再对第二个操作数求值。
2) 逻辑或（||）
3) 逻辑非（!）
```javascript
alert(!false);	//true
alert(!"blue");	//false
alert(!0);	//true
alert(!NaN);	//true
alert(!"");	//true
alert(!12345);	//false
```

**4. 乘性操作符**
1) 乘法（*）
2) 除法（/）
3) 求模（%）

**5. 加性操作符**
1) 加法：如果只有一个操作符是字符串，则将操作数转换为字符串，然后再将两个字符串拼接起来。
```var result = 5 + "5";	//"55"```
2) 减法

**6. 关系操作符**
小于（<）、大于（>）、小于等于（<=）、大于等于（>=）这几个关系操作符都返回一个布尔值。如果两个操作数都是字符串，则比较两个字符串所对应的字符编码值；如果其中一个是字符串，则将其转换为数值再进行比较。
```javascript
var result1 = "Brick" < "alphabet";	//true "B"的字符编码小于"a"
var result2 = "Brick".toLowerCase() < "alphabet".toLowerCase();	//false
var result3 = "23" < "3";	//true "2"的字符编码比"3"小
var result4 = "23" < 3;	//false "23"被转换为23 
```

**7. 相等操作符**
1)相等与不相等（==）：先转换再比较
2)全等与不全等（===）：不转换直接比较
```javascript
var result1 = ("55" == 55);	//true "55"被转换为55
var result2 = ("55" === 55);	//false
```

**8. 条件操作符**
```var max = (num1 > num2) ? num1 : num2	//取两者最大值```

**9. 赋值操作符**

**10. 逗号操作符**
```var num1 = 1, num2 = 2, num3 = 3```

---
# 四、语句
**1. if语句**
最佳实践是始终使用**代码块**：
```javascript
if(i >25) {
	alert("More than 25.");
} else if (i < 0) {
	alert("Less than 0.");
} else {
	alert("Between 0 and 25");
}
```

**2. do-while语句**
后测试循环语句，常用于循环体中代码至少要被执行一次的情形。
```javascript
do {
	statement
} while (expression);
```

**3. while语句**
前测试循环语句
```while(expression) statement```

**4. for语句**
前测试循环语句，使用while做不到的，for也做不到，只是把与循环相关的代码集中在了一个位置。
```for (;;)	//无限循环```

**5. for-in语句**
用来枚举对象的属性
```javascript
for (var propName in window) {
	document.write(propName);
}
```

**6. label语句**
在代码中添加标签，与for语句等配合使用。

**7. break和continue语句**
break语句立即退出循环，强制继续执行循环后面的语句；
continue语句立即退出循环，但退出后会从循环的顶部继续执行。
```javascript
var num = 0;
for (var i=1; i < 10; i++) {
	if (i % 5 == 0) {
		//break;continue;
	}
	num++;
}
alert(num);	//4,8
```

**8. with语句**
将代码的作用域设置到一个特定对象中，严格模式不允许使用。

**9. switch语句**
```javascript
switch (i) {
	case 1:
		alert("1");
		break;
	case 2:
		alert("2");
		break;
	case 3:
		alert("3");
		break;
	default:
		alert("Other");
}
```
---
# 五、函数
```javascript
function name(arg0, arg1，...，argN) {
	statements
};
```
1) 函数在定义时不必指定是否返回值；
2) 函数在执行return语句之后停止并立即退出，其后的任何代码永远不会执行；
3) return语句也可以不带有任何返回值，只用作停止函数，将会返回一个undefined值；
4) 参数类型、个数完全自由，可以通过arguments对象访问参数数组，arguments.length获取参数个数，arguments和参数对应值保持同步；
```javascript
function doAdd() {
	alert(arguments.length);
	if(arguments.length == 1) {
		alert(arguments[0] + 10);
	} else if (arguments.length == 2) {
		alert(arguments[0] + arguments[1]);
	}
}
doAdd(10);	//1,20
doAdd(30, 20);	//2,50
```
5) 没有传递值得命名参数将被自动赋予undefined值；
6) 没有函数签名，无法实现函数重载。
---

# 六、变量
**1. 数据类型**
变量包含两种不同的数据类型值：基本类型值和引用类型值，基本类型值指简单的数据段，包含Undefined、Null、Boolean、Number、String五种，引用类型是保存在内存中的对象，不能直接操作它的内存空间。

**2. 变量复制**
1) 基本类型变量复制，两个变量相互独立，可以参与任何操作而不会受相互影响。
2) 引用类型变量复制，两个变量引用同一个对象，改变其中一个变量，就会影响另一个变量
```javascript
var obj1 = new Object();
var obj2 = obj1;
obj1.name = 'TsingM';
alert(obj2.name);	//'TsingM'
```

**3. 传递参数**
函数参数相当于局部变量，也是一个简单的复制，不会影响到外部变量值。

**4. 检测类型**
1) typeof用于检测变量类型，引用类型统一返回Object。
2) instanceof用于检测具体的引用类型，类型包括Oject，Array，RegExp等。

## 执行环境及作用域
1) 执行环境分为全局执行环境和函数执行环境；
2) 每次进入一个新的执行环境，都会创建一个用于搜索变量和函数的作用域链；
3) 函数的局部环境不仅可以访问函数作用域中的变量，也有权访问父环境以及全局环境；
4) 父环境不能访问子环境中的变量；
5) 搜索变量值时按照由内而外的顺序向上级依次查找。

## 垃圾回收
1) 离开作用域的值将被自动标记为可以回收，因此将在垃圾收集期间被删除；
2) “标记清除”是目前主流回收算法，给不使用的值加上标记，然后回收其内存；
3) 另一种回收算法叫“引用计数”，不常使用；
4) 手动解除变量的引用有助于消除循环引用现象，对垃圾收集有益，即将变量设为空值null。
---
# 七、对象
## 1. new后面接构造函数
```javascript
var person = new Object();
person.name = "TsingM";
person.age = 24;
```
## 2. 对象字面量
```javascript
var person = {
	name : "TsingM",
	age : 24
}
```
可用于向函数传递大量可选参数
```javascript
function display(args) {
	xxxxxx
}
display({
	name: "TsingM",
	age: 29
});
```
JavaScript也可以使用方括号来访问对象的属性，其优点为可通过变量访问、避免语法错误。
```javascript
var proName = "name";
alert(person[proName]);
```
```javascript
person["first name"] = "TsingM";
```
---
# 八、数组
***数组的每一项可以保存任何类型的数据，例如第一个位置保存字符串，第二个位置保存数值，第三个位置保存对象......***
## Array类型创建方式
```javascript
var colors = new Array();
var colors = ["red", "blue", "green"];
```
## length属性
数组的项数保存在length中，始终会返回0或更大的值，可用于从数组末尾移除项或添加新项。
```javascript
var colors = ["red", "blue", "green"];
colors.length = 2;	//删除第三项
alert(colors[2]);	//undefined
colors[colors.length] = "green";	//添加第三项
alert(colors[2]);	//"green"
```

## 转换方法(toString, valuesOf)
```javascript
var colors = ["red", "blue", "green"];
alert(colors.toString());	//red,blue,green
alert(colors.valuesOf());	//red,blue,green
alert(colors);	//red,blue,green
```

## 栈方法（push, pop）
push()方法可以将参数逐个添加到数组**末尾**，返回修改后的长度；
pop()方法可以从数组末尾移除**最后一项**，并返回该项；
```javascript
var colors = new Array();
var count = colors.push("red","green");	//2
var items = colors.pop();	//"green"
```

## 队列方法（unshift, shift）
unshift()方法可以将参数逐个添加到数组**开头**，返回修改后的长度；
shift()方法可以从数组开头移除**第一项**，并返回该项；
```javascript
var colors = new Array();
var count = colors.unshift("red","green");	//2
var items = colors.shift();	//"red"
```

## 重排序方法（reverse, sort）
reverse()方法会反转数组的顺序；
sort()方法会升序排列数据项，默认当做字符串按照ASCII排列而不是数值；
想让sort()方法按照数值顺序升、降序排列，需要自写比较函数：
```javascript
var values = [0, 15, 123, 20, -1];
values.sort();	//[-1, 0, 123, 15, 20]
values.sort(function(a, b){return a - b;});	//[-1, 0, 15, 20, 123]
values.sort(function(a, b){return b - a;});	//[123, 20, 15, 0, -1]
```

## 操作方法（concat, slice， splice）
concat()方法可以基于当前数组中的所有项创建一个新数组；
```javascript
var colors = ["red", "green", "blue"];
var colors2 = colors.concat("yellow", ["black", "brown"]);	//["red", "green", "blue", "yellow", "black", "brown"]
```
slice()方法可以基于当前数组中的一个或多个项创建一个新数组，可接受一至两个参数，即要返回的起始和结束位置，新数组包括起始位置但不包括结束位置；
```javascript
var colors = ["red", "green", "blue"];
var colors2 = colors.slice(1);	//["green", "blue"]
var colors3 = colors.slice(0, 2);	//["red", "green"]
```
splice()方法主要用途是向数组的中部插入项，可以实现删除、插入、替换三种操作，返回删除项。三个参数分别为：起始位置、删除长度、替换项（可选）；
```javascript
var colors = ["red", "green", "blue"];
var removed = colors.splice(0, 1);	//删除第一项 ["green", "blue"]
removed = colors.splice(1, 0, "yellow", "orange");	//从位置1开始插入两项 ["green", "red", "yellow", "orange", "blue"]
removed = colors.splice(1, 1, "white", "purple");	//插入两项删除一项 ["green", "white", "purple", "yellow", "orange", "blue"]
```

## 位置方法（indexOf, lastIndexOf）
两个方法都接收两个参数：要查找的项和表示查找起点位置的索引（可选），其中indexOf()方法从数组的开头**向后**查找，lastIndexOf()方法从数组的末尾**向前**查找。
两者都返回查找项在数组中的位置，或者在没找到的情况下返回-1。
```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
numbers.indexOf(4);	//3
numbers.lastIndexOf(4);	//5
numbers.indexOf(4, 4);	//5
numbers.lastIndexOf(4, 4);	//3
```

## 迭代方法（every, filter, forEach, map, some）
该类方法都接收三个参数：数组项的值、该项在数组中的位置、数组对象本身。
作用都是对数组中的每一项运行给定函数，返回值相互不同：
every()方法：如果该函数对**每**一项都返回true，则返回true；
some()方法：如果该函数对**任意**一项返回true，则返回true；
filter()方法：返回该函数会返回true的项组成的数组；
forEach()方法：没有返回值；
map()方法：返回每次函数调用的结果组成的数组；
```javascript
var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
numbers.forEach(function(item, index, array) {
	//执行操作
});
```

## 归并方法（reduce, reduceRight）
两个方法都会迭代数组的所有项，然后构建一个最终返回的值，前者从前往后遍历，后者从后往前。
两个方法都接收两个参数：一个在每一项上调用的函数和作为归并基础的初始值（可选）。
调用的函数接收四个参数：前一个值、当前值、项的索引、数组对象。
可用于数组求和操作：
```javascript
var values = [1, 2, 3, 4, 5];
var sum = values.reduce(function(prev, cur, index, array) {
	return prev+cur;
});	//15
```