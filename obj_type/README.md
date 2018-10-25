# JavaScript数据类型


## 1. 根据标准划分

* 基本（原始）数据类型

```
 Boolean
 Null
 Undefined
 Number
 String
 Symbol (ECMAScript 6 新定义)
 Object
```

* 扩充数据类型 （都继承于Object）

```
 Math
 Date
 Array
 Function
 RegExp
```

* 宿主数据类型(由代码运行环境决定)

```
/*浏览器(BOM对象)*/
window
document
location
history
navigator
screen
frames
...//TODO
```

## 2. 根据存储方式的不同划分

* 值类型

```
 Boolean
 Null
 Undefined
 Number
 String
 Symbol (ECMAScript 6 新定义)
 /*所有基本数据类型，除了Object*/
```
* 引用类型

```
Object
/*所有的对象，无论是扩充还是宿主*/
```
* 区别

```
1，所有的值类型的值都直接存储在内存中，所有的引用类型的值都间接存储在内存中；
2，引用类型的变量名存储在内存中，只是记录一个地址，指向堆中该引用类型具体值的存储位置；
3，如果引用类型直接进行赋值操作，而不是创建新的存储空间后再赋值；
则接下来源数据的值发生变化时被赋值的数据源的值也跟着发生变化；
因为这个赋值只是赋予（复制）了一个相同的地址指向，而不是开辟了一份新的存储空间并把数据复制了一份，所以要格外注意。

简单打个比方：值类型就是现金可以直接用；引用类型就是存折，要用钱还得先去取
/*详见堆、栈和队列*/
```

## 3.Other


```
arguments、call、apply
define
require
export
import
```


