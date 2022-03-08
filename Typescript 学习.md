# Typescript 学习

## 特性

typescript 是一种给 javascript 添加特性的语言拓展，增加的功能包括：

- 类型批注和编译时类型检查
- 类型推断
- 类型擦除
- 接口
- 枚举
- Mixin
- 泛型编程
- 名字空间
- 元组
- Await

![img](Typescript 学习.assets/ts-2020-11-26-2.png)

![img](Typescript 学习.assets/ts-2020-11-26-1.png)

## 实现原理

typescript 是 javascript 的扩充，运行 typescript 需要先将其编译成 javascript，然后使用 node 一类的 javascript 引擎运行

![img](Typescript 学习.assets/ts-2020-12-01-1.png)

## 基础类型

| 数据类型   | 关键字    | 描述                                                         |
| :--------- | :-------- | :----------------------------------------------------------- |
| 任意类型   | any       | 声明为 any 的变量可以赋予任意类型的值。                      |
| 数字类型   | number    | 双精度 64 位浮点值。它可以用来表示整数和分数。`let binaryLiteral: number = 0b1010; // 二进制 let octalLiteral: number = 0o744;    // 八进制 let decLiteral: number = 6;    // 十进制 let hexLiteral: number = 0xf00d;    // 十六进制` |
| 字符串类型 | string    | 一个字符系列，使用单引号（**'**）或双引号（**"**）来表示字符串类型。反引号（**`**）来定义多行文本和内嵌表达式。`let name: string = "Runoob"; let years: number = 5; let words: string = `您好，今年是 ${ name } 发布 ${ years + 1} 周年`;` |
| 布尔类型   | boolean   | 表示逻辑值：true 和 false。`let flag: boolean = true;`       |
| 数组类型   | 无        | 声明变量为数组。`// 在元素类型后面加上[] let arr: number[] = [1, 2]; // 或者使用数组泛型 let arr: Array<number> = [1, 2];` |
| 元组       | 无        | 元组类型用来表示已知元素数量和类型的数组，各元素的类型不必相同，对应位置的类型需要相同。`let x: [string, number]; x = ['Runoob', 1];    // 运行正常 x = [1, 'Runoob'];    // 报错 console.log(x[0]);    // 输出 Runoob` |
| 枚举       | enum      | 枚举类型用于定义数值集合。`enum Color {Red, Green, Blue}; let c: Color = Color.Blue; console.log(c);    // 输出 2` |
| void       | void      | 用于标识方法返回值的类型，表示该方法没有返回值。`function hello(): void {    alert("Hello Runoob"); }` |
| null       | null      | 表示对象值缺失。                                             |
| undefined  | undefined | 用于初始化变量为一个未定义的值                               |
| never      | never     | never 是其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。 |

**注意：**TypeScript 和 JavaScript 没有整数类型。

## 变量声明

### 类型定义

- 不带类型限制

  ``` typescript
  //var [变量] = 值;
  var a = "hello";
  ```

- 带类型限制

  ``` typescript
  //var [变量] : [类型] = 值;
  var a:string = "hello";
  ```

typescript 可以有联合类型

联合类型（Union Types）可以通过管道(|)将变量设置多种类型，赋值时可以根据设置的类型来赋值。

**注意**：只能赋值指定的类型，如果赋值其它类型就会报错。

例如：

``` typescript
var val:string|number 
val = 12 
console.log("数字为 "+ val) 
val = "Runoob" 
console.log("字符串为 " + val)
```

typescript 可以只定义变量不赋初始值

typescript 的变量是强类型约束的

### 类型断言

类型断言可以手动指定一个指的类型，让其从一种类型更改为另一种类型

``` typescript
//语法格式
//<类型>值
//值 as 类型
var str = '1' 
var str2:number = <number> <any> str   //str、str2 是 string 类型
console.log(str2)
```

当 S 类型是 T 类型的子集，或者 T 类型是 S 类型的子集时，S 能被成功断言成 T。这是为了在进行类型断言时提供额外的安全性，完全毫无根据的断言是危险的，如果你想这么做，你可以使用 any。

它之所以不被称为**类型转换**，是因为转换通常意味着某种运行时的支持。但是，类型断言纯粹是一个编译时语法，同时，它也是一种为编译器提供关于如何分析代码的方法。

## 函数

### 返回值

typescript可以规定函数的返回值

例如：

``` typescript
function function_name():string { 
    // 语句
    return value; 
}
```

它规定函数必须返回一个 string 类型的值，不返回或返回其他类型的值无法进行编译。

### 参数

typescript 函数携带参数时可以对参数的类型进行限定

``` typescript
function add(x: number, y: number): number {
    return x + y;
}
console.log(add(1,2))
```

### 可选参数

在 TypeScript 函数里，如果我们定义了参数，则我们必须传入这些参数，除非将这些参数设置为可选，可选参数使用问号标识 ？。

``` typescript
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}
 
let result1 = buildName("Bob");  // 正确
let result2 = buildName("Bob", "Adams", "Sr.");  // 错误，参数太多了
let result3 = buildName("Bob", "Adams");  // 正确
```

### 默认参数

我们也可以设置参数的默认值，这样在调用函数的时候，如果不传入该参数的值，则使用默认参数，语法格式为：

```
function function_name(param1[:type],param2[:type] = default_value) { 
}
```

注意：参数不能同时设置为可选和默认。

以下实例函数的参数 rate 设置了默认值为 0.50，调用该函数时如果未传入参数则使用该默认值：

``` typescript
function calculate_discount(price:number,rate:number = 0.50) { 
    var discount = price * rate; 
    console.log("计算结果: ",discount); 
} 
calculate_discount(1000) 
calculate_discount(1000,0.30)
```

### 剩余参数

有一种情况，我们不知道要向函数传入多少个参数，这时候我们就可以使用剩余参数来定义。

剩余参数语法允许我们将一个不确定数量的参数作为一个数组传入。

``` typescript
function addNumbers(...nums:number[]) {  
    var i;   
    var sum:number = 0; 
    
    for(i = 0;i<nums.length;i++) { 
       sum = sum + nums[i]; 
    } 
    console.log("和为：",sum) 
 } 
 addNumbers(1,2,3) 
 addNumbers(10,10,10,10,10)
```

### 匿名函数

匿名函数是没有函数名称的函数，除了没有函数名称以外与正常函数没有太大的差异

例如：

``` typescript
var msg = function() { 
    return "hello world";  
} 
console.log(msg())
```

### Lambda 函数

也被称之为箭头函数

例如：

``` typescript
var foo = (x:number)=>10 + x 
console.log(foo(100))      //输出结果为 110
```

### 函数重载

重载是方法名字相同，而参数不同，返回类型可以相同也可以不同。

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

- 参数类型不同：

    ```typescript
    function disp(string):void; 
    function disp(number):void;
    ```

- 参数数量不同：

    ```typescript
    function disp(n1:number):void; 
    function disp(x:number,y:number):void;
    ```

- 参数类型顺序不同：

    ```typescript
    function disp(n1:number,s1:string):void; 
    function disp(s:string,n:number):void;
    ```

## 接口

### 概念

接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。

具体实现：

``` typescript
interface IPerson { 
    firstName:string, 
    lastName:string, 
    sayHi: ()=>string 
} 
 
var customer:IPerson = { 
    firstName:"Tom",
    lastName:"Hanks", 
    sayHi: ():string =>{return "Hi there"} 
} 
 
console.log("Customer 对象 ") 
console.log(customer.firstName) 
console.log(customer.lastName) 
console.log(customer.sayHi())  
 
var employee:IPerson = { 
    firstName:"Jim",
    lastName:"Blakes", 
    sayHi: ():string =>{return "Hello!!!"} 
} 
 
console.log("Employee  对象 ") 
console.log(employee.firstName) 
console.log(employee.lastName)
```

### 接口和函数

我们也可以使用接口来预定义函数结构

``` typescript
interface encypt{
	(key:string, value:string):string;
}

var md5:encypt = function (key, value):string{
	return key + ' ' + value // 模拟加密操作
}
console.log(md5('李', '二狗'))

var sha1:encypt = function(key, value):string{
	return key + '--' + value
}
console.log(sha1('dog', 'zi'))
————————————————
版权声明：本文为CSDN博主「bus_lupe」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/bus_lupe/article/details/91346827
```

### 接口和数组

我们可以按需设置数组索引和值的数据类型

``` typescript
interface namelist { 
   [index:number]:string 
} 
 
var list2:namelist = ["John",1,"Bran"] // 错误元素 1 不是 string 类型
interface ages { 
   [index:string]:number 
} 
 
var agelist:ages; 
agelist["John"] = 15   // 正确 
agelist[2] = "nine"   // 错误
```

### 接口继承

接口可以按照需要进行继承，允许单继承也允许多继承

单接口继承语法格式：

```typescript
Child_interface_name extends super_interface_name
```

``` typescript
interface Person { 
   age:number 
} 
 
interface Musician extends Person { 
   instrument:string 
} 
 
var drummer = <Musician>{}; 
drummer.age = 27 
drummer.instrument = "Drums" 
console.log("年龄:  "+drummer.age)
console.log("喜欢的乐器:  "+drummer.instrument)
```

多接口继承语法格式：

```typescript
Child_interface_name extends super_interface1_name, super_interface2_name,…,super_interfaceN_name
```

``` typescript
interface IParent1 { 
    v1:number 
} 
 
interface IParent2 { 
    v2:number 
} 
 
interface Child extends IParent1, IParent2 { } 
var Iobj:Child = { v1:12, v2:23} 
console.log("value 1: "+Iobj.v1+" value 2: "+Iobj.v2)
```

## 类

### 特征

typescript 的类定义和 javascript 类似

### 继承

typescript 的类支持单继承，不支持多继承，但支持多重继承

语法格式：

``` typescript
class child_class_name extends parent_class_name
```

### 继承类的方法重写

类继承后，子类可以对父类的方法重新定义，这个过程称之为方法的重写。

其中 super 关键字是对父类的直接引用，该关键字可以引用父类的属性和方法。

``` typescript
class PrinterClass { 
   doPrint():void {
      console.log("父类的 doPrint() 方法。") 
   } 
} 
 
class StringPrinter extends PrinterClass { 
   doPrint():void { 
      super.doPrint() // 调用父类的函数
      console.log("子类的 doPrint()方法。")
   } 
}
```

### static 关键字

static 能将类的成员方法和属性设置为静态类型

``` typescript
class StaticMem {  
   static num:number; 
   
   static disp():void { 
      console.log("num 值为 "+ StaticMem.num) 
   } 
} 
 
StaticMem.num = 12     // 初始化静态变量
StaticMem.disp()       // 调用静态方法
```

### 访问控制修饰符

TypeScript 中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。TypeScript 支持 3 种不同的访问权限。

- **public（默认）** : 公有，可以在任何地方被访问。
- **protected** : 受保护，可以被其自身以及其子类访问。
- **private** : 私有，只能被其定义所在的类访问。

以下实例定义了两个变量 str1 和 str2，str1 为 public，str2 为 private，实例化后可以访问 str1，如果要访问 str2 则会编译错误。

``` typescript
class Encapsulate { 
   str1:string = "hello" 
   private str2:string = "world" 
}
 
var obj = new Encapsulate() 
console.log(obj.str1)     // 可访问 
console.log(obj.str2)   // 编译错误， str2 是私有的
```

### 类和接口

类也可以实现接口，例如：

``` typescript
interface ILoan { 
   interest:number 
} 
 
class AgriLoan implements ILoan { 
   interest:number 
   rebate:number 
   
   constructor(interest:number,rebate:number) { 
      this.interest = interest 
      this.rebate = rebate 
   } 
} 
 
var obj = new AgriLoan(10,1) 
console.log("利润为 : "+obj.interest+"，抽成为 : "+obj.rebate )
```

## 对象

对象是包含一组键值对的实例。 值可以是标量、函数、数组、对象等，如下实例：

``` javascript
var object_name = { 
    key1: "value1", // 标量
    key2: "value",  
    key3: function() {
        // 函数
    }, 
    key4:["content1", "content2"] //集合
}
```

在 javascript 中，我们可以有如下操作：

``` javascript
var sites = { 
   site1:"Runoob", 
   site2:"Google" 
};

sites.sayHello = function(){ return "hello";}
```

这样在 javascript 中，这样的操作是正确可执行的

如果在 typescript 中，会出现编译错误，在 typescript 中应该添加类型模板

``` typescript
var sites = {
    site1: "Runoob",
    site2: "Google",
    sayHello: function () { } // 类型模板
};
sites.sayHello = function () {
    console.log("hello " + sites.site1);
};
sites.sayHello();
```

在 typescript 中，对象可以作为参数传入函数中

## 命名空间

### 概念

在 typescript 中可以使用 namespace 来解决命名重复的问题，语法格式类似：

``` typescript
namespace SomeNameSpaceName { 
   export interface ISomeInterfaceName {      }  
   export class SomeClassName {      }  
}
```

以上定义了一个命名空间 SomeNameSpaceName，如果我们需要在外部可以调用 SomeNameSpaceName 中的类和接口，则需要在类和接口添加 **export** 关键字。

要在另外一个命名空间调用语法格式为：

```typescript
SomeNameSpaceName.SomeClassName;
```

如果一个命名空间在一个单独的 TypeScript 文件中，则应使用三斜杠 /// 引用它，语法格式如下：

```typescript
/// <reference path = "SomeFileName.ts" />
```

IShape.ts 文件代码：

``` typescript
namespace Drawing { 
    export interface IShape { 
        draw(); 
    }
}
```

Circle.ts 文件代码：

``` typescript
/// <reference path = "IShape.ts" /> 
namespace Drawing { 
    export class Circle implements IShape { 
        public draw() { 
            console.log("Circle is drawn"); 
        }  
    }
}
```

Triangle.ts 文件代码：

``` typescript
/// <reference path = "IShape.ts" /> 
namespace Drawing { 
    export class Triangle implements IShape { 
        public draw() { 
            console.log("Triangle is drawn"); 
        } 
    } 
}
```

TestShape.ts 文件代码：

``` typescript
/// <reference path = "IShape.ts" />   
/// <reference path = "Circle.ts" /> 
/// <reference path = "Triangle.ts" />  
function drawAllShapes(shape:Drawing.IShape) { 
    shape.draw(); 
} 
drawAllShapes(new Drawing.Circle());
drawAllShapes(new Drawing.Triangle());
```

### 嵌套

命名空间支持嵌套，用法：

``` typescript
namespace namespace_name1 { 
    export namespace namespace_name2 {
        export class class_name {    } 
    } 
}
```

Invoice.ts 文件代码：

``` typescript
namespace Runoob { 
   export namespace invoiceApp { 
      export class Invoice { 
         public calculateDiscount(price: number) { 
            return price * .40; 
         } 
      } 
   } 
}
```

InvoiceTest.ts 文件代码：

``` typescript
/// <reference path = "Invoice.ts" />
var invoice = new Runoob.invoiceApp.Invoice(); 
console.log(invoice.calculateDiscount(500));
```

## 声明文件

TypeScript 作为 JavaScript 的超集，在开发过程中不可避免要引用其他第三方的 JavaScript 的库。虽然通过直接引用可以调用库的类和方法，但是却无法使用TypeScript 诸如类型检查等特性功能。为了解决这个问题，需要将这些库里的函数和方法体去掉后只保留导出类型声明，而产生了一个描述 JavaScript 库和模块信息的声明文件。通过引用这个声明文件，就可以借用 TypeScript 的各种特性来使用库文件了。

假如我们想使用第三方库，比如 jQuery，我们通常这样获取一个 id 是 foo 的元素：

```javascript
$('#foo');
// 或
jQuery('#foo');
```

但是在 TypeScript 中，我们并不知道 $ 或 jQuery 是什么东西：

```typescript
jQuery('#foo');

// index.ts(1,1): error TS2304: Cannot find name 'jQuery'.
```

这时，我们需要使用 declare 关键字来定义它的类型，帮助 TypeScript 判断我们传入的参数类型对不对：

```typescript
declare var jQuery: (selector: string) => any;

jQuery('#foo');
```

declare 定义的类型只会用于编译时的检查，编译结果中会被删除。

上例的编译结果是：

```javascript
jQuery('#foo');
```

声明文件以 **.d.ts** 为后缀，例如：

```
runoob.d.ts
```

声明文件或模块的语法格式如下：

```typescript
declare module Module_Name {
}
```

TypeScript 引入声明文件语法格式：

```typescript
/// <reference path = " runoob.d.ts" />
```

案例：

第三方库 CalcThirdPartyJsLib.js：

``` typescript
var Runoob;  
(function(Runoob) {
    var Calc = (function () { 
        function Calc() { 
        } 
    })
    Calc.prototype.doSum = function (limit) {
        var sum = 0; 
 
        for (var i = 0; i <= limit; i++) { 
            sum = sum + i; 
        }
        return sum; 
    }
    Runoob.Calc = Calc; 
    return Calc; 
})(Runoob || (Runoob = {})); 
var test = new Runoob.Calc();
```

要在 typescript 中使用，可以设置声明文件 Calc.d.ts：

``` typescript
declare module Runoob { 
   export class Calc { 
      doSum(limit:number) : number; 
   }
}
```

声明文件不包含实现，它只是类型声明，把声明文件加入到 TypeScript 中：

``` typescript
/// <reference path = "Calc.d.ts" /> 
var obj = new Runoob.Calc(); 
// obj.doSum("Hello"); // 编译错误
console.log(obj.doSum(10));
```

