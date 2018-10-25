# javascript原型和原型链，构造函数和实例

> 原型（构造函数）就是工厂，原型的实例就是工厂按照图纸生成的工具（比如汽车），
> 原型链（隐式的）就是生成的工具所具有的功能，而功能是工具的属性，
> 生成什么样的工具是由工厂（构造函数）决定的，图纸是有工厂和客户共同决定的


    var carFactory =function(options){  //原型,构造函数 （工厂）

    this.name = options.name;  //

    this.color = options.color;

    this.run  = function(){}; //

    this.stop = function(){};

    //......

    }

>
> //下面是原型的实例，注意，不一定要new，carFactory({name:"法拉利",color:"orange"})本身就是一个实例，
> //可以调用对应的属性和方法如run()和stop()等，
> //这里的new是一个继承，相当于另外复制了一份，是为了重复利用该工厂，而不是只生产一辆车，专门为该车提供服务，
> //关于继承，可以参考：[js继承][1]

    var car = new carFactory({name:"法拉利",color:"orange"});//实例

    car //{...}


> //在chrome下，输出一个对象，其中 __proto__即是原型链，是指该对象隐式的含有的一些功能，
> //该功能由原型构造函数决定，而所有的原型的祖宗原型是Object，所以所有的对象都有Object的一些默认的属性和方法，如:toString等

以下代码加深理解


    2..constructor=== Number // 2的构造者是Number
    Number.constructor ===Function//Number 的构造者是Function
    Function.constructor===Function //Function的构造者是 Function
    Math.constructor=== Object// Math的构造者是Object
    ({}).constructor===Object// {}的构造者是Object
    Object.constructor===Function //Object 的构造者是 Function


    2..__proto__=== Number.prototype // 2的构造者是Number
    Number.__proto__===Function.prototype //Number 的构造者是Function
    Function.__proto__===Function.prototype //Function的构造者是 Function
    Math.__proto__=== Object.prototype // Math的构造者是Object
    ({}).__proto__===Object.prototype // {}的构造者是Object
    Object.__proto__===Function.prototype //Object 的构造者是 Function


  [1]: https://segmentfault.com/a/1190000011235133

