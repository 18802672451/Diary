

## webAPI第1天

### 1-文档

```
document:  整个文档
DOM :   操控文档--文档对象模型，操作网页上的元素的API
BOM :   浏览器对象模型--操作浏览器部分功能的API
```

###  2-获得元素

```js
1.通过id名获得元素--documenlementById('id名')--dgi
2.通过标签名获得元素--document.getElementsByTagName('div');--dgt
3.通过类名获得元素--document.getElementsByClassName('');--dgc
4.通过name值来获取元素--document.getElementsByName('');--dgn
5.通过选择器名获得元素
  #box{ } ID选择器--document.querySelecto--doq
  .items{ }类选择器--document.querySelectorAll--doa
```

### 3-点语法设置css属性

```
1.样式---style   样式属性值---字符串
2.如果css属性名带有 -- , 应该去掉,然后首字母大写
3.js设置css属性连写 -- divBox.style.border = '5px solid blue';
```

### 4-事件

```
1.三要素 
事件源--谁来做--拿到的是数组,所以要加下标--直接拿到元素
事件类型--怎么做--当元素被点击的时候,执行函数--onclick
事件类型--做什么
2.给页面元素设置事件
  鼠标单击 onclick
  鼠标移入 onmouseover
  鼠标移出 onmouseout
  成为焦点 onfocus
  失去焦点 onblur
  表单输入 oninput
```

### 5-获取标签内容

```
1.innerText--获得标签内部文本,但是隐藏的元素无法获取
2.innerHTML--获取标签内所有的内容(文本,标签,属性,隐藏的内容)
3.textContent--获得标签内的文本内容,包括隐藏的元素--低版本浏览器不兼容(上古IE)
```

### 6-阻止a标签跳转

```html
<a href="#你来动我啊">百度</a>
<a href="JavaScript:">京东</a>
<a href="JavaScript:void(0)">京东</a>
<a href="JavaScript:null">京东</a>
<a href="JavaScript:undefined">京东</a>
<a href="#" onclick="return false">淘宝</a>
```

```
有多种方式可以a标签的跳转阻止，第一种不建议，其他的看你喜欢
```

## webAPI第2天

### 1-内置系统属性

```js
获取
1.点语法
	内置属性获取
	console.log(box.mm)
2.中括号 +key的方式
3.geAttribute(  )
	内置或者自定义属性都可以获取
	console.log(box.getAttribute( ' id ' )  )
设置(添加)
1. 点语法
	divBox.mm = '秀儿'
	可以设置,但是不会再行内显示
2. 利用中括号
	divBox['mm'] = '秀儿'
	可以设置,不在行内显示
3. setAttribute
	divBox.setAttribute( ' mm '   ,   '  pipi  ' )
	可以设置,还在行内结构显示
删除
1. 点语法
	 divBox.mm =  '  ' 
	只能删除属性值,无法删除属性名  自定义属性无法控制
2. 中括号 + key 
	divBox [ ' mm ' ] = '  '
	删除了值,属性名还在   自定义无法控制
3.  removeAttribute 
	divBox.removeAttribute( ' mm  '  )
	连根拔起  属性名和属性值都删除了
```

### 2-节点

#### 2-1种类

```
1.元素节点
	类型 :  1
	名称 :  大写标签名
	内容 : null
2.属性节点
	类型 :  2
	名称 :  属性名
	内容 : 属性值
3.文本节点
	类型 : 3
	名称 : #text
	内容 :  文本内容
4.注释节点
	类型 : 8  
	#comment
	内容 : 注释内容
```

#### 2-2特性

```
节点类型--nodeType
节点名称--nodeName
节点值----nodeValue
```

#### 2-3子节点--childNodes

```
把空的文本节点当成节点
获取所有元素的子节点
	元素节点
	文本节点
	注释节点
```

#### 2-4Children

```
Children
	只显示元素节点即使非空的文字节点也不显示
	获取所有子元素节点--元素节点
```

### 3-排他思想

```
先排除掉其他的(包括自己),最后再给自己(this)加想要的效果
```

### 4-设置索引index-->i

```js
lis[i].setAttribute('index', i);
```



##  webAPI第3天

### 1-文本节点

#### 1-节点与元素节点

##### 1-1上一个节点与上一个元素节点

```
console.log(pBox.previousSibling);//文本:回车
console.log(pBox.previousElementSibling);//元素节点
```

##### 1-2下一个节点与下一个元素节点

```
console.log(box.nextSibling); //文本: 回车
console.log(box.nextElementSibling); // 元素节点
```

##### 1-3第一个子节点与子元素节点

```
console.log(box.firstChild);  // 元素/文本/注释
console.log(box.firstElementChild);  // 元素
```

##### 1-4最后一个子节点与最后一个元素节点

```
console.log(box.lastChild); // 文本: 回车
console.log(box.lastElementChild); //元素节点
```

##### 1-5如何获得父节点

```
通过子元素获得父元素
console.log(box.parentElement);
comsole.log(box.parentNode);
```

#### 2-克隆节点与追加节点

##### 2-1克隆节点

```
返回值,返回一个新节点
cloneNode(  )  克隆节点, 没有节点内容   
cloneNode(true)  包括节点内容
克隆注意id问题
newBox.id += index;
idnex ++;
```

##### 2-2追加节点

appendChild(   );  追加到父元素的后面

#### 3-创建元素与删除元素

##### 1-创建新元素

```
 创建新元素 :  creatElem( 标签名 ) 
 只有document可以创建新的元素
 document.createElement(  )    ---快捷键  doc
```

##### 2-删除元素

```
 删除元素 : removerChild ( 需要删除的元素)
 删除元素必须由父元素控制删除
 removerChild(pArr[3])---删除指定元素
 利用for循环removerChild(pArr[0])---删除所有元素
 (父元素).innerHTML =  '  ';   删除所有元素--简单快捷建议使用
```

#####  3-插入元素

```
插入元素: insertBefore(需要插入的元素)
 父元素.insertBefore(新元素,位置元素)
 如果想插入到后面,那么必须获得下一个元素来设置
```

#####  4-替换元素

```
 父元素: replaceChild(新元素,旧元素)
 由父元素调用,直接替换旧元素
```

#####  5-键盘事件

```
 onkeyup : 键盘弹起
 onkeydown : 键盘按下
 onkeypress : 键盘按下(屏蔽功能键)
```

#####  6-输入框的内容

 获得输入框内容   input.value

#####  7-判断文字是否存在

```
字符串.indexOf(文字)
如果等于-1就代表不存在
```

#### 4-静态结构与动态结构

使用querySelectorAll拿到的结构属于静态结构,后续document的改变对他没有影响
getElementsByTangName: 动态结构,会根据document的改变而改变

## webAPI第4天

### 1- 定时器

##### 1-普通版定时器

每隔一段时间,就执行某个操作一次  如:闹钟

```js
            // 声明定时器
            // 1. 利用匿名函数的方式来声明
            setInterval (
                function(){
                    console.log('哥哥,我爱你');
                },1000
                // 1000是毫秒,也就是一秒钟
            )
             // 2. 利用封装函数方法
            //  timeID是定时器的编码
             setInterval(love,1000);
```

##### 2-倒计时版定时器

```js
            // 1.用匿名函数
            // timeID = setTimeout(
            //     function () {
            //         console.log('现场燃爆了');
            //     }, 3000
            // )
            // 2. 函数封装定时器
            timeID = setTimeout(boomEgg, 3000);
```
总结: 
```
setlnterval---普通定时器
clearInterval(timeID)---清空定时器
----------------------------------
setTimeout---倒计时定时器
clearlTimeout(timeID)---清空定时器
普通定时器:每隔一段时间就执行一次
倒计时定时器:倒数结束之后,会执行一次代码,之后定时器就结束
```

##### 3-定时器动画

```
1.利用定时器修改top或者left=值
2.每隔一段时间就修改位移距离
3.赋值时记得拼接单位
4.需要给动画设置到达终点停止定时器
5.注意定时器加速问题
```

##### 4-盒子平移动画js

```
1. 互相干扰  因为共用同一个timeID
2. 互不干扰  利用元素对象保存各自的timeID
```

##### 5-offset家族

```
1. 盒子真实宽度---offsetWidth
2. 盒子真实高度---offsetHeight
3. 与父元素左边距离---offsetLeft
4. 与父元素右边距离---offsetTop
```

##### 6.-动画封装

```js
// 2. 封装动画函数
    function moveAnimation(elm,target) {
        // 3. 清空定时器
        clearInterval(elm.timeID);
        // 4. 获得当前元素的位置
        let elmLeft = elm.offsetLeft;
        // 5. 设置步长
        // 如果是往右走,那么步长为正数
        // 如果是往左走,那么步长为负数
        // 问题: 如何判断.步长是正数还是负数
        // 还没有到终点,那就继续走,就是正数
        // 如果已经超过终点,那就需要回头,就是负数
        //  目标      当前
        // target - elmLeft > 0 ,代表你还没到终点,继续走,正数
        // target - elmLeft < 0 ,代表你已经超过终点,往回走,负数
        let step = (target - elmLeft) > 0 ? 2 : -2;
        // 5. 设置定时器
        elm.timeID = setInterval(
            function () {
               // 6. 修改当前位置
               elmLeft += step; 
               // 7. 判断盒子需不需要继续移动
               // 如果剩余距离大于步长,那么继续走
               // 如果剩余距离小于步长,那么写死终点,并停止定时器
               // 剩余距离: 目标 - 当前---> Math.abs(target - elmLeft)
               if (Math.abs(target - elmLeft) > Math.abs(step)) {
                   // 如果剩余距离大于步长,那么继续走
                   elm.style.left = elmLeft + 'px';
               } else {
                   // 如果剩余距离小于步长,那么写死终点,并停止定时器
                   elm.style.left = target + 'px';
                   clearInterval(elm.timeID);
               }
            },5
        )
    }
```

##### 7-判断回车

e.keyCode == 13

## webAPI第5天

### 1-简单轮播图

```c
        // 需求:
        // 点击数字按钮.背景会发生改变: 设置类名current
        // 点击数字按钮,对应的ul需要发生位移: 调用动画函数
        // 动画函数(谁动,去哪)
        // 谁动: ul盒子
        // 去哪: 根据按钮的下标来确定位移的距离
        // 1. 获得需要的元素
        let spanArr = document.getElementsByTagName('span');; //数字按钮
        let ulBox =document.getElementsByTagName('ul')[0];; //运动元素
        let moveWidth = document.getElementsByClassName('inner')[0].offsetWidth; //位移单位的长度
        // 2. 遍历数字按钮设置点击事件
        for (let i = 0; i < spanArr.length; i++) {
            // 4. 给每一个按钮设置索引: index = i
           spanArr[i].setAttribute('index',i);

            //  3. 设置点击事件,修改背景颜色
            spanArr[i].onclick = function () {
                // 排他思想
                for (let j = 0; j < spanArr.length; j++) {
                    spanArr[j].className = '';
                }
                this.className = 'current';

                // 5. 根据按钮的索引,来确定位移的距离
                // 按钮索引    目标距离
                // 0           0 * 单位距离
                // 1           1 * 单位距离
                // 2           2 * 单位距离
                // 获得当前点击的按钮索引值
                let index = this.getAttribute('index');
                // 6. 计算位移的目标距离
                //  注意,因为动画整体失望左边移动,所以方向是负数
                let target = -index * moveWidth;
                // 7. 调用动画函数
                moveAnimation(ulBox, target);
            }
        }
```

### 2-焦点轮播图

```
//当鼠标移入,箭头按钮出现
// 当鼠标移出,箭头按钮消失
// 左边箭头,上一页功能
// 右边箭头,下一页功能
// 根据点击的次数,来决定位移的距离
// 注意: 按钮的点击是有限制
//  位移距离 =  -点击次数  *  moveWidth;
let target = -clickCount * moveWidth;
```

### 3-简单焦点轮播图

```css
       // 3. 给每一个数字按钮设置点击事件
        for (let i = 0; i < spanArr.length; i++) {
            // 设置索引
            spanArr[i].setAttribute('index', i);
            spanArr[i].onclick = function () {
                for (let j = 0; j < spanArr.length; j++) {
                    spanArr[j].className = '';
                }
                this.className = 'current';
                let target = -this.getAttribute('index') * moveWidth;
                moveAnimation(ulBox, target);
                // 6. 每次点击数字按钮的时候,要让箭头按钮保持同步
                // 将index与clickCount进行同步
                clickCount = this.getAttribute('index');
```

### 4-自动无缝轮播图

```css
// 1. 获取需要的元素
    let ulBox = document.getElementsByTagName('ul')[0];//位移的元素
    let timeID;
    // 2. 设置一个定时器(不需要停止,永动机)
    timeID = setInterval(moveInterval,8);
    function moveInterval( ) {
        let ulLeft = ulBox.offsetLeft;//当前位置
        // 3. 修改位移的距离,整体往做运动,所以是负数
        ulLeft += -2;
        // 4. 将修改的位移,赋值给ul
        // 判断: 当前ul位移是否已经达到替身图片
        // 如果是,那么要立刻切换回第0张
        // 如果已经到达替身图片,那就代表已经位移了四张图片的宽度总和: 1200
        if (ulLeft > -1200) {
            // 还没有到替身图片,可以继续平移
            ulBox.style.left = ulLeft + 'px';
        } else {
            // 已经到达替身图片,再继续就会穿帮
            // 应该立刻切换回第0 张的位置
            ulBox.style.left = '0px';
        }
    }
    document.getElementById('divBox').onmouseover = function  ( ) {
        clearInterval(timeID);
        // 停止定时器
    }
    document.getElementById('divBox').onmouseout = function  ( ) {
         timeID = setInterval(moveInterval,8);
        //  重启定时器
    }
```

### 5-完整版轮播图

```
    // 需求:
    // 根据图片的数量来创建数字按钮
    // 克隆第0张图片的元素,追加到最后,作为替身图片
    // 点击数字按钮,会修改背景颜色
    // 点击数字按钮,ul元素会进行位移
    // 鼠标悬停会出现箭头按钮
    // 下一页功能
    // 上一页功能
    // 箭头按钮与数字按钮也要同步
    // 自动轮播功能
    // 自动轮播的时候,数字按钮也要同步
```

## webAPI第6天

### 1-获得元素样式属性

```js
window.getComputedStyle(元素)['属性名']
通过封装函数减少代码量
```

### 2-scrool家族

```css
scrollWidth   内容的宽---不受隐藏影响
scrollHright  内容的高---不受隐藏影响
scrollTop    垂直滚动距离
scrollLeft   水平滚动距离
```

### 3-滚动事件

```css
 onscroll事件   当滚动的时候回持续触发
获得页面滚动距离 
```

### 4-client家族

```css
宽高+padding
clientWidth    内容区域宽度
clientHeight   内容区域高度
---------------------
clientTop    上边框宽度
clientLeft   左边框宽度
```

### 5-获得页面滚动距离

```css
document.body  body标签
document.documentElement html标签
兼容方式:
1. scrollTop:document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop || 0
2. scrollLeft:document.documentElement.scrollLeft || window.pageXOffset || document.body.scrollLeft || 0
```

### 6-获得页面内容区域

```css
1. clientWidth: window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth || 0
2. clientHeight:window.innerHeight|| document.documentElement.clientHeight || document.body.clientHeight || 0
```

### 7-事件对象

```css
e = window.event || e;
事件对象: 不管是哪个事件被触发,都会产生事件对象,里面保存了一些与事件触发相关的信息

事件对象的三个坐标
1. clientX--Y
可视区域的左上角与触发点的距离
滚动出去看不见的区域是不算可视的
    console.log('clientX:' + e.clientX);
2. pageX--Y
页面的左上角与触发点的
页面区域包括滚动出去的区域(不管页面有没有滚动)
    console.log('pageX' + e.pageX);
3. screenX--Y
屏幕的左上角与触发点的距离
	console.log('screenX' + e.screenX);

```

### 8-注册事件的方法

```
1. 利用on关键字----无法同时存在多个相同事件类型
2. 利用add方法
addEventListener('事件类型',执行函数,false)
事件类型:不要+on--->click,mouseover等
```

### 9-事件源

```
e.target---事件源:触发事件的源头
```

### 10-冒泡与捕获

```
冒泡:从内到外,从小到大
捕获:从外到内,从大到小
e.stopPropagation();
```

### 11-事件阶段

```
e.eventPhase
1-捕获
2-正常
3-冒泡
```

## webAPI第7天

### 1-window中三个事件

```css
1. window.onload --> 等页面加载完毕之后执行
2. window.onbeforeunliad -->页面关闭之前,要关闭还没关闭的一刹那
3. window.onunload -->页面正在关闭(执行完这个事件,整个页面就关闭了)
```

### 2-location对象

```css
1.显示网站当前地址---->console.log(location.href)
2.修改当前地址,跳转页面---->location.href = 'http://www/jd.com';
                          location.assign('http://www.jd.com');
                          location = 'http://www.jd.com';
3.替换页面地址------->location.replace('http://www.jd.com');
3.重载页面------->location.reload();
```

### 3-hisstory对象

