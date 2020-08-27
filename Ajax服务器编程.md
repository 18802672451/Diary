## Ajax服务器编程

### Ajax第一天
#### 1-服务器入门知识
##### 	1.了解服务器
###### 		可以提供某种服务的机器(电脑)
​		成为服务器:安装对应的软件
| 音乐服务器 |    QQ音乐,  网易云    |
| :--------: | :-------------------: |
| 视频服务器 |   腾讯视频,  爱奇艺   |
| 文件服务器 |    百度网盘,  迅雷    |
| 邮箱服务器 |   QQ邮箱,  263邮箱    |
| web服务器  | 谷歌浏览器   phpstudy |

##### 	2.掌握浏览器与服务器交换流程
​		a. 浏览器的访问服务器 的几种方式
​			直接输入地址    (  a标签的href ---- window.loaction.href  ---- 网页会跳转 )   ajax   网页不会跳转 
​		b.浏览器访问服务器三个流程
​			请求----处理---响应 			

#### 2-ajax技术

ajax作用: 在网页不挑战的情况下向服务器请求数据进行    局部刷新   节省网页性能(避免不必要的重复)

###### 2-1ajax工作流程

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
    <a href="https://autumnfish.cn/api/joke">点我看笑话</a>

    <div id="box"></div>

    <script>
        /* 
        
        1. ajax技术 ： 在网页不跳转的情况下向服务器请求数据。
        2. XMLHttpRequest 对象（xhr小黄人对象） ： 负责实现ajax技术的内置对象。
            2.1 创建XHR对象
                * let xhr = new XMLHttpRequest();
            2.2 设置请求方法和地址
                * xhr.open('get','url');
            2.3 发送请求
                * xhr.send();
            2.4 注册响应事件
                * xhr.onload = function(){};
        */


        //1.创建XHR对象
        let xhr = new XMLHttpRequest();
        //2.设置请求方法和地址
        xhr.open('get','https://autumnfish.cn/api/joke');
        //3.发送请求
        xhr.send();
        //4.注册响应回调事件
        /*注意点 
        a. 这个事件不会注册时候触发。 触发时机： 服务器成功响应数据
        b. 这个事件触发时间不固定的 ： 取决于 你的带宽，数据大小，服务器带宽
         */
        xhr.onload = function(){
            //服务器成功响应数据
            console.log( xhr.responseText );
            //显示到页面
            document.querySelector('#box').innerHTML = xhr.responseText;
        };

    </script>
</body>
</html>
```

###### 2-2ajax注意点get与post

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <style>
        .info {
            color: red;
        }
    </style>
</head>

<body>
    <h2>用户注册</h2>
    <input type="text" placeholder="请输入注册的用户名" class="username" />
    <span class="info"></span>
    <br />
    <input type="button" value="注册" class="submit" />

    <script src="./libs/jquery-1.12.4.min.js"></script>

    <script>
        /*学习目标： post请求发送参数 

            1. post请求发送参数
                a.需要设置固定的请求头： 'application/x-www-form-urlencoded'
                b.参数在xhr.send('key=value')
                    * 注意没有问号

            2. get与post发送参数区别
                * a. post需要单独设置请求头
                * b. 发送位置不同
                    * get在url后面发：           url?key=value 
                    * post在send()方法里面发：   xhr.send('key=value')
        */

        /* 用户注册
        - 请求地址：https://autumnfish.cn/api/user/register
        - 请求方法：post
        - 请求参数：username
        */

        /*思路分析 
        1.给注册按钮注册事件
        2.获取输入框文本
        3.ajax发送请求
        4.服务器响应之后渲染页面
        */

        //1.给注册按钮注册事件
        $('.submit').click(function () {
            //2.获取输入框文本
            let username = $('.username').val();
            //3.发送ajax请求

            //(1)创建xhr
            let xhr = new XMLHttpRequest();
            //(2)设置请求方法和地址
            xhr.open('post', 'https://autumnfish.cn/api/user/register');

            //(3)设置请求头（只有post才需要，为固定格式）
            xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');

            //(4)发送ajax请求
            xhr.send('username=' + username);
            //(5)注册响应事件
            xhr.onload = function () {
                $('.info').text(xhr.responseText);
            }

        });

    </script>
</body>

</html>
```

#### 3-JSON格式数据

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
        1. JSON是什么 ：JSON是一种数据格式，本质是字符串。

        2. JSON作用：解决跨平台问题。
            服务器的编程语言有很多种（python,java,php等）,而每一种编程语言的数据类型不同的。
        他们之间不能互通。

        3. JSON与JS互转
            JSON 转 JS ； JSON.parse(js对象)
                * 服务器一般返回json对象，不能直接使用需要转成js对象
            JS转JSON ： JSON.stringify(js对象)

        */

        //1. json数组必须使用[]包起来
        //json里面的内容必须要使用双引号包起来
        let jsonArr = '["10","20","30"]';

        console.log(jsonArr);
        let jsArr = JSON.parse(jsonArr);
        console.log(jsArr);

        //2. json对象必须要使用{}包起来

        let jsonObj = '{"name":"张三"}';

        let jsObj = JSON.parse(jsonObj);
        console.log(jsObj);


        //3. js -> JSON
        let js = {
            name:'张三',
            age:20
        };

        console.log( JSON.stringify(js) );//转json字符串
          
    </script>
</body>

</html>
```

##### 3-1JQ使用ajax介绍

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
</head>

<body>
    <input type="button" value="get方法" class="get" />
    <input type="button" value="post方法" class="post" />
    <input type="button" value="ajax方法" class="ajax" />

    <script src="./libs/jquery-1.12.4.min.js"></script>

    <script>
        /* 学习目标： jq使用ajax
          $.get()     :  发送get请求
          $.post()    :  发送post请求
          $.ajax()    :  发送get+post请求
        
        */

        //1. $.get()     :  发送get请求
        $('.get').click(function () {
            /**
            * @description:发送get请求
            * @param {type} url : 地址
            * @param {type} data : 参数
            * @param {function} callback : 响应回调
            * @return: 
            */
            $.get('https://autumnfish.cn/api/hero/detail','name=娑娜',function(backdata){
                console.log(backdata);  
            });

            $.get('https://autumnfish.cn/api/hero/detail', {
                name:'娑娜'
            }, function (backdata) {
                console.log(backdata);
            });
        });

        //2. $.post()     :  发送post请求
        $('.post').click(function () {
            /**
            * @description:发送get请求
            * @param {type} url : 地址
            * @param {type} data : 参数
            * @param {function} callback : 响应回调
            * @return: 
            */
            $.post('http://www.tuling123.com/openapi/api', {
                key: '2162602fd87240a8b7bba7431ffd379b',
                info: '请告诉我舔狗的下场。'
            }, function (backdata) {
                console.log(backdata);
            });
        });


        //3. $.ajax()    : 发送get与post
        $('.ajax').click(function () {
            /**
            * @description:
            * @param {对象} 
            *   url:请求路径 
            *   type:请求方法
            *   data:请求参数
            *   success:响应回调  function(backData){}
            * @return: 
            */
            $.ajax({
                url:'https://autumnfish.cn/api/hero/detail',
                type:'get',
                data:{
                    name:'娑娜'
                },
                success:function(backdata){
                    console.log(backdata);

                }
            });

            $.ajax({
                url: 'http://www.tuling123.com/openapi/api',
                type: 'post',
                data: {
                    key: '2162602fd87240a8b7bba7431ffd379b',
                    info: '请告诉我，我的女朋友在哪里？'
                },
                success: function (backdata) {
                    console.log(backdata);
                }
            });
        });


    </script>
</body>

</html>
```

##### 3-2dataType检测json格式

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

    <script src="./libs/jquery-1.12.4.js"></script>
    <script>
        /* 
        jq使用ajax的注意点 ： 设置dataType属性检测json格式
        */

        $.ajax({
            url: 'http://www.tuling123.com/openapi/api',
            type: 'post',
            /* 
            限制服务器返回的数据为json格式
            如果是json ： jq会自动帮我们转成json
            如果不是json: jq不会执行sucess方法，避免代码出错
            */
            dataType:'json',
            data: {
                key: '2162602fd87240a8b7bba7431ffd379b',
                info: '请告诉我，我的女朋友在哪里？'
            },
            success: function (backdata) {
                console.log(backdata);
            }
        });    
        
    </script>
</body>

</html>
```

### Ajax第二天

#### 1-XML格式介绍  (了解)

##### 1-1 XML数据格式

- 1. 解决跨平台:	json(目前主流)  	XML(以前的主流)

  2. 如何解析XML数据格式

     - 不能使用json方式来解析XML

     -  jquert语法:	$('选择器' , XML数据).text( )

#### 2-模板引擎

​	模板引擎:

​	学习传送门:  <https://aui.github.io/art-template/zh-cn/index.html>

- 模板引擎流程

  1. 导包

     <script src="./libs/template-web.js"></script>

  2. 写模板

     <script id='tpl' type="text/html"></script>

      a. 一定要写ID属性

      b. 一定要设置type属性  建议写成 type=text/html

  3. 调用官方API

     `let htmlStr =  template('tpl', jsonObjc.data);`

     第一个参数: 模板id	第二个参数: 要渲染的对象	返回值: 渲染好的html 

     模板引擎核心原理:   字符串替换

  4. 渲染解析好的html字符串

     `document.body.innerHTML = htmlStr;`

- 模板引擎语法

  ```html
  <script id="weather_list" type="text/html">
  	<!-- 模板语法 -->
  	<!-- (1)输出 -->
  	<!-- 第一种写法: 大胡子mustache语法 -->
  	<p>{ { data.ganmao } } </p>
  	<!-- 第二种写法:    原始语法 -->
  	<p> <%= data.ganmao %> </p>
  
  	<!-- (2)条件 -->
  	{ { if data.forecast } }
  
  	{ { /if}}
  
  	<!-- (3)循环 -->
  	{ { each target}  }
           <li>
                  <span>数组下标: {{$index}}</span>
                  <span>数组元素: {{$value}}</span>
           </li>
  	<!-- $value 与 $index 可以自定义：{{each target val key}}。 -->
  	{ { /each}}
  </script>
  ```

- 模板引擎易错点总结

  1. 导包

     a. 路径错误  :   固定格式报错 	'template' is not defined

  2. 写模板

     a.id错误

     b.必须要设置type=text.html  

      * 不能不写,也不能写成 type=text/javascript 

        原因 :   默认值: text/javascript  默认浏览器渲染引擎从上往下解析DOM树的时候,如果发现script标签,需要js引擎来解析(识别出这是js代码)

        type=text/html   :    告诉浏览器这里面不是js代码,不要使用js引擎来解析

     c.模板语法错误   :      固定格式报错  " 告诉你第几行模板语法错误"

     d.对象取值语法错误(单词写错)   :   不报错但是也不会渲染

  3. 调用官方API

     a.id错误  :  固定错误模板找不到 template not found: Cannot read property 'value' of null

     b.第二个参数必须是js对象

  4. 渲染页面

     a. 父元素选择器写错了

#### 3-实战案例

##### 3-1英雄查询

```html
<!DOCTYPE html>
<html lang="zh-cn">

<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Bootstrap 101 Template</title>

  <!-- 导包 -->
  <script src="./libs/js/jquery-1.12.4.js"></script>
  <script src="./libs/js/bootstrap.min.js"></script>
  <link rel="stylesheet" href="./libs/css/bootstrap.min.css">
  <script src="./libs/js/template-web.js"></script>

</head>

<body>
  <nav class="navbar navbar-light bg-light">
    <form class="form-inline" >
      克鲁赛德战记
      <input class="form-control mr-sm-2 search" type="search" placeholder="请输入英雄名字" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0 btn-search" type="submit">搜索</button>
    </form>
  </nav>
  <!-- 栅格系统 -->
  <div class="container">
    <div class="row">
      <div class="col-lg-3">
        <div class="media">
          <div class="media-left">
            <a href="#">
              <img class="media-object" src="http://p0.qhimg.com/dr/72__/t016f2baa3729884891.png" alt="...">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">英雄名字</h4>
            英雄技能
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 写模板 -->
  <script id="hero_list" type="text/html">
    {{ each list v }}
    <div class="col-lg-3">
      <div class="media">
        <div class="media-left">
          <a href="#">
            <img class="media-object" src="{{ v.icon }}" alt="...">
          </a>
        </div>
        <div class="media-body">
          <h4 class="media-heading">{{ v.name }}</h4>
          {{ v.skill }}
        </div>
      </div>
    </div>
    {{ /each }}
  </script>
  <script>
    /*
    请求地址：https://autumnfish.cn/api/cq
    请求方法：get
    请求参数：query
    参数名	参数说明	备注
    query	英雄名	可以为空，为空获取所有数据
    */

    /*思路分析 
    1.给搜索按钮注册点击事件
    2.获取输入框文本
    3.ajax发送请求
    4.服务器响应之后 模板引擎渲染页面
    */

    //1.给搜索按钮注册点击事件
    $('.btn-search').click(function(e){
      /* 注意点：表单里面的按钮有一个默认跳转事件。 一般需要阻止 */
      e.preventDefault();

      //2.获取输入框文本
      let name = $('.search').val();
      console.log(name);
      
      //3.ajax发送请求
      $.ajax({
        url:'https://autumnfish.cn/api/cq',
        type:'get',
        dataType:'json',
        data:{query:name},
        success: function(backData){
          console.log(backData);
          //4.服务器响应之后 模板引擎渲染页面
          $('.row').html(template('hero_list',backData));
          
        }
      });      
    });

  let name = '123';
  // url('123')
  let str1 = 'url(' + name + ')';//url(123)
  let str2 = 'url("' + name + '")';//url("123")
  console.log(str1);
  console.log(str2);
  </script>
</body>

</html>
```

##### 3-2天知道(天气查询)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <title>天知道</title>
  <link rel="stylesheet" href="css/reset.css" />
  <link rel="stylesheet" href="css/iconfont.css" />
  <link rel="stylesheet" href="css/main2.css" />
  <script type="text/javascript" src="js/jquery-1.12.4.min.js"></script>
  <style>
    .tem .iconfont {
      font-size: 50px;
    }
  </style>
</head>

<body>
  <div class="wrap">
    <div class="search_form">
      <div class="logo"><img src="img/logo.png" alt="logo" /></div>
      <div class="form_group">
        <input type="text" class="input_txt" placeholder="请输入查询的天气" />
        <button class="input_sub">搜 索</button>
      </div>
      <div class="hotkey">
        <a href="javascript:;">北京</a><a href="javascript:;">上海</a><a href="javascript:;">广州</a><a
          href="javascript:;">深圳</a>
      </div>
    </div>
    <ul class="weather_list"></ul>
  </div>

  <!-- 导入jQ -->
  <script src="./js/jquery-1.12.4.min.js"></script>
  <!-- 导入模板引擎 -->
  <script src="./js/template-web.js"></script>

  <!-- 写模板 -->
  <script id="weather_list" type="text/html">
    {{ each data.forecast v }}
    <li>
      <div class="info_type">
        <!-- 小雨 -->
        {{ if v.type.indexOf('小雨') != -1 }}
        <span class="iconfont">&#xe932;</span>
        <!-- 雨 -->
        {{ else if v.type.indexOf('雨') != -1 }}
        <span class="iconfont">&#xe931;</span>
        <!-- 晴 -->
        {{ else if v.type.indexOf('晴') != -1 }}
        <span class="iconfont">&#xe933;</span>
        <!-- 雨夹雪 -->
        {{ else if v.type.indexOf('雨夹雪') != -1 }}
        <span class="iconfont">&#xe934;</span>
        <!-- 阴 --> 
        {{ else if v.type.indexOf('阴') != -1 }}
        <span class="iconfont">&#xe92d;</span>
        <!-- 风 -->
        {{ else if v.type.indexOf('风') != -1 }}
        <span class="iconfont">&#xeb8c;</span>
        <!-- 雪 -->
        {{ else if v.type.indexOf('雪') != -1 }}
        <span class="iconfont">&#xeb87;</span>
        <!-- 多云 -->
        {{ else if v.type.indexOf('多云') != -1 }}
        <span class="iconfont">&#xeb79;</span>
        <!-- 雷 -->
        {{ else if v.type.indexOf('雷') != -1 }}
        <span class="iconfont">&#xeb77;</span>
        <!-- 冰雹 -->
        {{ else if v.type.indexOf('冰雹') != -1 }}
        <span class="iconfont">&#xeb76;</span>
        <!-- 雾霾 -->
        {{ else if v.type.indexOf('雾霾') != -1 }}
        <span class="iconfont">&#xeb75;</span>
        {{ /if }}
        
      </div>
      <div class="info_temp">高<b>{{ v.high.split(' ')[1] }}</b><br>低 {{ v.low.split(' ')[1] }}</div>
      <div class="info_date"><b>{{ data.city }}</b><span>{{ v.date }}</span></div>
    </li>
    {{ /each }}
  </script>

  <script>
    /*思路分析 
    1.搜索按钮点击事件
      1.1 获取输入框文本
      1.2 ajax发送请求
      1.3 服务器响应之后 模板引擎渲染页面
    
    2.热门城市点击事件
      2.1 输入框文本变成当前点击的a标签文本
      2.2 ajax发送请求
      2.3 服务器响应之后 模板引擎渲染页面

    3.页面一加载：请求第一个热门城市数据

    4.loading加载动画
      核心思路： gif动图实现
      步骤：
        显示： ajax发送之前
        隐藏： ajax响应之后

    */

    //1.搜索按钮点击事件
    $('.input_sub').click(function () {
      //获取输入框文本
      let city = $('.input_txt').val();
      //显示loading： ajax发送之前
      $('.input_sub').addClass('loading');

      //ajax请求
      $.ajax({
        url: 'http://wthrcdn.etouch.cn/weather_mini',
        type: 'get',
        dataType: 'json',
        data: { city: city },
        success: function (backData) {
          console.log(backData);
          //服务器给了数据之后，过一会儿再加载数据。让用户多看一会酷炫的加载动画
          setTimeout(function () {
            //隐藏loading： ajax响应之后
            $('.input_sub').removeClass('loading');
            //模板引擎渲染页面
            $('.weather_list').html(template('weather_list', backData));
          }, 1000);
        }
      });
    });

    //2.热门城市点击事件
    $('.hotkey>a').click(function () {
      //输入框文本变成当前点击的a标签文本
      $('.input_txt').val($(this).text());
      $('.input_sub').click();
    });

    //3.默认加载第一个热门城市
    $('.hotkey>a:eq(0)').click();
  </script>
</body>

</html>
```

##### 3-3聊天机器人

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <link rel="stylesheet" href="css/reset.css" />
  <link rel="stylesheet" href="css/main.css" />
  <script type="text/javascript" src="js/jquery-1.12.4.min.js"></script>
  <script type="text/javascript" src="js/scroll.js"></script>
  <script type="text/javascript" src="js/jquery-ui.min.js"></script>
  <script type="text/javascript" src="js/jquery.mousewheel.js"></script>
  <!-- 导入模板引擎 -->
  <script src="./js/template-web.js"></script>

  <title>聊天机器人</title>
  <style>
    img {
      width: 40px;
      height: 40px;
    }
  </style>
</head>

<body>
  <div class="wrap">
    <div class="header">
      <h3>舔狗王</h3>
      <img src="img/01.gif" alt="icon" />
    </div>
    <div class="main">
      <ul class="talk_list" style="top: 0px;"></ul>
      <div class="drag_bar" style="display: none;">
        <div class="drager ui-draggable ui-draggable-handle" style="display: none; height: 412.628px;"></div>
      </div>
    </div>
    <div class="footer">
      <img src="img/02.gif" alt="icon" />
      <input type="text" placeholder="说的什么吧..." class="input_txt" />
      <input type="button" value="发 送" class="input_sub" />
    </div>
  </div>

  <!-- 我的聊天模板 -->
  <script id="mine" type="text/html">
      <li class="right_word">
        <img src="img/02.gif" alt=""><span> {{ a }} </span>
      </li>
  </script>

  <!-- 机器人聊天模板 -->
  <script id="jiejie" type="text/html">
    <li class="left_word">
      <img src="img/01.gif" alt=""><span> {{ text }} </span>
    </li>
  </script>

  <script>
    /* 
    请求地址：http://www.tuling123.com/openapi/api
    请求方法：post
    请求参数：key,info
    2162602fd87240a8b7bba7431ffd379b
    a618e456f0744066840ceafb6a249d9d
    d7c82ebd8b304abeacc73b366e42b9ed
    7b1cf467c0394dd5b3e49f32663f8b29
    9fbb98effab142c9bb324f804be542ba
    */

    /* 思路分析
    1.发送按钮点击事件
      1.1 获取输入框文本
      1.2 生成自己的聊天内容
    2.ajax请求机器人的聊天内容
      2.1 服务器响应之后模板引擎渲染
    3.非空判断与文本清空
      非空判断： ajax发送之前
      文本清空 ： ajax响应之后
    */

    //1.发送按钮点击事件
    $('.input_sub').click(function () {
      /* 非空判断 */
      if( $('.input_txt').val().length == 0 ){
        alert('说点啥呢？');
        return;
      };

      //1.1 获取输入框文本
      let text = $('.input_txt').val();
      //1.2 渲染自己的文本
      // console.log( template('mine',{a:text}) );
      // ;
      $('.talk_list').append(template('mine', { a: text }));
      //1.3 自动滚到最底部
      resetui();

      /* 文本清空 */
      $('.input_txt').val('');

      //2.ajax请求机器人数据
      $.ajax({
        url: 'http://www.tuling123.com/openapi/api',
        type: 'post',
        dataType: 'json',
        data: {
          key: 'd7c82ebd8b304abeacc73b366e42b9ed',
          info: text
        },
        success: function (backData) {
          console.log(backData);
          $('.talk_list').append(template('jiejie', backData));
          //自动滚到最底部
          resetui();
        }
      });

    });
  </script>
</body>
</html>
```



### Ajax第三天

#### 1-案例-克鲁赛德战记

- .trim( )  只能去掉两边的空格 	.replace( )  去掉所有的空格,需要使用正则的全局匹配替换

![去掉空格](59期ajax/03-课程资料/第三天/01-教学资源/去掉空格.png)

- 如果是ajax动态添加的元素，需要注册委托事件。这种情况下在ajax中非常常见

  ​	入口函数解决 ： 元素一开始就有，但是太多了。 可能执行到js的时候还没有加载完。 保证一定要先让页面的元素加载完之后再获取DOM

  ​	事件委托:	 元素一开始没有，无法获取的。 这个元素是后来被动态追加到DOM树的。 只能注册委托事件

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <link rel="stylesheet" href="./css/index.css" />
  </head>
  
  <body>
    <img src="./img/header.png" alt="" class="header" />
    <div class="cq-wrap">
      <!-- 导航 -->
      <div class="nav">
        <ul>
          <li><img src="./img/sword.png" alt="" /><span>剑士</span></li>
          <li><img src="./img/knight.png" alt="" /> <span>骑士</span></li>
          <li><img src="./img/Archer.png" alt="" /> <span>弓手</span></li>
          <li><img src="./img/hunter.png" alt="" /> <span>猎人</span></li>
          <li><img src="./img/magic.png" alt="" /> <span>法师</span></li>
          <li><img src="./img/flamen.png" alt="" /> <span>祭司</span></li>
        </ul>
      </div>
      <!-- table -->
      <table class="cq-list">
        <thead>
          <th>勇士</th>
          <th>技能</th>
          <th>武器</th>
        </thead>
        <tbody>
          <tr>
            <td>
              <img class="icon" src="http://p6.qhimg.com/dr/72__/t01b8063ea608652431.png" alt="" />
              <span>
                涅斯军长官尤莉娅
              </span>
            </td>
            <td>
              <img class="skill" src="http://p9.qhimg.com/dr/52__/t01087d8e61575ab25d.png" alt="" />
              注射!
            </td>
            <td>
              <img class="weapon" src="http://p6.qhimg.com/dr/45__/t0178ac936dcb72650f.png" alt="" />
              疫苗-G
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- 遮罩层 -->
    <div class="cover" style="display: none">
      <img class="loading" src="./img/loading01.gif" alt="" />
    </div>
  
    <script src="./js/jquery-1.12.4.min.js"></script>
    <!-- 模板引擎 -->
    <script src="./js/template-web.js"></script>
  
    <!-- 英雄列表模板 -->
    <script id="hero_list" type="text/html">
      {{ each data.heros v }}
      <tr>
        <td>
          <img class="icon" src="{{ v.heroIcon }}" alt="">
          <span>
            {{ v.heroName }}
          </span>
        </td>
        <td>
          <img class="skill" src="{{ v.skillIcon }}" alt="">
          {{ v.skillName }}
        </td>
        <td>
          <img class="weapon" src="{{ v.weaponIcon }}" alt="">
          {{ v.weaponName }}
        </td>
      </tr>
      {{ /each }}
    </script>
  
    <script>
      /*接口文档 
        请求地址:https://autumnfish.cn/api/cover/random
        请求方法：get
        请求参数：无
  
        请求地址：https://autumnfish.cn/api/cq/category
        请求方法：get
        请求参数：type
        参数名	参数说明	备注
        type	英雄类型	不能为空，可选值有:剑士，骑士，弓手，猎人，法师，祭司
        请求地址：https://autumnfish.cn/api/cq/gif
        请求方法：get
        请求参数：name
        参数名	参数说明	备注
        name	英雄名
  
       */
  
      /*思路分析 
      1. 每隔6s,更新随机背景图片
  
      2. 点击每一个tab栏：tab栏切换
       2.1 排他思想修改样式
       2.2 获取当前点击的type类型
       2.3 ajax发送请求
       2.4 服务器响应之后  模板引擎渲染页面
  
      3. 点击头像icon
       3.1 获取当前头像对应的name
       3.2 加载loading动画
       3.3 ajax发送请求
       2.4 服务器响应之后  渲染页面
  
      4. 点击cover ： 隐藏cover
     */
  
      /* 功能1 ： 每隔6s,更新随机背景图 */
      setInterval(function () {
        $.ajax({
          url: 'https://autumnfish.cn/api/cover/random',
          type: 'get',
          dataType: 'json',
          success: function (backData) {
            console.log(backData);
            //显示背景图
            $('body').css('backgroundImage', 'url(' + backData.url + ')');
          }
        });
      }, 15000);
  
      /* 功能2：点击每一个tab栏：tab栏切换  */
      $('.nav>ul>li').click(function () {
        //(1)排他思想修改样式
        $(this).addClass('active').siblings().removeClass('active');
        //(2)获取当前点击的英雄type
        let type = $(this).children('span').text();
        console.log(type);
        //(3)ajax发送请求
        $.ajax({
          url: 'https://autumnfish.cn/api/cq/category',
          type: 'get',
          dataType: 'json',
          data: { type: type },
          success: function (backData) {
            console.log(backData);
            //(4)模板引擎渲染页面
            $('table>tbody').html(template('hero_list', backData));
          }
        });
      });
  
      /* 页面一加载：默认请求第一个tab栏数据 */
      $('.nav>ul>li:eq(0)').click();
  
      /* 功能3：点击icon头像 加载gif技能动图 
      
      注意点 ： 
        (1). ajax动态添加的元素 需要注册委托事件(ajax中非常常见)
        (2). 如果参数有空格的话，可以使用trim()方法去除空格
      */
      $('table>tbody').on('click', '.icon', function () {
        //(1)获取当前头像对应的name
        let name = $(this).next().text().trim();
        console.log(name);
        //显示loading
        $('.cover').fadeIn();
        //(2)ajax发送请求
        $.ajax({
          url: 'https://autumnfish.cn/api/cq/gif',
          type: 'get',
          dataType: 'json',
          data: { name: name },
          success: function (backData) {
            console.log(backData);
            //服务器响应之后，将返回的gif显示到cover>img中
            $('.cover>img').attr('src', backData.data.skillGif);
          }
        });
      });
  
      /* 4. 点击cover ： 隐藏cover */
      $('.cover').click(function () {
        $(this).fadeOut(500, function () {
          $(this).children('img').attr('src', './img/loading01.gif');
        });
      });
  
    </script>
  
  </body>
  
  </html>
  ```

  

#### 2-http原理了解

##### 2-1 onreadystatechange事件介绍

```html
<script>
	/* onreadystatechange 事件
	onreadystatechange 与 onload异同点
		相同点: 作用一致  都是服务器响应事件
		不同点: 浏览器兼容性不同
			onload: 最新出的. 	旧版浏览器不支持的
			onreadystatechange:	浏览器兼容性更好
				a. 会调用多次
				b. 需要判断 xhr.readyState==4  才能获取服务器响应数据
</script>
```

##### 2-2 ajax原理

![请求报文三部分](59期ajax/03-课程资料/第三天/01-教学资源/请求报文三部分.png)

------

![响应报文三部分](59期ajax/03-课程资料/第三天/01-教学资源/响应报文三部分.png)

------

![ajax原理](59期ajax/03-课程资料/第三天/01-教学资源/ajax原理.png)

```html
<script>
	/*
    1. http网络协议原理 :	约定 客户端(浏览器) 与 服务端(后台) 数据交换的格式.
    	1.1 客户端数据必须是	请求报文
    		请求行	:	请求方法和地址
    		请求头 :	数据格式(浏览器告诉服务器,我发你的是什么数据)
    		请求体 :	请求参数
    	1.2 服务端数据必须是	响应报文
    		响应行 :	请求状态码
    			200	:	成功
    			400/3/4	:	失败	(浏览器的锅)
    			400	:	失败	(服务器内部错误)
    		响应头	:	数据格式(服务器告诉浏览器,我给你的数据格式)
    		响应体	:	服务器响应数据
    2. ajax原理 :	就是设置请求报文三个部分
    
	*/
</script>
```

