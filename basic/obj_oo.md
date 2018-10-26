# JS面向对象

    内容简介：
    1，关于面向对象
    2，关于面向物理模型
    3，示例
    4，总结


**1，关于面向对象**

javascript中的面向对象是一个老生常谈的问题，可能有人问你的话你也能霹雳啪啦的说一通，比如最常见的，

对象的三要素：对象的名字、对象的属性、对象的方法

    //例子：
    function obj(){    //对象名： obj
    this.desc=“示例”      //对象属性 desc
    this.getDesc=function(){   //对象方法 getDesc
    return this.desc;
    }
    }

或者稍微高级一点：对象的封装、对象的继承，对象的实例化


    这里内容太多，略过，可以自己去查资料，
    留个坑，回头自己写一篇文章填上 -_-|||,毕竟说太多就跑题了
    填坑一：
[继承](https://github.com/zonerscode/JDoc/blob/master/basic/obj_inherit.md)

还有一点，就是尽量用面向对象的思维去解决问题

    //例子-错误的写法：
    if(a){}
    else if(b){}
    else if(c){}
    else{}

    //例子-面向对象的写法：
    let obj = {
        a:function(){},
        b:function(){},
        c:function(){},
        d:function(){}
    }
    //item = a || b || c || d ...
    let result = obj[item]();

    //错误的写法
    function(a,b,c,d,e){}

    //正确的示范
    let param = {a:"a",b:"b",c:"c"...}
    function(param){}

    ...


其实以上都不是我要说的，这里我更偏向于把对象看作一件现实当中的“事物”，即物理上存在的东西，然后把它抽象出来，就是我们需要的东西

**2，关于面向物理模型**

面向物理模型这个说法我不知道有没有人说过，反正我是这么理解的，就这么说吧，

简单点的物理模型


    //例如
    电灯对象：{
    名字：电灯，
    方法1：开,
    方法2：关,
    配置：充电 || 换电池 ？
    }
    //备注：当然可能还有其它的，我这里只挑主要的说

复杂点的物理模型


    //例如
    滑动的滑块：{
    名字：滑块A，
    初始速度：v，
    加速度：a，
    地面摩擦力：f，
    加速度持续时间：t，
    可选 ：{
    质量：m，
    半径：r
    },
    计算：{
    运动距离：s，
    运动时间：T，
    .......
    }
    }

//备注：我不是来帮你们复习物理题的哈，这确实是一个模型，当你写一些动画效果时应该算是常用的物理模型

混合物理模型

    其实说了那么多，然而我们用到的时候，基本上都是两种模式的混合，
    所以在实际抽象模型（数学建模？）的时候，分块拆分是很好的选择

**3，示例**

    我知道，只谈理论不写代码都是耍流氓，虽然我很擅长.......不耍流氓，所以，这里就用代码来说话

比如我这里要写一个多功能选择器的插件，类似IOS的日历选择器，只是不仅仅是支持日历，可以自定义内容,
基于简单物理模型------静态-------数据，样式，配置参数

    var picker=function(options){
         this._modelData= options.modelData || {}; //填充数据
         this._lineHeight=options.lineHeight || 40; //行高
         this._character=options.character || “-”;  //间隔符号
         this._showLines=options.showLines || 3；  //显示行数,必须为奇数
         this.getSelectOpti   //获取选中的选项信息
           //do sth
         }
         this.renderHtml=function(){}  //渲染插件
    }
    picker.prototype.init=funtion(){}
    // .........
    //备注：简要代码，方面理清思路

基于复杂物理模型------动态------动作，改变，计算

    .....{
        this._lineHeight = options.lineHeight || 48;//px *此处lineHeight需要在样式中设置！
        this._moveDistance = options.moveDistance || 1;//每次滚动的单位 px ，加快滚动速度，与回弹速度
        this._moveDouble = options.moveDouble || 2;// 惯性系数 数字越大 拖动后滚动的距离越远
        /*this._dragSpeed = options.dragSpeed || 1; //惯性系数*/
        this._moveRate = options.moveRate || 500;// 1~1000 移动频率 数字越大，频率越高
        this._character = options.character || null;//间隔符号
        this._showLines = options.showLines || 3;//默认显示行数
        this._fza = options.fza || 0.02; //阻力系数 单位时间内速度减小的值
        this._resistance = options.resistance || 0.10;// 当滚动超出边界时受到阻力
    }
    //........
    picker.prototype.scrollToIndex=function(){} //滑动到第N个
    picker.prototype.slideY=function(){} //滑动动画  包括匀速运动，匀减速运动等
    picker.prototype.autoFitIndex=function(){} //自动贴合
    picker.prototype.updatePicker=function(){} //更新数据
    picker.prototype.scrollPrev=function(){}
    picker.prototype.scrollNext=function(){}
    picker.prototype.stopCallBack=function(){}
    //..........

完整代码 :
[Github](https://github.com/OoSpace/JDoc/blob/master/src/picker.html)

**4，总结：**

    其实这玩意说白了就是一个插件，一个地址，一个demo的事情，
    可是我却能写这么多，由此可见吹牛逼（理论知识和抽象能力）的重要性。




