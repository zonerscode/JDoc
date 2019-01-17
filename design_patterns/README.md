#  常用的JavaScript设计模式

### 1，委托模式

```
通过将多个对象的统一格式请求委托给同一个对象来减少事件处理或者内存开销
```
示例代码：

```
/*一般方式*/
<ul>
<li onClick="change"></li>
<li onClick="change"></li>
<li onClick="change"></li>
<li onClick="change"></li>
</ul>

let change = function(){
    //do sth here
}

/*委托方式*/
<ul onClick="change">
<li></li>
<li></li>
<li></li>
<li></li>
</ul>

let change = function(event){
    //根据event判断如果是LI标签，则统一触发事件
    //do sth here
}
```
> 备注：委托不仅可以节省内存开销，也使动态的插入或者移除HTML元素时，无需重新绑定事件

### 2，观察者模式

```
通过定义一种对象和观察者之间的依赖关系，解决对象和观察者之间的强耦合
```

### 3，工厂模式

```
通过分类抽象出对象工厂，然后方便的生产出各种标准一致的‘产品’
```
示例代码：

```
//对象工厂
let person = {
    age:"",
    sex:"",
    name:"",
    income:"",
    address:"",
    idCard:""
}
/*工厂方法*/
let createStudent = function(options){
    return Object.assign(person,options)
}

/*生产学生*/
let studentA = createStudent({
    grade:"大四",
    schoolName:"中国科技大学"
})
```


```
//组装工厂
let jsonToQueryString = function(json){
        return '?' +
            Object.keys(json).map(function (key) {
                return encodeURIComponent(key) + '=' +
                    encodeURIComponent(json[key]);
            }).join('&');
}

let getStr = jsonToQueryString({
    a:"1",
    b:"2",
    c:{
        c1:"",
        c2:""
    }
})

//拆卸工厂等：略
```

```
备注：该模式可以节省重复劳动，节省代码量，使代码美观易读易维护，
并让各部分的逻辑参数等符合同样的标准，避免人工手写复制粘贴失误等
```

### 4，享元模式

```
通过共享细粒度的数据而节省内存和开销
```
### 5，单例模式


```
//单例模式
let global = {};
let singleModel = function(obj){
    //do sth
    global = Object.assign(obj,global);
    return global
}

new singleModel({
    doSthA:function(){console.log("a")},
    doSthB:function(){console.log("b")}
});
    
new singleModel({
    doSthB:function(){console.log("b1")},
    doSthC:function(){console.log("c")}
})
//使用
global....
```

```
是指只允许实例化一次的对象类，避免方法和命名冲突等
```

### 6，链式调用

```
链式模式的核心思想就是在调用完对象的方法以后可以回当前对象（this）,然后继续调用下去
```

```
//示例代码：
let jQuery = {
    foundId:function(){console.log(1);return this},
    addArr:function(){console.log(2);return this},
    delArr:function(){console.log(3);return this},
}
//执行
jQuery.foundId().addArr().delArr()
```

```
备注：这只是一种最简单的调用方式，仅供参考，举一反三
```


### 7，策略模式

```
策略模式的 目的是使算法脱离于模块而独立管理，解除代码之间的耦合影响
```

### 8，状态模式

```
解决程序中繁杂的分支判断语句问题，避免大量多层的if else 嵌套
```
//示例代码：

```
//一般写法：
if(a){}
else if(b){}
else if(c){}
else if(d){}
```

```
//状态管理例子
let obj = {
    a:function(){
    
    },
    b:function(){
    
    }
    //...
}

//使用
let type = a || b || c || d;
obj[type]();

obj[a]();
```

```
状态管理模式可以较方便的解除各状态之间的耦合，
使本来只能从上到下的上下文执行方式，
变成可以分为多个分支的执行方式，而且更方便复用。
```


### 9，桥接模式

```
通过将实现层（如绑定的事件）与抽象层（如页面UI逻辑）解除耦合，使两部分可以独立
```
### 10，模版模式（某些框架的组件）

```
通过定义一套操作算法骨架，使得子类可以不改变父类的算法结构的同时，重新定义算法中的某些实现步骤
```

### 11，适配器模式

```
将一个类（对象）的接口（方法或属性）转化为另外一个接口或对象，用来避免过多的硬编码和兼容
```
### 12，节流模式

```
通过对重复执行的的业务逻辑进行控制，在执行完最后一次符合某条件的操作后，取消操作，并清理内存
```

```
//示例代码：
let timer= 0;
let _st = setInterval(function(){
    //do sth repeated
    let pass = checkPass();
    if(timer>=1000 || pass){
        clearInterval(_st)
    }
},1000);

let checkPass = function(){
    //TODO sth
    return true || false
};

```

```
应该是最简单的节流模式了orz
```

### 13，惰性模式

```
减少每次代码执行时的重复性的分支判断，通过对对象重新定义来屏蔽原对象中的分支判断。
即如果代码已经走过第一个分支逻辑，那么接下来，就没必要再让代码去执行各个分支的判断，
直接执行第一个逻辑即可
```

```
//示例代码：
let AddEvent = function(dom, type, fn){
  if(dom.addEventListener){
    AddEvent = function(dom, type, fn){
        dom.addEventListener(type, fn, false);
      }
  }else if(dom.attachEvent){
    AddEvent = function(dom, type, fn){
        dom.attachEvent('on'+type, fn);
      }
  }else{
    AddEvent = function(dom, type, fn){
        dom['on'+type] = fn;
      }
  }
 AddEvent(dom, type, fn);
};

```


