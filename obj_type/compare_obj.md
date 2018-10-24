# JavaScript中的对象以及比较和判断

#### 1. 对象的定义
JS中的所有事物都是对象，对象是指带有**属性**和**方法**的特殊数据类型。

JS自带很多内部对象：

`String` `Date` `Array` 等

对象的创建，属性及方法的使用方式

```
//例如：

var a; //创建空对象

var stu = {}; //创建没有自定义属性和方法的空对象

var obj = new Object(); //同上

var func = (function(){ //构造函数式创建
    var v = 0;//私有属性
    var b = function(){};//私有方法

    return {

    }
})();

var user = {
    name:"小明",
    age:"18",
    run:function(){
    }
};//创建一个有自义属性和方法的空对象


user.name //小明
user['name'] //小明
user['school'] = '清华'// 赋值
user.school = '清华'// 同上

user.run();//调用

user.prototype.stop = function(){}//添加新的方法
user.stop();//调用
```
#### 2. 空对象的判断
如果只是判断对象为`null`或者`undefined`

```
var obj;
if(!obj){
    console.log("对象为空");
}
```
如果是判断对象没有任何`可枚举`属性

```
JSON.stringify(obj)=='{}';//大部分情况下也都可以用
for...in能够遍历可枚举属性，包括prototype中的（继承来的）
Object.keys(ES2015)值遍历·自有的·可枚举属性

注意：不要用JSON.parse(str)=={}来判断，永远都是false，
因为对象的值是引用类型的，引用地址不同就不相等
```
但是对象的属性也可以通过设置`enumerable=false`为不可枚举的，那么通过上面的方法你就无法判断对象是否具有某个属性了


#### 3. 对象的相等判定

一般比较相等都是比较`不为空`的两个对象的相等

```
{}=={}; //false 对象是引用类型的，所以引用地址不同就不同
```

所以一般我们比较两个对象是否`‘相等’` 都是比较它们是否具有相同的属性和方法，以及它们对应的值是否相等,而不是通过‘==’来比较。

#### 4. 对象属性的顺序

```
顺序和你的添加顺序无关，
ES6的 Map()支持有序的对象，
不同的浏览器的排序规则也不同，
因此想跨浏览器的话最好使用数组排序
```
