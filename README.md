# Front-end-knowledge-point

javascript的复习


（一）. 一些关键词
*continue 跳出本次循环
*break 跳出循环

（二）. 不常有的语法书写
switch( 判断条件 ) {
  case 结果：
  break 防止击穿
}

（三）. typeof 的数据类型
*number
*string
*object
*boolean
*function
*undefined

（四）. 函数中常见的
*a. arguments 实参的集合
*b. 函数默认返回undefind
*c. getComputedStyle(obj)[attr]
*d. obj.currentStyle[attr]

（五）. 定时器异步的
setInterval()
clearInterval();
setTimeout();
clearTimeout();

还可以
setInterval("fn(2)",1000);

（六）. 运动框架Tween的使用，以及获取css 3d transfrom函数的使用
*mTween(el,target,time,type,callBack) target可以是一个拥有多个属性的对象

cssTransform(el,attr,val)  设置获取transfrom的样式
函数封装
tween.js

（七）作用域
var 关键词是把 变量名提到前面
function 是把整个函数提到前面 (var fn = function(){},同var一样)

（八）for in for of
for in 遍历的key值
for of（es6）遍历的val值

（九）JSONP的方法( 严格的书写规范 )
*JSON.parse()
*JSON.stringify()

（十）中文的排序方法
var arr = ["深圳","成都","北京","大连","武汉","长沙","上海","广州","杭州"];
var arrIndex = {
            北京:1,
            上海:2,
            广州:3,
            深圳:4,
            杭州:5,
            武汉:6,
            成都:7,
            长沙:8,
            大连:9
        };
arr.sort(function(a,b) {
     return arrIndex[a] - arrIndex[b]
});

( 十一 )
创建时间对象
new Date()  // 可以接受一串时间戳,创建时间对象

时间对象下的方法
*getFullYear() 年
*getMonth() 月 +1
*getDate() 日
*getDay () 周几 (周日为0)
*getHours() 小时
*getMinutes() 分钟
*getSeconds() 秒
*getTime() 时间戳

设置时间的字符串形式
new Date('月份『英文』 日,年 时:分:秒');
new Date(2016,9,1,10,10,10);

倒计时
事件差值计算公式,a时间 到 b时间
var t = Math.floor((a - b)/1000);
var str = Math.floor(t/86400)+'天'+Math.floor(t%86400/3600)+'时'+Math.floor(t%86400%3600/60)+'分'+t%60+'秒'


( 十二 ) apply call bind
改变函数内部的指向
apply(this的指向,[参数的集合]);
call(this的指向,参数a,参数b);
第一个参数为null,不改变this指向

Function.prototype.bind,改变this指向但是不会立即执行
var obj = {
  fn: function() { console.log(this); }     
}
setTimeout(obj.fn, 1000); //window
setTimeout(obj.fn.bind(obj),1000); //obj

借用系统对象上的方法(需要改变this指向)
例如：数组方法push
var arr1 = [1,2,3];
var arr2 = [4,5,6];
系统对象Array的原型上的方法
Array.prototype.push.apply(arr1,arr2); this指向arr1, arr1.push arr2
Array.prototype.slice.apply(类数组); 类数组变为数组,slice方法的this指向类数组
Array.prototype.shift.apply(类数组); 截取类数组

( 十三 ) 一元操作符
*delete
删除对象下的属性
delete obj.name

（十四）本地存储
local storage
环境: 服务器环境下
生命周期: 永远存在

常见的方法localStorage对象下
localStorage.getItem(key);
localStorage.removeItem(key);
localStorage.setItem(key,val);
localStorage.clear()

window.storage 事件(注意,触发事件后.浏览器所有同级页面都会触发该事件)

event对象下常用的属性
event.oldval; 修改前的信息
event.newval; 修改后的信息

（十五）字符串的常见的方法
模板字符串
`test${ 变量 }test${ 变量 }`

charAt();

1.查找
indexOf('test',n) 没有返回-1
includes() 是否包含,返回boolean

2.截取
subString(n,m)
slice(n,m)

3.分割成数组
split('') //参数''就是每一个都是数组的子项

4.大小写
toLowerCase();
toUpperCase();

5.去除首尾的空格
trim();



（十六）数组的常见方法
创建三种方法
new Array(); 长度
Array.of(); 内容
arr = [];

Es6中判断是不是数组类型
Array.isArray();

Es6中类数组转换成数组
Array.from();

1.查找
  indexOf();
2.添加 返回长度
  push();
  unshift();
3.删除 返回被删除的
  pop();
  shift();
4.截取 返回子数组
  slice(n,m); // 不写的话,全部截取
5.删除,替换,添加
  splice(n,m) // 删除n到m个
  splice(n,m,z) // m>n 替换n开始,m个,替换成z
  splice(n,m,z) // m<n m与n之间添加z
6.颠倒数组
  reverse();
7.数组拼接成字符串
  join(''); // 不写''会包含,
8.排序
  sort(); // a,b 是数组里的某一项
  sort(function(a,b){
    return a-b; (小到大)
    return b-a; (大到小)
    return Math.random() - 0.5 (随机排序)
  });
9.合并数组
  concat();
  arr1.concat(arr2);

           
数组常见的一些算法( 冒泡排序，快速排序,去重 )
###冒泡排序
var arr = [2,3,4,1,5,6];
for(var i=0; i<arr.length; i++) {
  for(var j=i+1; j<arr.length; j++) {
    if(arr[i] > arr[j]) {  // 从小到大
      var tran = arr[i];
      arr[i] = arr[j];
      arr[j] = tran;
    }
  }
}

###快速排序 // 递归
var array = [3,4,1,5,2,6];
function iSort(arr) {
  var left = [];
  var right = [];
  var filst = arr.shift();
  while(array.length) {
    var number = arr.shift();
    if( number<filst ) {
       left.push(number);
    }else {
       right.push(number);
    }
  }
  return iSort(left).concat(filst,iSort(right));
}

###数组去重的几种思路
var arr = [2,2,6,7,4,3,1,2,3,5,6,6,7,7,8,1,2];

思路一： // 最蠢的,性能最差的
for(var i=0; i<arr.length; i++) {
  for(var j=i+1; j<arr.length; j++) {
    if(arr[i] === arr[j]) {
      arr.splice(j,1);
      j--;
    }
  }
}

###思路二:
var obj = {};
var newArray = [];
for(var i=0; i<arr.length; i++) {
  if(!obj[arr[i]]) {
    obj[arr[i]] = 1;
    newArray.push(arr[i]); 
  }else {
    obj[arr[i]]++;
  }
}


（十七）DOM
DOM中常用的方法,属性

childNodes
obj.childNodes  obj的子节点列表集合
nodeType  // 当前元素的节点类型
attributes // 当前元素的属性集合
children // 元素子节点列表集合
firstElementChild // 第一个子节点
lastElementChild // 最后一个子节点
NextElementSibling // 下一个子节点
previousElementSibling // 上一个子节点
parentNode // 当前节点的父节点
offsetParent // 离当前元素最近的定位父级节点(没有默认为body)

offsetLeft offsetTop // 到定位父级的left,top值(没有定位父级html)
obj.style.width // 样式宽
obj.clientWidth // 可视区宽
obj.offsetWidth // 占位宽

getBoundingClientRect().left .top //相对可视区(会自动适应添加滚动条高度)

设置,获取,删除自定义属性
getAttribute(key)
setAttribute(key,val)
removeAttribute(key)

obj.createElement(TagName) //创建
obj.removeChild() //删除
obj.appendChild() //添加
obj.insetBefore(new,old) //添加
obj.replaceChild(new,old) //替换


DOM里获取表单元素可以通过name值
// 获取父级form
var oForm = document.getElementById('form');
// 通过input的name值获取元素
oForm.username;
PS：
 input.select() 选中页面内容

DOM操作表格



（十八）BOM
window.location
  window.location.href //url地址
  window.location.search //search值
  window.location.hash //hash值    window.onhashchange 事件

navigator
  navigato.userAgent 浏览器信息

常见的方法
  open();
  close();
  reload();
  document.write(val) //解析JS代码,任何JS代码,JSON.parse只能解析JS格式

各种常见的尺寸
原生 
 可视区尺寸
   window.innerWidth / document.documentElement.clientWidth
 滚动条滚动距离
   window.pageXOffset / document.documentElement.scrollLeft
   设置滚动条滚动距离 window.scrollTo(X,Y);
 内容宽高(包含margin)
   scrollHeight
 文档宽高
   document.body.offsetHeight

Jquery
  $obj.outerWidth(false/true) true时可以获取margin
  $obj.innerWidth() 不包含border和margin
  $obj.width 宽/高

 
document 一些属性
  document.image // 文档中所有图片的集合

关于滚轮事件
ie/chrome: onmousewheel
fireFox: DOMMousescroll // 使用addEventListener绑定,需要阻止默认事件 event.preventDefault();

ie/chrome: event.wheelDelta (上正下负)
fireFox: event.detail (上负下正)

（十九）Event对象
兼容性写法：var ev = ev || event

event对象下常见的属性
clientX,Y 鼠标相对于可视区的位置
pageX,Y 鼠标相对于文档的位置

事件流(开始接收与window对象)
  当某个元素事件被触发的时候，从捕获阶段(外到内)到冒泡阶段(内到外)的整个过程就叫事件流（事件模型）
事件冒泡(默认)
  obj.addEventListener(eventName,succ(匿名/有名),false);
  // 兼容IE8 obj.attachEvent(on + eventName,succ()); // 没有事件捕获,函数内部this指向window而不是事件对象,使用call
  阻止冒泡
    ev.cancelBubble = true;
    stopPropagetion();
事件捕获
  obj.addEventListener(eventName,succ(匿名/有名),true);
取消事件绑定
  obj.removeEventListener(eventName,succ,true/false);
  兼容IE8
    obj.detachEvent(on + eventName,succ);

键盘事件
  onkeydown,onkeyup
event对象下的常见属性
  keyCode
  ctrlKey
  shiftKey
  altKey

事件的默认行为
oncontextmenu
阻止事件的默认行为
return false;  ev.pareventDefault();

事件委托(事件源) 利用冒泡机制。把事件添加到父级上使用ev.target判断谁是事件源


###（二十）Ajax
Ajax,JSONP(跨域请求,同协议,同端口,同域名)
原生Ajax的封装
function ajax(json) {
  var settings = {
    'url':json.url||'',
    'method':json.method||'get',
    'data':json.data || {},
    'succ':json.succ || function(){},
    'type':json.type || 'json'
  };
  var ajax = new XMLHttpRequest();
  var arr = [];
  for(var attr in settings.data){
    arr.push(attr+'='+settings.data[attr]);
  };
  settings.data = arr.join('&');
  if(settings.method === 'get'){
    var w = settings.data?'?':'';
    ajax.open(settings.method,settings.url+w+settings.data+'&'+new Date());
    ajax.send();
  }else{
    ajax.open(settings.method,settings.url);
    ajax.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
    ajax.send(settings.data);
  };
  ajax.onreadystatechange = function(){
    if(ajax.readyState === 4){
      if(ajax.status >=200 && ajax.status <= 206){
         success && success(xhr.responseText);
      }
    }
  } 
}
###原生JSONP的封装
function jsonp(json){
      var oS = document.createElement('script');
      oS.className = 'os';
      var head = document.getElementsByTagName('head')[0];
      var onOff = true;
      var fnName = 'jquery_'+new Date().getTime();
      var settings = {
            url:json.url || '',
            data:json.data || {},
            callback:json.callback||'callback',
            succ:json.succ || function(){},
            fnName:json.fnName || fnName
      };
      //传给后台的字符串的cd=fn或者callback=fn
      settings.data[settings.callback] = settings.fnName;
      var arr = [];
      for(var attr in settings.data){
            arr.push(attr+'='+settings.data[attr]);
      }
      settings.data = arr.join('&');
      //声明调用的函数
      window[settings.fnName] = function(json){
            var oss = head.getElementsByClassName('os');
            oss = Array.from(oss);
            onOff = false;
            if(oss.length > 1){
                  for(var i=0;i<oss.length;i++){
                        head.removeChild(oss[i]);
                  }
            }else{
                  head.removeChild(oS);
            }
            settings.succ(json);
      }
      oS.src = settings.url + '?' + settings.data;

      head.appendChild(oS);
}
###JQuery中Ajax的使用
$.ajax({
  url: 'xxx.php',
  data: 'name=xxx&age=xxx',
  type: 'get',
  jsonp: cd //可能回调函数key不是callback是cd
  success: function(){},
  error: function(){}
})

（二十一）JQuery
1.选择器
  可以使用css选择器,也可以使用css的选择器
2.常见的方法
  $(function(){});
  html(); 
  css();
  css("background-position","-"+ value +"px -"+ value +"px");
  attr();
  prop(); 判断checked是true还是false
  filter(); 过滤
  not(); 反过滤
  has(); 包含
  next(); 下一个节点
  prev(); 上一个节点
  find(); 过滤子节点
  eq(); 一组元素的下标
  index(); 一组元素的索引
  addClass(); 添加class 
  removeClass(); 删除class
  width(); 内容宽
  innerWidth(); 内容+padding
  outerWidth(); 内容+padding+border
  outerWidth(); 内容+padding+border+margin
  insertBefore();
  inserAfter();
  append();
  prepend();
  off(); 取消事件绑定
  remove(); 删除节点
  事件绑定on obj.on({eventName1:function(){},eventName2:function(){}});
  scrollTop 滚动距离
  创建节点 $('<TagName>')
  event对象
  pageX/Y 鼠标坐标
  which keyCode
  阻止默认事件 ev.pareventDefault();
  阻止冒泡 ev.shopPropagation();
  offset().top.left //相对于文档,不是可视区
  offsetParent() 获取定位父级
  parent() 父级节点
  val() value值
  size() length
  each(function(i,el){}); //循环
  hide()隐藏
  show()显示
  fodeIn()淡入
  fodeOut()淡出
  fodeTo(m,n) //m时间 n opcity值
  get(i) 转换为原生对象
  detach() 删除节点而且保留被事件,返回被删除的节点
  parents()所有祖先节点 参数是过滤条件
  closest(条件)指定的最近的祖先节点
  siblings()所有兄弟节点
  nextAll()
  prevAll()
  slice(n,m)截取一组元素
  
运动
  animate(x,y,z,s)
  x:目标
  y：time
  z：type
  s: suss
  delay()延迟执行(只针对动画)
  stop()阻止当前运动
  stop(true)阻止后续运动
  stop(true,true)阻止当前以及后续运动,立即运动到当前目标点
  finish()直接到目标点
  
###事件委托
  父.delegate('target','eventName',function(){
   this //目标元素
  });

###工具方法
  $.type(a) 判断类型
  $.trim(str) 首尾空格
  $.proxy(suss,this,arguments) 和call类似
  $.makeArray(类数组)

ajax
$.ajax({
  url: 'xxx.php',
  data: 'name=xxx&age=xxx',
  type: 'get',
  jsonp: cd //可能回调函数key不是callback是cd
  success: function(){},
  error: function(){}
})

###$.extend({}) 扩展工具函数
###$.fn.extend({})扩展jq函数

（二十二）正则表达式
var regexp = /正则表达式/ig;
var regexp = new RegExp('正则表达式',gi) //这里是字符串需要注意转义

g 全局匹配
i 忽略大小写

常用的方法
test 
  regexp.test(string) 返回 boolean
search
  string.search(regexp) 返回位置
match
  string.match(regexp) 返回符合字符串的数组
replace(第三个参数回调用函数)
  string.replace(regexp,string2) 符合正则表达式进行替换
  string.replace(regexp,string2,function($0,$1,$2) {
    // $0 每一次匹配到的字符串
    // $1 每一次匹配到的位置
    // $2 整个字符串
    return;
  })

字符类
[abc] // a || b || c
[0-9] // 使用数字
[a-z] // 所有字母
[0-9A-Za-z] //所有数字字母
[^a] // 除了a以外的任何字符
. 任何字符

转义字符(大写是取反)
\d 所有数字
\w 所有数字字母下划线
\s 所有空白字符

量词
{n,m} n-m次
{n,} 至少n次
{,m} 最多m次
{n} n次
+1 1到任意次
* 0到任意次
? 0或一次

PS:
 符号比如 . ( ) 是需要转义的 .=>\.
 在 new RegExp()由于是字符串形式 \ 也是需要转义的 \\
 (由于是字符串形式,所以可以使用变量)

单词边界
\b
new RegExp('\\b'+className+'\\b');


var json = {
  name:'小明',
  age:18
}
var str = '今天{name}说:我今年{age}';
var s = str.replace(/\{[a-z]+\}/g,function($0){
  return json[$0.replace(/\{|\}/g,'')];
});

（二十三）面向对象
面向对象的特征：封装,继承,多态

构造函数
function Man(name,age) {
  this.name = name;
  this.age = age;
}
Man.prototype.getAge = function(){};
Man.prototype.getName = function(){};

自定义事件
  原生
    绑定：function bindEvent(obj,events,fn) {
           obj.listev = obj.listevent || {};
           obj.listev[events] = obj.listev[events] || [];
           obj.listev[events].push(fn);
           obj.addEventListener(events,fn,false);
         }
    触发：function fireEvent(obj,events) {
           for(var i=0; i<obj.listev[events].length; i++) {
             obj.listev[events][i]();  
           }
         }    
  Jquery
    绑定：obj.addEventListener(obj,'eventName',function(){});
    触发：obj.trigger(eventName);

拷贝
###1.如果对象或者数组内部没有undefind或者function完全可以使用
  obj = JSON.parse(JSON.stringify(obj));
###2.深度拷贝(for in循环,和使用toString判断数据类型)
  function extend(obj) {
    var ex = Object.prototype.toString.call(obj) == 'Array' ? []:{};
    for(var attr in obj) {
      if(typeof obj[attr] != 'Object') {
        ex[attr] = obj[attr];
      }else {
        ex[attr] = extend(obj[attr]);
      }
    }
    return ex;
  }

包装对象
给系统的普通类型添加方法可以通过 String.prototype.getLast = function(){}
str.getLast();

继承(两种)
1.
function A(name,age) {
}
function B(name,age,id) {
  A.call(this,name,age);
  this.id = id;
}
for(var attr in A.prototype) {
  B.prototype[i] = A.prototype[i];
}
2.
function B() {
  A.call(this);
}
var F = function(){};
F.prototype = A.prototype; //F的prototype和A的prototype是同址的
B.prototype = new F(); // B的prototype的指向和F的prototype的指向不一样。但是可以通过原型链找到，但是不能修改，只能在自身上修改
B.prototypre.constructor = B; // prototype.constructor是对象的构造函数


Function 与 Object的关系
Function的构造函数是自身，由于JS不是真正的面向对象所以
任何对象都是由Fucntion构成的,通过原型链找方法的时候，先找
Function下的prototype然后是Object下的prototype

toString判断对象类型
  Object.prototype.toString.call(obj); 返回结果[object Array],[object Object]...
进制的转换
  number.toString(进制);

原型链
对象下
arr.say ->  arr.__proto__ -> Array.prototype -> Array.prototype.__proto__   ->  Object.prototype  -> obj
构造函数下
Array.say -> Array.__proto__ -> Function.prototype
原型链的查找，是从最内侧向外查找，实例与原型的连接，可以通过引用的传递，连接的更远，

（二十四）HTML5


（二十五）CSS3
1.选择器
CSS选择器
el [key] 包含key这个属性的元素
el [key=val] 包含key这个属性且等于val的
el [key|=val] 包含key且属性值等于val 或者以 val开头
el [key~=val] 多个值（空格分隔）拥有val属性的
el [key$=val] 以val结尾的
el [key^=val] 以val开头的
el [key*=val] 包含val的
结构选择器
E>F：E的所有子元素F
E~F：E后面的所有兄弟元素F
E+F：E后面的第一个兄弟元素F

（二十六）HTML,CSS


###（二十七）cookie
格式
  document.cookit = 'key1=encodeURI(val1); key2=encodeURI(val2); expires=' + oData.toGMTString();  //toGMTString字符串化日期
函数的封装
  function setCookie(key, val, time) {
    var oDate = new Date();
    oDate.setDate = oDate.getDate + time;
    document.cookie = encodeURI(key) + '=' + val + '; ' + 'expire =' + oDate.toGMTString();
  }
  
  function getCookie(key) {
    var arr = document.cookie.split('; ');
    for(var i=0; i<arr.length; i++) {
      var arr2 = arr[i].split('=');
      for(var j=0; j<arr2.length; j++) {
        if(arr2[0] === key) {
          return decodeURI(arr2[1]);
        }
      }
    }
  }

  function removeCookie(key) {
    setCookit(key,'',-1); //设置过期时间
  } 

（二十八）Vue开发遇到的问题


（二十九）原生移动端
1.meta标签设置
    <!-- 适口适配 -->
    <meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
    <!-- IOS全屏浏览 -->
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <!-- 禁止百度转码显示 -->
    <meta http-equiv="Cache-Control" content="no-siteapp">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">
2.不使用fixed模拟固定定位,使用position:absolute模拟,html,body height:100% width:100%
3.像素比设置
  function setSize() {
    var html = document.getElementsByTagName('html')[0];
    var viewWidth = document.documentElement.clientWidth;
    html.style.fontSize = viewWidth / 16 + 'px';
  }

4.移动端事件以及event对象下常见的属性
    touchstart
    touchmove
    touchend
    orientationchange 
    event.changeTouches[0] 对象下 pageX,pageY 是手指的坐标

5.移动端默认样式
a,
input,
button {
  -webkit-text-size-adjust: 100%; //横竖屏字体
  -webkit-tap-highlight-color: rgba(0,0,0,0); //a标签的遮罩
  -webkit-appearance: none;  //表单的圆角
}

6.移动端系统菜单问题
doucment.addEventListener('touchstar',function(ev){
  ev.preventDefault();
})   

7.rem布局借助scss,$变量的使用

（三十）CSS预处理器 SCSS
混合宏 @mixin name($arguments:val){}声明  @include name(arguments);调用

继承 @extent .btn{}声明  .btn-abc{@extent .bth};使用

占位符 %mt5{}声明  @extent %mt5;使用 

（三十一）常用的数学方法
Math.abs() 绝对值
Math.ceil() 向上取整
Math.floor() 向下取整
Math.round() 四舍五入
Math.random() 随机数
Math.max() //一组数据中最大的 Math.max.apply(null,arr);
Math.sqrt() 开根号
Math.pow(x,y) x的y次幂
Math.PI PI

x-y
Math.round(Math.random()*(y-x) + x);

（三十三）better-scroll 与 Vue，常用的移动端插件


（三十四）闭包
函数嵌套函数,外层函数的变量内部函数可以使用,不会受到JS的垃圾回收机制的影响，会常驻在内存里 // 内层函数使用了外层函数的局部变量,可以一直使用,不会因为外层函数执行结束后,被垃圾回收机制清理

var test = (function()
  var a = 1; //变量a长驻在内存里
  return function() {
    a++;
    alert(a);
  }
)();

test() // 2
test() // 3

####成员变量私有化
var test = (function(){
  function aaa() {
  };
  function bbb() {
  };
  return {
    a: aaa,
    b: bbb
  }
})();
aaa与bbb函数只属于test

循环中使用闭包 
for(var i=0; i<test.length; i++) {
  (function(i){  //参数局部变量i接收i
    test[i].onclick = function() {
      console.log(i)  //注意本质上创建了test.length个函数,和var i
    };
  })(i);  //传入的for中i
}

（三十五）常用ESMAScript6
let 声明块级作用域变量
const 声明常量
解构赋值
 数组的解构赋值 var [a,b,c] = [1,2,3];
 对象的解构赋值 var {a,b,c} = {a:1,b:2,c:3};
箭头函数 () => {}
面向对象的语法糖
class Man {
  //构造函数
  constructor(name) {
    this.name = name;
  }
  getName() {
  }
} 
继承
class Cat extends Man {
 constructor(name,age) {
   super(name);
   this.age = age;
 }
 //继承新的方法,但是可以重写
 super.getName() {
 }
 getAge(){
 }
}

（三十六）学习Vue过程中遇到移动端常见的小技巧，以及移动端知识


（三十七）display: flex
1.兼容性：webkit内核需要添加 -webkit-flex 前缀

主轴方向和交叉轴方向不是固定的,如果x轴是交叉轴，y就是主轴，反之同理

flex的属性（父级的属性）
flex-direction //设置主轴的方向  row,row-reverse,column,colume-reverse
flex-wrap // 是否换行 nowrap wrap wrap=reverse
flex-flow  // flex-direction 和 flex-wrap的简写（属性值用空格分开）
justify-content //主轴对齐方式 flex-start右对齐 flex-end右对齐 center中间对齐 space-between两侧对齐空隙平分 space-around空隙全部平分
align-items //交叉轴对齐方式 flex-start起点对齐 flex-end 终点对齐 center中点对齐 baseline第一行文字基地点对齐
align-content //多根轴线对齐方式（多跟轴线才有效果）
// flex-start交叉轴起点 flex-end交叉轴终点 center交叉轴中点 space-between两端对齐,中间平分 space-around平均分配间隔


order //排列顺序 越小越靠左越小越靠上
flex-grow // 放大的比例,如果平分三分，flex-grow是2，放大一倍，别的缩小一倍 默认为0不放大 全部设置为1等分剩余的空间
flex-shrink //缩小比例.如果设置为0,别的项目缩小的时候，不进行缩小 默认为1自动缩小
flex-basis //设置空间大小（300px...）
flex //flex-grow flex-shrink flex-basis的缩写 默认 0,1，auto（最后两个可选）  flex：1如果父级有滚动条失效
两列布局
1列固定宽度，一列自适应
flex：0 0 100px;
flex: 1 
align-self // 允许单个子项与其他项目不一样的对齐方式可以覆盖 align-items对齐的方式


关于HTML,BODY
html 100% body 100% wrap 100%  -- OK
html 100vh body 100vh wrap 100vh  -- OK
html min 100vh body min 100vh wrap 100vh  -- OK
html min 100% body min 100% wrap min 100vh  -- OK
html min 100% body min 100% wrap min 100vh  -- OK

html min 100vh body min 100% wrap min 100%  -- no
