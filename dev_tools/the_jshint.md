# 关于jshint的配置


```
JSHint默认使用用户当前目录下的.jshintrc文件（json格式）作为配置文件
```
[英文文档](https://jshint.com/docs/options/)


###  jshint配置

-------

**各种配置方式**

* 命令行通过 –config 选项手动指定配置文件;

* 通过 在package.json中的添加标记手动配置;

```
"jshintConfig": {
    "undef": true,
    "unused": true,
    "predef": [
      "MY_GLOBAL",
      "ads"
    ]
  }
```

* 使用 .jshintrc 文件；

```
运行时jshint会从当前路径下开始，一层一层往上找
```
```
/**示例配置**/
{
  "sub":true,
  "laxbreak":true,
  "laxcomma":true,
  "regexp":true,
  "asi": true,
  "browser": true,
  "loopfunc":true,
  "expr":true,
  "node": true,
  "es5": true,
  "esnext": true,
  "bitwise": true,
  "curly": true,
  "immed": true,
  "latedef": false,
  "expr": true,
  "eqeqeq": false,
  "eqnull": false,
  "newcap": true,
  "noarg": true,
  "undef": true,
  "proto": true,
  "strict": false,
  "smarttabs": true
}
```

* 内联配置；


除了使用配置文件,您可以在你的文件中使用jshint或者globals开头，
并跟着配置项以冒号分隔值列表来配置JSHint。


例如,下面的代码片段将启用警告未定义的和未使用的变量和告诉JSHint全局变量命名MY_GLOBAL。

```
/* jshint undef: true, unused: true */
/* globals MY_GLOBAL */
```

可以使用单行或者多行来配置JSHint，如果放在函数里面，则只影响该函数。
ignore 告诉jshint忽略一个代码块

```
// Code here will be linted with JSHint.
/* jshint ignore:start */
// Code here will be ignored by JSHint.
/* jshint ignore:end */
```
上面的代码在jshint ignore:start和 ignore:end之间的所有代码都将被JSHint忽略;

或者忽略一行:

```
ignoreThis(); // jshint ignore:line
```

以上都只是示例，具体使用的话还是去看文档吧，orz -_-|||


### JSHint配置文件中的规则有3类：

-------

```
Enforcing: 这些规则被置为true，JSHint会对代码进行更严格的检查。
Relaxing: 这些规则被置为true，JSHint会容忍规则中定义的情况出现。
Environment: 这些规则被置为true，JSHint会认为代码默认有一些全局变量
```
> 1.校验选项：Enforcing


```
bitwise
禁用位运算符，位运算符在 JavaScript 中使用较少，经常是把 && 错输成 &。
bitwise: true
```


```
camelcase
警告:此选项已被弃用,将在JSHint的下一个主要版本被删除.
此选项可以强制所有变量名称为使用驼峰风格或UPPER_CASE用下划线。
camelcase:true/false
```

```
curly
循环或者条件语句必须使用花括号包围.
这个选项需要你总是把花括号在块循环和条件。JavaScript块时可以省略括号包含只有一个语句,例如:
while (day)
shuffle();
然而,在某些情况下,它会导致错误(你可能会认为 sleep()是一个循环的一部分,而事实上它不是)
while (day)
shuffle();
sleep();
```

```
enforceall
警告:此选项已被弃用,将在JSHint的下一个主要版本被删除.
它启用所有强制执行选项和禁用该版本中定义的所有的Relaxing options；
```


```
eqeqeq
设置为true,禁止使用这个选项 ==和 !=，强制使用 ===和 !==。
eqeqeq: true
```
```
es3
警告:此选项将在JSHint的下一个主要版本被删除,使用esversion: 3代替.
使用ECMAScript 3规范。使用这个选项主要为了兼容低级浏览器 IE 6/7/8/9-and其他遗留JavaScript环境。
```

```
es5
警告:此选项将被删除在JSHint的下一个主要版本，使用 esversion: 5代替。
这个选项允许语法中定义ECMAScript 5.1规范，这包括允许保留关键字作为对象属性。
```

```
esversion
这个选项用于指定的ECMAScript版本代码必须遵循。它可以假设以下值之一:
3--如果你需要可执行程序在老这类浏览器Internet Explorer 6/7/8/9-and其他遗留JavaScript环境
5--先使语法中定义ECMAScript 5.1规范。这包括允许保留关键字作为对象属性。
6--告诉JSHint代码使用ECMAScript 6具体的语法。请注意,并不是所有的浏览器都实现它们。
```
```
forin
这个选项要求所有 for in循环过滤对象的item。他在声明中允许for遍历一个对象所有属性的名称包括通过原型链继承来的属性。
for (key in obj) {
if (obj.hasOwnProperty(key)) {
// We are sure that obj[key] belongs to the object and was not inherited.
}
}
```

```
freeze
这个选项禁止重写原生对象的原型列如 Array, Date等等。
```

```
funcscope
禁止从外部访问内部声明的变量
function test() {
if (true) {
var x = 0;
}
x += 1; // Default: 'x' used out of scope.
// No warning when funcscope:true
}
```

```
futurehostile
允许警告js未来版本中定义的标识符。
```

```
globals
这个选项可以用来指定一个没有正式定义的全局变量的白名单。
配置 globals在单个文件,看看内联配置.
```

```
immed
警告:此选项已被弃用,将在JSHint的下一个主要版本被删除。
需要直接调用的函数必须被括号包围，如：（function（）{}（））;
```

```
indent
警告:此选项将在JSHint的下一个主要版本被删除。
设置代码缩进长度
```

```
iterator
禁止iterator属性有关的警告。
此属性不支持所有浏览器所以小心使用它。
```

```
latedef
禁止定义之前使用变量。
这个选项设置为“nofunc”将允许函数声明被忽略。
```

```
maxcomplexity
设置代码文件独立直线路径最大复杂度检测。
```

```
maxdepth
设置代码最大嵌套深度。
// jshint maxdepth:2
function main(meaning) {
var day = true;
if (meaning === 42) {
while (day) {
shuffle();
if (tired) {
// JSHint: Blocks are nested too deeply (3).
sleep();
}
}
}
}
```

```
maxerr
设置JSHint最大警告数。默认50
```

```
maxlen
警告:此选项将在JSHint的下一个主要版本被删除
设置最大行数
```

```
maxparams
这个选项允许您设置每个函数的形参最大数量
// jshint maxparams:3
function login(request, onSuccess) {
// ...
}
// JSHint: Too many parameters per function (4).
function logout(request, isManual, whereAmI, onSuccess) {
 // ...
}
```

```
maxstatements
这个选项允许您设置语句允许的最大声明数:
// shint maxstatements:4
function main() {
var i = 0;
var j = 0;
// Function declarations count as one statement. Their bodies
// don't get taken into account for the outer function.
function inner() {
var i2 = 1;
var j2 = 1;
return i2 + j2;
}
j = i + j;
return j; // JSHint: Too many statements per function. (5)
}
函数也算声明。
```

```
newcap
警告此选项已被弃用,将被删除在JSHint的下一个主要版本
要求所有构造器使用new F()形式。
```

```
noarg
禁止使用这个选项 arguments.caller和 arguments.callee。这两个 .caller
和.callee将会被弃用。事实上,ECMAScript 5 严格模式禁止使用arguments.callee
```

```
nocomma
这个选项禁止使用逗号操作符。
```

```
noempty
警告此选项已被弃用,将被删除在JSHint的下一个主要版本。
空代码块警告。
```

```
nonbsp
不换行的空格警告
```

```
nonew
这个选项禁止使用new构造器函数。有些人喜欢调用构造函数，但是不赋值给任何对象:
new MyConstructor();
```

```
notypeof
检查无效 typeof操作符的值
// 'fuction' instead of 'function'
if (typeof a == "fuction") { // Invalid typeof value 'fuction'
// ...
}
```

```
predef
扩展的隐式全局变量
```

```
quotmark
警告此选项已被弃用,将被JSHint的下一个主要版本删除。
这个选项执行代码中使用引号的一致性。它接受三个值:

true-- 代码字符串禁止单引号双引号混用,

"single"--只允许单引号

"double"--只允许双引号。
```

```
shadow
检查变量重复定义
他接受4个值：

"inner" 只检查是否在相同的作用域重复定义

"outer" 检查外部作用域

false 与inne一样

true 允许变量覆盖
```

```
singleGroups
禁止使用分组操作符
// jshint singleGroups: true
delete(obj.attr); // Warning: Unnecessary grouping operator.
```

```
strict
ECMAScript 5严格模式

"global" - 全局层面的严格模式"use strict";

"implied" - 文件里面使用"use strict";

false - 禁止使用严格模式

true - 函数上面必须使用一个"use strict";
```

```
undef
变量未定义
// jshint undef:true
function test() {
var myVar = 'Hello, World';
// Oops, typoed here. JSHint with undef will complain
console.log(myvar);
}
如果你的另一个文件中定义的变量,你可以使用 global指令告诉JSHint。
```

```
unused
变量定义未使用
// jshint unused:true
function test(a, b) {
var c, d = 2;
return a + d;
}
test(1, 2);
// Line 3: 'b' was defined but never used.
// Line 4: 'c' was defined but never used
```

```
varstmt
设置为true时，禁止使用var声明变量
// jshint varstmt: true
var a; // Warning: var declarations are forbidden. Use let or const instead.
```
> 2.宽松选项：Relaxing
> 设置为true时,这些选项会使代码JSHint产生更少的警告。

```
asi
禁止缺少分号警告
```

```
boss
禁止比较表达式的值没有达到预期警告。
通常情况下,代码 if (a = 10) {}是一个错误,但他有可能这样用
for (var i = 0, person; person = people[i]; i++) {}
你可以禁止这个错误，比如
for (var i = 0, person; (person = people[i]); i++) {}
```

```
debug
忽略 debugger
```

```
elision
告诉JSHint代码使用ES3数组省略元素,或空元素(例如, [1, , , 4, , , 7]
).
```

```
eqnull
禁止 == null比较。通常这样的比较有用,当你想检查一个变量是否null
或 undefined
```

```
eqnull
警告此选项将在JSHint的下一个主要版本被 esversion: 6代替
使用ECMAScript 6具体语法，有些浏览器不支持
```

```
evil
禁止使用eval
```

```
expr
禁止使用表达式，一般的使用函数调用。
```

```
globalstrict
下个版本中会使用 strict: "global"代替。
全局严格模式会和第三方小插件冲突，所以不推荐使用。
```

```
lastsemic
检查一行代码最后声明后面的分号是否遗漏
var name = (function() { return 'Anton' }());
```

```
laxbreak
检查不安全的折行(下个版本将被删除)
```

```
laxcomma
检查逗号在代码行最前面的编程风格
var obj = {
name: 'Anton'
, handle: 'valueof'
, role: 'SW Engineer'
};
```

```
loopfunc
禁止内部循环，定义函数的内部循环可能导致这样的错误:
var nums = [];
for (var i = 0; i < 10; i++) {
nums[i] = function (j) {
return i + j;
};
}
nums0; // Prints 12 instead of 2
解决上面的代码,你需要复制的变量 i:
var nums = [];
for (var i = 0; i < 10; i++) {
(function (i) {
nums[i] = function (j) {
return i + j;
};
}(i));
}
```

```
moz
JSHint Mozilla扩展。除非你开发专门为Firefox web浏览器不需要这个选项。
```

```
multistr
将在下个版本中被删除
这个选项会抑制警告多行字符串。允许多行字符串在JavaScript是危险的,如果你小心在一个转义字符()和一个新行之间输入一个空格，将会导致整个字符串错误。
注意,即使这个选项允许正确多行字符串,它仍然警告说对多行字符串没有转义字符之间或与任何转义字符和空格。
// jshint multistr:true
var text = "Hello\World"; // All good.
text = "HelloWorld"; // Warning, no escape character.
text = "Hello\World"; // Warning, there is a space after \
```

```
noyield
检查函数生成器没有yield声明
```

```
plusplus
禁止一元递增和递减运算符的使用
```

```
proto
禁止关于__proto__属性的警告
```

```
scripturl
禁止使用脚本URL定向，比如javascript:...
```

```
sub
下个版本将被删除
检查[]使用，可以使用.代替[]
person['name'] vs.person.name.
```

```
supernew
检查怪异结构 new function () { ... }和 new Object;
这样的结构是有时用于单列在JavaScript中:
var singleton = new function() {
var privateVar;
this.publicMethod = function () {}
this.publicMethod2 = function () {}
};
```

```
validthis
注意:可以使用这个选项只有在函数的范围
在非构造器函数中使用 this
```

```
withstmt
检查with使用声明。
with声明语句可以引起开发者和意外全局变量定义之间的混乱。
```

> 3.环境选项：Environment
> 这些选项让JSHint知道一些预先定义的全局变量。

```
browser
暴露浏览器属性的全局变量，列如 window,document;
注意:这个选项不暴露变量 alert或 console。
```

```
browserify
这个选项定义全局变量使用时可用Browserify工具建立一个项目
```

```
couch
这个选项定义全局暴露CouchDB。CouchDB是一个面向文档的数据库,可以查询和索引MapReduce的方式使用JavaScript
```

```
devel
这个选项定义了全局变量,通常用于日志调试: console, alert等等
```

```
dojo
这个选项定义全局暴露的Dojo Toolkit.
```

```
jasmine
这个选项定义全局暴露jasmine的单元测试框架.
```

```
jquery
这个选项定义全局暴露的jQuery库。
```

```
mocha
这个选项定义全局暴露的“BDD”和“TDD”的ui mocha单元测试框架.
```

```
module
这个选项告诉JSHint,输入代码描述了一个ECMAScript 6模块。所有模块的代码解释为严格模式代码。
```

```
mootools
这个选项定义全局暴露的MooToolsJavaScript框架。
```

```
node
这个选项定义全局变量可以当你的代码运行在node的运行时环境
```

```
nonstandard
这个选项定义非标准但广泛采用全局变量等 escape和 unescape.
```

```
phantom
这个选项定义全局可用你的核心运行时内部PhantomJS运行时环境
```

```
prototypejs
这个选项定义全局暴露的prototypejs框架。
```

```
qunit
这个选项定义全局暴露QUnit单元测试框架
```

```
rhino
这个选项定义全局变量可以当你的代码运行在rhino的运行时环境。rhino是一个开源的实现完全用Java编写的JavaScript。
```

```
shelljs
这个选项定义全局暴露ShellJS库
```

```
typed
这个选项定义全局变量数组类型构造函数。
```

```
worker
这个选项定义全局变量可以当你的代码运行在web worker.web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能.
所有主流浏览器均支持 web worker，除了 Internet Explorer。
```
```
wsh
这个选项定义全局变量可以当你的代码运行在Windows Script Host的运行时环境
```

```
yui
这个选项定义全局暴露的yui框架。
```


