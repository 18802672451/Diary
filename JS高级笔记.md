# JS高级笔记

## JS高级第一天

### 1-面向对象介绍

```c
面向对象 : 面向对象是一种解决问题的思维方式
面向对象 : 注重的是结果
面向过程 : 注重的是过程
面向对象本质 : 面向过程的封装
(1)以前思维方式：面向过程    ->   注重的是过程
(2)面向对象思维方式  ->  注重的是结果
```

### 2-面向对象编程

```c
// 面向过程 : 注重的是过程
// 弊端 : (1)代码冗余 (2)不便于维护

// 使用函数封装
// 好处: 解决代码冗余
//弊端： 全局变量污染  （全局变量重复设置导致覆盖现象）

//使用对象方法
//封装 ： 将代码放入对象的方法中  （1）解决代码冗余  (2)解决全局变量污染

了解面向对象的原理: 对面向过程的封装
实际开发中,遇到功能先在网上找有没有现成的对象,如果有就直接CV,没有自己写
用别人写好的对象: (1) 好处: 效率高  (2)坏处: 不好维护
自己写好的对象: (1) 坏处: 效率低  (2)好处: 便于维护
```

### 3-原型

```c
// 对象创建原理(new关键字工作原理)
// 1. 创建对象
// 2. this指向这个对象
// 3. 知名对象的赋值
// 4. 自动返回这个对象
```

```c
// 原型: 每一个构造函数创建的时候，系统会自动创建一个对象，称之为原型对象。
// 原型作用：解决 (1)内存资源浪费  + (2)全局变量污染
// 原型语法 ： 两种对象可以访问
        a. 构造函数.prototype
        b. 实例对象直接访问
```

![1596424804820](C:/Users/86188/AppData/Roaming/Typora/typora-user-images/1596424804820.png)

```c
1-构造函数方法的弊端:
 内存资源浪费: 每调用一次构造函数,就会在内存声明一个函数。导致内存资源浪费
2-.使用全局函数解决 ： 内存资源浪费 
  弊端----全局变量污染
3-使用对象 封装 : 把代码放到对象方法中
	同时解决 内存资源浪费 + 全局变量污染
	弊端: 治标不治本. 使用对象后,只能减少全局变量的数量,而且obj本身还是全局的
// 4-原型对象 : 完美解决构造函数  内存资源浪费 + 全局变量污染
	//(1)原型 : 每一个函数在被创建的时候,系统自动创建一个与之对应的对象,称为原型对象
//	(2)作用 : 内存资源浪费 + 全局变量污染
// 	(3)语法 : 如何访问(取值+赋值)原型
	// 	a. 构造函数.prototype
		//b. 实例对象直接访问原型的成员
```

![1596425169233](C:/Users/86188/AppData/Roaming/Typora/typora-user-images/1596425169233.png)

```c
//a. __proto__ : 属于实例对象，指向原型对象
//b. __proto__作用： 可以让实例对象 访问原型中的成员
//c. 注意点：
      // 开发中： 不要写__proto__,直接省略。 因为__proto__不是W3C标准属性
      // 学习中： 可以使用，可以帮助我们更好的理解原型
```

### 4-constructor属性

```c
// .prototype : 属于构造函数，指向原型对象
//            * 作用： 解决内存资源浪费 + 全局变量污染
// .__proto__: 属性实例对象，指向原型对象
//            * 作用： 可以让实例对象访问原型中的成员
// constructor : 属于原型对象,指向构造函数
//            * 作用： 可以让实例对象 知道自己是被哪一个构造函数创建
```

![1588083693450](01-jS高级第一天/01-JS高级课程笔记/day01.assets/1588083693450.png)

### 5-总结

```php+HTML
 1. 哪些成员应该放入原型？
       * 所有实例对象共有的成员
2. 实例对象访问原型的规则？
       * 就近原则： 如果一个实例对象自己有成员，优先访问自己的。自己没有就访问原型的。
3、原型可以重新赋值。
        * 实例对象访问 修改前的原型还是修改后的原型？ 取决于这个实例对象是在修改前还是修改后背创建
                * 修改前创建： 访问修改前的
                * 修改后创建： 访问修改后的
```

## JS高级第二天

### 1-面向对象三大特征介绍

```c
面向对象是一种(解决问题)思维方式
面向对象的思维方式有三大特征
	//a. 封装 : 将代码放入对象的方法中
	//b. 继承 : 一个对象拥有另一个对象所有的成员(属性+方法)
		//(1) 自己实现继承的三种方式
		//(2) js通过原型链来实现继承的
	//c. 多态 : 一个对象在不同情况下的多种状态
```

### 2-继承的三种实现方式

``` c
// 1. 继承 : 一个对象(子对象)拥有另一个对象(父对象)所有的成员
// 2. 三种实现继承的方式
	(1) 混入式继承 : 遍历父对象的成员,添加给子对象
		特点 : 每继承一次,需要遍历一次父元素
		应用场景 :使用与单个对象继承
	(2) 替换原型 : 将父对象 作为子对象构造函数的原型
		特点 : 可能会覆盖子对象构造函数 原本的原型
		应用场景 : 用于多对象继承
	(3) 混合式 :混入式 + 替换原型
	     方案 : 遍历父对象,添加给子对象构造函数的原型
```

### 3-原型链

```c
//js是通过原型链来实现继承
	//1.原型链: 每一个对象都有__proto__属性指向自己的原型,而原型又是一个对象,也有自己的__proto__属性指向原型的原型,以此类推形成一种链式结构,称之为原型链
	//2.对象访问原型链中成员的规则: 就近原则
		//对象访问成员的时候,优先访问自己的.自己没有就反问原型的,如果原型也没有,那就找原型的原型,以此类推直到终点Null.如果还找不到,则是程序报错,提示'xxx' is not a function
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
    	//1.构造函数
        function Person(name,age){
            this.name = name;
            this.age = age;
        };

        //2.原型对象
        Person.prototype.sayHi = function(){
            console.log('人生若只如初见，何事秋风悲画扇');
        };

        Person.prototype.type = '哺乳动物';

        //3.实例化对象
        let p1 = new Person('又又',18);
        console.log(p1);

        //请说出以下代码执行结果
        console.log(p1.name);//又又      p1自己有name属性
        console.log(p1.type);//哺乳动物   p1自己没有type，但是p1的原型有
        console.log(p1.hobby);//undefined p1自己没有hobby，原型也没有
        p1.sayHi();// 人生若只如初见，何事秋风悲画扇   p1自己没有这个方法，原型有
       // p1.eat();//报错 xxx is not defined    p1自己没有这个方法，原型也没有

       //为什么不报错？  p1自己没有这个方法，原型也没有这个方法，但是原型的原型有
        p1.toString();

        //查看p1的原型链
        console.log(p1.__proto__.constructor);//Person
        console.log(p1.__proto__ === Person.prototype);//true

        //查看p1的原型的原型
        console.log(p1.__proto__.__proto__.constructor);//Object
        console.log(p1.__proto__.__proto__ === Object.prototype);//true

        //查看p1的原型的原型的原型
        console.log(p1.__proto__.__proto__.__proto__);//null

    </script>
</body>
</html>
```

![1596510621569](C:/Users/86188/AppData/Roaming/Typora/typora-user-images/1596510621569.png)

### 4-内置对象的原型链

```js
//基本包装类型:  new String()   new Boolean()  new Number()
这个三个对象里封装一些处理基本数据类型的方法
var : 老版本的声明变量关键字
let : 最新版js声明变量关键字,两者区别不大,但是开发主流一般会使用left
// ECMAScript内置对象
	1. date日期对象原型链
	2. array数组对象原型链
	3. string对象的原型链
//DOM对象的原型链
```

#### 4-1date日期对象原型链

![date原型链代码](实践/JS高级.day2/imgs/date原型链代码.png)

![date日期对象原型链](实践/JS高级.day2/imgs/date日期对象原型链.png)

#### 4-2 array数组对象原型链

![arr原型链代码](实践/JS高级.day2/imgs/arr原型链代码.png)

![arr数组对象原型链](实践/JS高级.day2/imgs/arr数组对象原型链.png)

#### 4-3String对象的原型链

![String原型链](实践/JS高级.day2/imgs/String原型链.png)

#### ![String字符串对象的原型链](实践/JS高级.day2/imgs/String字符串对象的原型链.png)

#### 4-4DOM对象的原型链

```js
let box = document.querySelector('#box');
let p1 = document.querySelector('#p1');
```

![DOM](JS高级.day2/imgs/DOM.png)

### 5-函数也是对象

```html
<html>
<body>
<script>
//函数属于对象.
	//对象有点语法操作属性,如果函数也可以使用点语法来操作属性,说明函数也是对象
	//1.原型
		//构造函数prototype : 指向原型
		//原型对象constructor : 指向构造函数
		//实例对象__proto__ : 指向原型
	//2.js中所有的对象都是构造结构函数创建
		//原型对象 : 都是被Object构造函数创建
		//函数对象 : 都是被Function构造函数
		//实例对象 : 由对应的结构函数创建(自定义构造函数Person,SonWang创建的实例对象,由对应的构造函数创建)
    
    /* 所有函数的声明，底层原理都是调用  new Function()
        a. 前面所有的参数都是形参  b. 最后一个函数是函数体代码
        */
        //声明无参无返回函数
        let fn1 =  new Function('console.log("老铁666")');
        fn1();

        //声明有参有返回函数
        let fn2 = new Function('a','b','return a + b');
        console.log(  fn2(10,20) );//30
    
    //1. js基础 : 函数声明有两种语法
    //(1)函数声明 : function 函数名(){//函数体代码}
    // 具名函数 : 声明的时候有函数名
    function fun1(a,b){
        console.log('1111');
        return a+b;
    };
    
    //(2)表达式声明 : let 函数名 = 匿名函数
    //匿名函数: 声明的时候没有函数名
    let fn2 =  function(){
        consloe.log('2222');
    };
    
    //2. js基础: 函数调用也有两种语法
    //2.1 函数调用: 函数名();
    fu1(10,20);
    fn2();
    
    //2.2自调用语法: (函数)();
    (function(){console.log(666)})();  //常用于匿名函数自调用
    (function fn3()){
     console.log(8888)
     })(); //任何函数都可以使用这种自调用语法,只是一般具名函数不会这样写
</script>
</body>
</html>
```

![函数也是对象](02-js高级第二天/01-教学资源/函数也是对象.png)

### 6-instanceof运算符原理结束

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
        /* 
        1. 原型 : 函数对象、原型对象、实例对象三者之间的关系
            构造函数prototype : 指向原型
            原型对象constructor : 指向构造函数
            实例对象__proto__ : 指向原型
        2. js中所有的对象都是构造函数创建
            原型对象 ： 都是被Object构造函数创建
            函数对象 ： 都是被Function构造函数
            实例对象 ： 由对应的构造函数创建 (自定义构造函数Person,SonWang创建的实例对象，由对应的构造函数创建)
        3. instanceof运算符 ： 检测一个构造函数prototype 在不在对象的原型链中。
            语法：  实例对象  instanceof 构造函数
            规则： 检测 右边构造函数的prototype 在不在左边对象的原型链中
                true: 在  false:不在
        */     
        
        let arr = [10,20,30];
        /* 
        arr实例对象原型链  arr.__proto__  ->  Array.prototype -> Object.prototype - > null
        */
        console.log( arr instanceof Array);//true
        console.log( arr instanceof Object);//true

        /* 
        根据instanceof运算符规则： 左边object是一个对象，  右边object是一个函数
        object对象原型链 object.__proto__ -> Function.prototype ->Object.prototype ->null
        
        */
       console.log( Object.__proto__.constructor );//Function
       console.log( Object.__proto__ === Function.prototype );//true
    
        console.log( Object instanceof Object);//true
        console.log( Object instanceof Function);//true


        /* 
        根据instanceof运算符规则： 左边Functiont是一个对象，  右边Function是一个函数
        function对象原型链 Function.__proto__ -> Fuction.prototype -> Object.prototype -> null
        */
        console.log( Function.__proto__.constructor );//Function
        console.log( Function.__proto__ === Function.prototype );//true

        console.log( Function instanceof Function);//true
        console.log( Function instanceof Object);//true
    </script>
</body>
</html>
```

![1596532646904](C:/Users/86188/AppData/Roaming/Typora/typora-user-images/1596532646904.png)

### 7-静态成员与实例成员

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
    	/*
    	静态成员: 属于函数对象自己的成员
    	实例成员: 属于实例对象的成员
    	*/
        function.Person(name,age){
            //构造函数里面的成员属于实例成员
            this.name = name;
            this.age = age;
        }
        //静态成员: 函数自己的成员
        Person.hobby = '保养对象';
        let p1 = new Person('ikun',30);
        console.log(p1.name);//实例成员: 属于实例对象
        console.log(p1.age);//实例成员: 属于实例对象
        
        //console.log(p1.hobby);//undefined 静态成员只有函数自己才可以访问
        console.log(Person.hobby);//保养健康
        
        /* 静态成员经典场景: 只执行一次函数 
        */
        function fn(){
            if(!fn.flag){
                console.log('投票了');
                fn.flag = true;
            };
        };
        fn();//有效
        fn();//无效
        fn();//无效
        fn();//无效
        fn();//无效
        
        //let bol = true;
        //if(bol){
        //    console.log(1);
        //}else{
        //    console.log(2);
        //};
        
        /*
        if(条件 true/false){
        	条件成立需要执行的代码
        }else{
        	条件不成立需要执行的代码
        }
        
        注意点: if小括号里面的条件可以写三种代码
        关系表达式: 结果是布尔类型
        布尔类型的值
        其他的值: 编译器会自动转成为布尔类型判断是否成立
        */
    </script>
</body>
</html>
```

## JS高级第三天

### 1-函数三种调用模式(this指向)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        /* 
        1. 函数三种执行方式: 普通函数  对象方法   构造函数
        2. this指向 : 谁调用,就指向谁
            this的指向取决于调用方式,与声明无关
                a. 普通函数 :  this指向window
                b. 对象方法 :  this指向对象
                c. 构造函数 :  指向new创建的对象
         */

        function fn (){
            console.log('1111');
            console.log(this);
        }

        //  1 普通函数
        fn(); // window.fn();

        //  2 对象的方法
        let obj = {
            name: 'ikun',
            age:30,
            eat:fn
        };

        // 由于eat的值就是fn的值,所以调用eat就是调用的fn
        //  3 构造函数 
        let p1 = new fn();//this 指向new创建的对象
        console.log(p1);
    </script>
</body>
</html>
```

### 02-函数上下文执行模式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
  /* 函数4中调用方式 
        
        1. 函数三种执行方式 : 普通函数  对象方法 构造函数
            共同点 : this的指向无法修改  是固定的 (一旦修改程序报错)
            普通函数 : this指向window
            对象方法 : this指向对象 
            构造函数 : this指向new创建的对象

        2. 函数第四种执行方式 : 上下文模式
            作用 : 修改函数里面的this
            语法 : 三个语法作用一直都是修改this, 只是传参方式不同
                2.1 函数名.call(修改后的this,形参1,形参2)
                    应用场景 : 适用于函数形参 <= 1
                2.2 函数名.apply(修改后的this,数组或伪数组)
                    应用场景 : 适用于函数形参 >= 2
                2.3 函数名.bind(修改后的this,形参1,形参2)
                    注意点 : 
                        a. bind()不会立即执行,这个函数,而是返回一个修改this之后的新函数
                        b. 一般用bind调用不会立即传递形参(一旦传递,形参就固定了无法修改),而是调用返回						的新函数的时候再传参
                    应用场景 : 适用于某个函数不需要立即执行,而是过一会儿才执行
                        事件处理函数 + 定时器函数
         */
         function fn (a,b){
             console.log(this);
             console.log(a+b);

             return a+b;
         }
         fn();
        //  2.1 函数名.call(修改后的this,形参1,形参2)
        fn.call({name:'张三'},100,101);

        // 2.2 函数名.apply(修改后的this,数组或伪数组)
                //  应用场景 : 适用于函数形参 >= 2
        fn.apply({name:'李四'},[10,20]);
        
        // 2.3 函数名.bind(修改后的this,形参1,形参2)
        //             注意点 : 
        //                 a. bind()不会立即执行,这个函数,而是返回一个修改this之后的新函数
        //                 b. 一般用bind调用不会立即传递形参(一旦传递,形参就固定了无法修改),而是调用							返回的新函数的时候再传参
        //             应用场景 : 适用于某个函数不需要立即执行,而是过一会儿才执行
        //                 事件处理函数 + 定时器函数
        let newFn = fn.bind({name:'王五'});
        newFn(22,33);
    </script>
</body>
</html>
```

### 3-函数上下执行模式注意点

```html
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
     <script>
         /*
         1. 上下文执行默认作用 : 修改函数中的this指向
         2. 注意点 : this只能指向引用类型(array function object). 如果指向基本类型
         	* 基本包装类型string number boolean : 自动转成对应的对象类型 new String() new Number()  				new Boolean()
         	* undefined与null : 修改无效,this指向window
         */
         function fn(){
            console.log(this);
            console.log( typeof this);
        };
        fn.call({name:'1111'});
        fn.call([10,20,30]);
         //如果上下文模式把this修改为基本数据类型
        //基本包装对象会自动转成对应的内置对象
        fn.call('abc');
        fn.call(123);
        fn.call(true);
        //undefined和null : 修改无限，this默认指向window
        fn.call(undefined);//window
        fn.call(null);//window
        fn.call();//window
    </script>
</body>
</html>
```

### 4-伪数组转数组

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
        /* 函数4种调用方式
        1.函数三种执行方式 ： 普通函数、对象方法、构造函数
            * 共同点 ： this的指向无法修改，是固定的.(一旦修改程序报错)
            * 普通函数 ： this指向window
            * 对象方法 ： this指向对象
            * 构造函数 ： this指向new创建的对象
        2.函数第四种执行方式： 上下文模式
            * 作用： 修改函数里面的this
            * 语法： 三个语法作用一致都是修改this，只是传参方式不同
                2.1 函数名.call(修改后的this,形参1,形参2)
                    场景：用于函数原本形参 <= 1
                2.2 函数名.apply(修改后的this,数组或伪数组)
                    场景：用于函数原本形参 >= 2
                2.3 函数名.bind(修改后的this,形参1,形参2)
                    不会立即执行函数体，而是返回一个修改this之后的新函数
                    场景： 用于这个函数不需要立即执行，而是过一会儿执行（事件处理函数，定时器函数）
        */
        //1.伪数组 ： 有数组三要素（下标，元素，长度），但是不能调用数组的API
        //伪数组本质是一个对象 : (属性名恰好就是下标， 但是对象原型不是指向Array.prototype,所以无法调				用数字方法)
        let weiArr = {
            0:20,
            1:30,
            2:60,
            3:80,
            length:4
        };
        console.log(weiArr);
        // console.log(weiArr.reverse());//报错 伪数组无法调用数组方法
        
        //2.伪数组转数组 ： 目的是让伪数组也可以调用数组的方法
        //2.1 遍历伪数组，添加到真数组中
        let arr = [];
        for(let i = 0;i<weiArr.length;i++){
            arr.push( weiArr[i] );
        };
        console.log(arr);
        
         //2.2 arr.push.apply(arr,伪数组)
        //(1)push()方法支持一次性添加多个元素
        //弊端 ： 形参数量太多
        let arr = [];
        arr.push( weiArr[0],weiArr[1],weiArr[2],weiArr[3] );
        console.log(arr);
        
        let arr = [];
        //这里不需要修改this，仅仅只是利用apply可以自动遍历数组|伪数组，来逐一传参的特点
        arr.push.apply(arr,weiArr);
        console.log(arr);
        
         /* 
        2.3 Array.prototype.slice.call(伪数组)
        (1)数组的原型中有一个方法叫做slice 。  它有一个特点，不传参数，默认会返回数组自身
        (2)如果伪数组也可以调用slice,那么就可以返回一个真数组
        (3)但是伪数组不能直接调用slice,会报错。  原因：伪数组自己没有slice，原型也没有slice
        (4)思考：为啥真数组可以调用slice呢？  原因： 数组自己没有slice，但是原型有
        (5)原型中的成员，有两种访问方式
            a. 构造函数自身：  Array.prototype
            b. 每一个实例对象
        (6)越过原型链，直接利用构造函数的prototype来调用slice :  Array.prototype.slice()
        (7)越过原型链虽然可以调用slice，但是此时slice方法中的this就是原型对象 Array.prototype
        (8)既要调用slice，又希望slice方法里面的this指向伪数组
            * 相当于是weiArr来调用slice
        */
        let arr1 =  Array.prototype.slice.call(weiArr);
        console.log(arr1);
    </script>
</body>
</html>
```

### 5-伪数组排序

```html
<html>
    <body>
        <script>
           	 //第一种方式: 先把伪数组转成真数组,然后调用sort
			let arr = Array.prototype.slice.call(weiArr);
            arr.sort(function(a,b){return a-b});
            cnnsole.log(arr);
            // Array.prototype.sort.call(weiArr,function(a,b){return a-b});
            // 思路: 越过原型链查找机制,直接调用数组原型的sort,并且把this修改为伪数组
            Array.prototype.sort.call(weiArr,function(a,b){return a-b});
            console.log(weiArr);
        </script>
    </body>
</html>
```

### 6-求最大值

```html
<html>
    <body>
        <script>
            /* 求数组最大值 */
            let arr = [112,234,,676,5,6343,67];
            // 擂台思想
            // 1.擂台思想
            	let max = -Infinity;//用于存放表示正无穷大的数值
            // 2. 遍历挑战者
            for(let i = 0; i < arr.length;i++){
                // 3.依次和擂主pk
                if(arr[i] > max){
                    max = arr[i]
                };
            };
            console.log(max);
            
            /* Math.max */
            // let max1 = Math.max(arr[0],arr[1],arr[2],arr[3],arr[4]);
            // 利用apply自动遍历数组传参的特点 (底层与上面代码一致,只是apply会自动遍历数组逐一传参)
            let max1 = Math.max.apply(Math,arr);
            console.log(max1);
        </script>
    </body>
</html>
```

### 7-求数组最大值

```html
<html>
    <body>
        <script>
            /* 
            1. 复习 typeof关键字检测数据类型 : typeof 数据
            	* 弊端: 无法检测 null 和 array 这两种数据类型,返回值都是object
            	* typeof null : 'object'
            	* typeof []   : 'object'
            2. 介绍 对象的toString()方法检测数据类型
            	* Object.prototype.toString() : 返回固定格式字符串 [object 数据类型]
            	* Array.prototype.toString() : 返回数组.join ()方法拼接的字符串
            3. 总结: 万能检测数据类型
            	* 固定语法: Object.prototype.toString.call(数据)
            */
            // a. 值类型(基本数据类型)
            let str = '我爱你们';
            let num = 68;
            let bol = true;
            let und = undefined;
            let nul = null;
            // b. 引用类型(复杂数据类型)
            let arr = [12,13,14];
            let fn  = function(){};
            let obj = {name:'link'};
            console.log(typeof str); //'string'
            console.log(typeof num); //'number'
            console.log(typeof bol); //'boolean'
            console.log(typeof und); //'undefined'
            console.log(typeof nul); //'object'
            console.log(typeof arr); //'object'
            console.log(typeof fn);  //'function'
            console.log(typrof obj); //'object'
            
            /* 2. 对象的toString()方法介绍
            Object.prototype.toString() : 返回一个固定格式字符串 '[object 数据类型]'
            Array.protottpe.toString()  : 底层原来是调用数组的join()方法
            */
            console.log(obj.toString()); //[object Object]
            console.log(arr.toString()); //[object Array]
            
            /* 3. 万能检测数据类型 : 越过了原型链,直接调用Object.prototype里面的toString
            	* 因为很多对象的原型都覆盖了toString(),所以通过原型链无法直接访问到Object的原型里面				dtoString
            	* 总结 : Object.prototype.toString.call(数据)
            */
            console.log(Object.prototype.toString.call(str));//[objcet	String]
            console.log(Object.prototype.toString.call(num));//[object	Number]
            console.log(Object.prototype.toString.call(bol));//[object	Boolean]
            console.log(Object.prototype.toString.call(und));//[object Undefined]
            console.log(Object.prototype.toString.call(nul));//[object	Null]
            console.log(Object.prototype.toString.call(arr));//[object	Arrat]
            console.log(Object.prototype.toString.call(fn)); //[object	Function]
            console.log(Object.prototype.toString.call(obj));//[object	Object]
        </script>
    </body>
</html>
```

## JS高级第四天

### 1-递归函数

```html
<html>
    <body>
        <script>
        	/* 
        	1. 递归函数 : 一个函数在函数体中调用自己
        	2. 递归函数作用 : 函数体代码重发执行
        		* 递归函数做到事和循环一样的,能用递归做的就可以用循环做.只是语法简洁性不同.
        	3. 递归注意点 : 一定要有结束条件,否则会导致死循环.
        	*/
            
            // 单函数递归
            function fn(){
                console.log('好好学习');
                fn();
            };
            fn();
            
            // 双函数递归
            
            // 使用递归
            function getSum(n){
                return n == 1 ? 1 : n + getSum(n - 1);
                
                /* if(n == 1){
                    return 1;
                }else{
                    return n + getSum(n - 1);
                }; */
            }
        </script>
    </body>
</html>
```

### 2-递归遍历DOM树

```html
<html>
    <body>
        <script>
        	 /* 需求: 获取某一个父元素所有的后代元素 (变量DOM树)
        1. js原生的DOM语法可以实现吗?  不行
            a. DOM原生语法, 只能获取子代元素:  父元素.chlidren
        2. 思路: 写一个函数,遍历父元素的子元素. 如果子元素也有自己的子元素,ze继续遍历获取子元素的子元素,以此类推形成函数递归调用
         */

        let box = document.querySelector('#box');
        let arr = [];//存储所有的后代元素

        function find(ele){
            for(let i = 0;i < ele.children.length;i++) {
                console.log(ele.children[i]);
                arr.push(ele.children[i]);
                // 继续递归调用: 获取子元素的子元素
                find(ele.children[i]);
            }
        };
        find(document);
        </script>
    </body>
</html>
```

### 3-闭包

#### 1-闭包介绍

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        /*
        1.闭包函数
            1.1 作用:
            1.2 语法:
            1.3 注意点:
         
        2.学习路线 : 需求, 在函数外边访问函数里变量
            2.1 复习函数作用域
            2.2 函数返回值的特点
            2.3 闭包介绍
        */

        /*
        1. js有两种作用域
            1.1 全局作用域(全局变量): 在函数外面声明,可以在页面任何地方访问
                * 全局变量生命周期 : 页面打开时声明 页面关闭时销毁
                * 生命周期: 从变量声明 到 变量销毁
            1.2 局部作用域(局部变量): 在函数里面声明,只能在函数体里面使用
                * 局部变量声明周期 : 执行函数体开始声明, 然后函数调用结束销毁
        */
        // function fn (){
        //     let person = {
        //         name:'jk姐姐',
        //         age:19
        //     };
        // };
        // fn();
        // // 函数外面无法直接获取(访问)函数内部的成员
        // console.log(person);

        /* 2. 如何实现在函数外部访问函数里边的变量
            解决方案 : 使用return
            问题 : 每调用一次,就会生成一个新的对象
         */

        // function fn() {
        //     let person = {
        //         name: 'jk姐姐',
        //         age: 19
        //     };
        //     return;
        // };
        // let p1 = fn();
        // // p1 和 p2 虽然里面的数据相同,但是这是两个不同的对象(地址不同)
        // console.log(p1);

        /* 
        3. 如何实现 在函数外边访问函数里面的变量,并且保证
            解决方案: 使用闭包
            闭包作用: 在函数外面访问函数里面的变量
            闭包语法: 语法不固定,但是分为三个步骤
                (1) 在外部函数中声明一个闭包函数
                (2) 在闭包函数中返回你想访问的变量
                (3) 返回闭包函数
            闭包本质 : 沟通全局作用域与局部作用域的一座桥梁
         */

        function outer(){
            let person = {
                name:'Jk姐姐'
            };
            // (1)在外部函数的里面声明一个内部函数(闭包函数)
            function closure(){
                // (2) 在闭包函数中返回你想要返回的变量
                return person
            };
            // (3)返回这个闭包函数
            return closure; 
        };
        // 调用外边函数  得到闭包函数
        let  bibao = outer();
        // 调用闭包函数,得到局部变量
        let p1 = bibao();
        let p2 = bibao();

        console.log(p1,p2);
        console.log(p1 == p2);//true
    </script>
</body>
</html>
```

![图解闭包](资料/04-JS高级第四天/imgs/图解闭包.png)

#### 2-闭包注意点

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
        /* 闭包
        1.1 作用：在函数外面访问函数内部的变量
        1.2 语法：
            a. 在函数里面声明一个闭包函数
            b. 在闭包函数中访问局部变量
            c. 返回这个闭包函数
        1.3 注意点：
            (1)得到相同的值：外部函数调用一次，闭包函数调用多次
            (2)得到不同的值：外部函数调用多次，闭包函数调用1次
        */   
       
        //外部函数
        function outer(){
            let num = Math.ceil(Math.random()*100);
            //a.在函数里面声明一个闭包函数
            function closure(){
                //b.在闭包函数中访问局部变量
                return num;
            };
            //c.返回这个闭包函数
            return closure;
        };

        //(1)得到是相同的值： 外部函数调用一次，闭包函数调用多次
        //调用外部函数一次，得到闭包函数
        // let bibao = outer();
        // //调用闭包函数多次
        // let n1 = bibao();
        // let n2 = bibao();
        // let n3 = bibao();
        // console.log(n1,n2,n3);

        //(2) 得到不同的值： 外部函数调用多次，闭包函数调用一次
        // let bibao1 = outer();
        // let num1 = bibao1();
        let num1 = outer()();

        // let bibao2 = outer();
        // let num2 = bibao2();
        let num2 = outer()();

        // let bibao3 = outer();
        // let num3 = bibao3();
        let num3 = outer()();

        console.log(num1,num2,num3);
    </script>
</body>
</html>
```

![闭包相同(不同值)图解](资料/04-JS高级第四天/imgs/闭包相同(不同值)图解.png)

#### 3-闭包经典应用场景(沙箱模式)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <script>
       /* 
       1.沙箱模式：值得是一个独立的内存空间（局部作用域）.通常是一个匿名函数自调用
       2.沙箱模式作用：
            a. 避免全局变量污染
            b. 模块化开发 ： 一个功能对应一个沙箱
        3.沙箱注意点 ：不要在沙箱内部访问全局变量，应该使用参数传递
            * （1）沙箱外面的变量，代码可能会压缩出错
            * （2）破坏封装性
       */   
       (function(w){
           let a = {
                eat:function(){
                    console.log('吃饭');
                },
                play:function(){
                    console.log('玩');
                }
           };

           //暴露接口
           w.a = a;
       })(window);
       
   </script>
</body>
</html>
```

### 4-ES6类与继承

#### 1-class关键字

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        /* 
        1. class关键字作用: 声明类函数 (相当于以前的构造函数)
            * class语法作用和以前的构造函数语法一致,只是写法不同
                a. 将构造函数与原型方法 卸载一个大括号中,提高代码阅读性
                b. class类函数必须要使用new来调用,语法更加桂发
        2. 语法: 
                class 构造函数名 {
                    // 构造函数
                    constructor(){

                    };
                    // 原型中的方法
                    eat(){

                    };
                };
         */

        // ES6继承 : class类函数
        class Person {
            //(1) 构造函数: 固定的语法 constructor(){}
            constructor() {
                this.name = 'name';
                this.age = '20';
            }

            //(2) 原型中的方法
            eat() {
                console.log('吃饭');
            };

            learn() {
                console.log('续写');
            }
        };

        /* ES6语法的本质其实还是以前的原型语法,只是写法不同.还是可以用以前的语法给原型添加成员 */
        Person1.prototype.type = '人类';

        //(3) 实例对象
        // class类函数必须要用new调用,否则会报错
        let p2 = new Person1('班长', 19);
        console.log(p2);
    </script>
</body>
</html>
```

#### 2-extends关键字

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        /* 
        1. extends关键字 : 用于继承
        2. 底层原理 : 替换原型
            * Student.prototype.__proto__ = Person.preototype
            * s1.__proto__.__proto__ === Person.prototypr
         */

         /*  父对象 */
         class Person{
            //  构造函数
            constructor(name,age){
                this.name = name;
                this.age = age;
            };

            // 原型方法
            eat(){
                console.log('人要吃饭');
            }
         };
         Person.prototype.type = '人类';
         let p1 = new Person('ikun',30);

         /*  子对象 继承与父对象 
         extends关键字底层原理: Student.prototype.__proto__ = Person.prototype
        */

         class Student extends Person{
            //  构造函数
            // constructor(name,age,score){
            //     this.name = name;
            //     this.age = age;
            //     this.score = score;
            // };
            // 原型方法
            work(){
                console.log('停止斗图');
            };

         }
         let s1 = new Student('班长,20,001');
         console.log(s1);

         console.log(s1.type);//人类
         s1.eat();//吃饭
    </script>
</body>
</html>
```

![ectends关键字图解](资料/04-JS高级第四天/imgs/ectends关键字图解.png)

#### 3-super关键字

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <script>
        /* 
        super关键字 : 在子类函数中调用父类的方法
         */

        class Student extends Person {
            //  构造函数
            constructor(name, age, score) {
                // 在子类结构函数中,去调用父类的构造函数
                /*  细节: 如果重写了子类的构造函数construc, 必须要调用父类的方法super()
                 */
                super(name, age);
                this.score = score;
            };
            // 原型方法
            work() {
                /* 调用父类的方法 */
                //  super.eat()底层原理:  Person.prototype.eat();
                console.log('停止斗图');
            };

        };
        let s1 = new Student('班长', 20, 99);
        console.log(s1);
        s1.work();
    </script>
</body>

</html>
```

## JS第五天

### 1-正则表达式

```html 
<html>
    <body>
    	<script>
        /* 
        1.正则表达式 ：RegExp (regular expression)  是ECMAScript内置对象
        2.作用 ：对 字符串进行逻辑匹配 运算
        3.使用流程 ：
            (1)创建正则对象 :  new RegExp(/正则表达式/);
            (2)test('字符串') ： 对字符串进行逻辑匹配运算
        */

        /* 
        1.正则表达式 ：是一个对 字符串进行逻辑匹配运算 的对象
            a. 正则是内置对象 ： 存储一些属性和方法
            b. 表达式 :  对字符串 进行逻辑匹配 运算
        
        2.使用流程 ：两个步骤
        */

        //(1)调用构造函数，创建正则对象
        let reg =  new RegExp(/a/);

        //(2)调用test方法，对字符串进行运算   true:符合规则   false:不符合
        console.log(  reg.test('abcdefg') );
        console.log(  reg.test('123456') );


        /* 了解： 正则表达式字面量写法  /正则表达式/ */

        console.log(  /a/.test('我爱你') );//false
         </script>
    </body>
</html>
```

![正则表达式](实践/JS高级.day5/imgs/正则表达式.png)

#### 1-2.元字符与原义文本字符

```html
<html>
    <body>
        <script>
        /* 
        一个正则表达式主要由两部分组成
            1.原义文本字符 ： 就是字符本身的含义，千万别想多了
            2.元字符 ： 改变了字符串本身的含义 （相当于js的关键字）
                . \ | [] {} () + ? * $ ^
        */    
		
       
        //1.原义文本字符 ： 就是字符本身的含义，千万别想多了
        /*  /abc/ :  含义，就是检查字符串中有没有abc。 别想多了
                不是说有a或者有b或者有c，也不是说有a 和 b 和 c
        */

        console.log(/abc/.test('a123'));//false
        console.log(/abc/.test('ab123c'));//false
        console.log(/abc/.test('abc123'));//true

        console.log(/黑马/.test('绿裙很黑'));//false
        console.log(/黑马/.test('一匹黑色的马'));//false
        console.log(/黑马/.test('黑马程序员，宇宙最强IT培训'));//true
        </script>
    </body>
</html>
```



### 2-字符类与反向类

```h
// 字符类 : /[abc]/
	// 	/abc/ : 原义文本字符,检测字符串有没有abc
	//	/[abc]/ : 字符类   将a和b和c这三种字符类归为一类,只要满足任何一类即可
		// 字符串里面只要有abc 任意一个字符即可
// 2.反向类 : /[^abc]/ : 将没有a ， 没有b，没有c的字符串归为一类。
	//	字符串里面只要有任意一个不是a 、 b 、 c即可
```

### 3-范围类

```html
1. 范围类 
        /[0-9]/  : 检测是否有数字字符
        /[a-z]/  : 检测是否有小写字母
        /[A-Z]/  : 检测是否有大写字母
2.注意点：
        a. 范围是一个闭区间 ：  /[0-9]/  包含0和9
        b. 范围类可以连接 :  /[0-9a-zA-Z]/ : 检测字符串有没有数字 或者 英文字母
        c. 范围类左边 < 右边 ， 否则正则报错
              /[5-8]/ :正确 检测5-8范围的数字
              /[8-5]/ :错误 报错
```

### 4-预定义类

- ​	预定义类：相当于js的api。 作者提前封装好的直接使用即可![预定义类](实践/JS高级.day5/imgs/预定义类.png)

### 5-边界

-  严格匹配: 	^字符串$
  - 例如:  ^abc$ :  含义是, 字符串必须是以a开头, 中间必须是b, 结尾必须是c
    - 满足该条件的只有一个字符串: abc	

![边界](实践/JS高级.day5/imgs/边界.png)

### 6-量词

![量词](实践/JS高级.day5/imgs/量词.png)

### 7-分组

```javascript
/*1. () 这个元字符有三个含义
		 a.分组：使量词作用于分组
		 	* 量词只能作用于一个字符，如果想作用与多个字符，就要使用分组（将多个字符当成一组）
		   b.提升优先级：通常与元字符 | 一起使用
            c.反向引用
   2. |   或
   		* | 默认作用于两边的所有字符，如果只想作用与指定字符，则可以使用() 来提升优先级
 */

 //1. 需求： 匹配连续出现三次love的字符串

    //1.错误写法:  /love{3}/  , 含义： lov + e{3}
    console.log ( /love{3}/.test ( "lovelovelove" ) );//false
    console.log ( /love{3}/.test ( "loveee" ) );//true
    console.log ( /love{3}/.test ( "loveeeabc" ) );//true
    //2.正确做法：使用分组   /(love){3}/
    console.log ( /(love){3}/.test ( "lovelovelove" ) );//true
    console.log ( /(love){3}/.test ( "loveee" ) );//false

    //2. 需求：匹配 love 或者 live
    //1.错误写法:  /lo|ive/  ,含义：  lo  或者  ive

    console.log ( "I love you".replace ( /lo|ive/, "X" ) );// I Xve you
    console.log ( "I live you".replace ( /lo|ive/, "X" ) );// I lX you

    //2.正确写法： /l(o|i)ve/, 含义：匹配love 或者 live

    console.log ( "I love you".replace ( /l(o|i)ve/, "X" ) );// I X you
    console.log ( "I live you".replace ( /l(o|i)ve/, "X" ) );// I X you
	
	/* 
        3.反向引用 ： 正则表达式会把小括号中匹配到的内容给存起来。存入$1-$9中。 用于反向引用。

        场景 ： 日期格式  大陆日期格式 yyy-mm-dd   香港日期格式：dd-mm-yyyy
        2020-08-15  转换成  15/08/2020
     */
	 console.log( '2020-08-15'.replace(/(\d{4})-(\d{2})-(\d{2})/,'$3/$2/$1') );//15/08/2020

```



### 8-修饰符

```html
 <html>
     <body>
         <script>
         	/* 
         	1. 修饰符: 影响整个正则规则的特殊符号(对正则起修饰作用)
				i: intensity  不区分大小
				g: global   全局匹配
				m: multiple 检测换行符(需要和边界一起使用)
			
			2. 修饰符语法:  /正则表达式/修饰符
         	*/
             // 1. i: intensity  不区分大小
             console.log('AaAAAaaa'.replace(/a/,'X'));//AXAAAaaa  默认情况下正则区分大小写
             console.log( 'AaAAAaaa'.replace(/a/i,'X') );// XaAAAaaa i:不区分大小写
             
             // 2. g: global   全局匹配
             console.log( 'AaAAAaaa'.replace(/a/,'X') );// AXAAAaaa 默认情况下正则只能匹配第一个
        	console.log( 'AaAAAaaa'.replace(/a/g,'X') );// AXAAAXXX g:全局匹配
             
             // 3. m: multiple 检测换行符            
             /* 让边界  能够识别换行符  */
             //每一行的第一个我，改成你字
      		let str = '我爱我学生\n我爱我学生\n我爱我学生';
        	console.log(str);
        	console.log( str.replace(/^我/gm,'你') );
         </script>
     </body>
</html>
```