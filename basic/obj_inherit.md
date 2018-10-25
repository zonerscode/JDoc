# JS继承

> js中的继承有多少种方式？去某度搜一下，说几种的都有，
看的头晕眼花，还是云里雾里，于是就自己认真理一下，写一篇按照自己的理解来进行的分类。

**JS实现继承的核心技术点无非几种：**

     1: new 关键字
     2: prototype
     3: call、apply
     4: Object.create() ES5
     5: Object.assign() ES6
     6: 拷贝(深拷贝、浅拷贝)
> 网上有说4,5,6种的，大多是组合使用然后根据具体使用情况分类， 也有阮一峰老师按照构造函数、非构造函数的分类(这个好理解些)，
> 这些都各有各的道理，但是都是他们的分类，不是我自己理解的分类， 所以即使这次看懂了，下次难免会忘记，因此自己总结一下。

**1，构造函数式继承，new**

    var func=function(name){
    this.name=name
    };
    var b=new func("b");
    var c=new func("c");
    b.name;//b
    c.name;//c

**2，原型链式继承，prototype**

    var func=function(des){
    this.des=des;
    };
    func.prototype.color="red";
    var b=function(){
    this.color=function(){
    return "green"
    }
    return "orange"
    };
    b.prototype=func.prototype;//私有的des无法继承
    b()//orange
    new b().color()// green
    new b().color;// function(){return "green"} 私有覆盖公有


**3，call、apply**


    /*父*/
    function Parent(add,net,no,teacher) {
     this.add = add;
     this.net = net;
     this.no = no;
     this.teacher = teacher
    }
    /*子*/
    function Child(name,age,sex,id) {
     this.name = name;
     this.sex = sex;
     this.age = age;
     this.id = id;
     Parent.call(this,"添加","www.google.com","1024","copy");
     //这个时候的Parent中的this已经被Child所代替
    }
    var child = new Child("都变了","18","男","2333");
    child.add //添加



    function Parent(add,net,no,teacher) {
     this.add = add;
     this.net = net;
     this.no = no;
     this.teacher = teacher
    }
    /*子类*/
    function Child(name,age,sex,id) {
     this.name = name;
     this.sex = sex;
     this.age = age;
     this.id = id;
     Parent.apply(this,["添加","www.google.com","1024","copy"]);
     //这个时候的Parent中的this已经被Child所代替
    }
    var child = new Child("都变了","18","男","2333");
    child.add //添加

**4，Object.create() ES5支持**


    var func=function(des){
    this.des=des || "empty"
    };
    func.prototype.getDes=function(){
     return this.des
    }

    var b=function(){}
    b.prototype=Object.create(new func("哈哈哈"));
    //此处new func("哈哈哈") 用JSON对象替代可能会比较好理解，不过不修改也是有原因的
    new b("Dobie").getDes()// 哈哈哈


**5: Object.assign() ES6支持**


    var func=function(des){
    this.des=des || "empty"
    };
    func.prototype.getDes=function(){
     return this.des
    }

    var b=function(){}
    b.prototype=Object.assign(new func("哈哈哈"));
    //此处new func("哈哈哈") 用JSON对象替代可能会比较好理解
    new b("Dobie").getDes()// 哈哈哈

**6: 拷贝(深拷贝、浅拷贝)**


    这个去某度搜一下就可以，暂时留坑，原理如标题名，就是循环复制一份出来，
    区别是浅拷贝只拷贝引用（推荐了解 javascript 堆和栈，又是一个坑），
    修改时会影响到父类，深拷贝则是完全单独开辟新的存储地址，不会互相影响







