### BOM
> Javascript包含
    
* 1 、ECMASscript:定义了语言的数据类型、语法、内置对象
* 2、 DOM : Document Object Model 文档对象模型 文档对象模型
* 3、 BOM ： Browser Object Model 浏览器对象模型
    * 对象模型：
      * 文档
      * 浏览器
    * 把文档（浏览器）转换成对象
    * 定义了语言操作文档这种结构数据应该提供的一些方法
* Net
    *  XMLHttpRequest & Fetch
* 图形图像
    * Canvas、SVG、WebGL
* 音频视频
    * Auio、Video
* 文件
    * FileReader
* 本地数据类型
    *  Cookie、Storage、WebSQL、IndexDB
    
——————
>  Node.JS
*  ECMAScript
*  DOM
*  Net
*  File
*  System
*  DataBase
*  ...
---
### 学习BOM学什么
* window
    * screen : 屏幕
    * navigator : 浏览器内核
    * history : 历史记录
    * location : 地址地位
    * document : 文档
*   我们将学到与浏览器窗口交互的一些对象，例如可以移动、调整浏览器大小的window对象，可以用于导航的location对象与history对象，可以获取浏览器、操作系统与用户屏幕信息的navigator与screen对象，可以使用document作为访问HTML文档的入口，管理框架的frames对象等。在这里，只介绍一些window对象等的基础知识，其中会有一些ECMAscript的知识还会说明。其他对象Location、Screen、Navigator、History不详细介绍
*  ![image](http://hi.csdn.net/attachment/201112/6/0_1323158503Bo6d.gif)
---
### 1window详解
> 是什么？==对象==：
* 每一个页面（窗口）都有一个独立的window对象，这个对象是所有其他（BOM\DOM）对象的最顶层对象
*  window对象：BOM的核心对象是window，它表示浏览器的一个实例。在浏览器中，window对象有双重角色，它既是通过javascript访问浏览器窗口的一个接口，又是ECMAScript规定的Global对象。
```
<script type="text/javascript">
  var age=26;//这里定义的全局变量和全局函数被自动归在了window对象名下
  function sayAge(){
    console.log(this.age);
  }
  console.log(window.age);//26
  sayAge();//26 相当于window.sayAge()
  window.sayAge();//26
 
  //全局变量和在window对象上直接定义属性的唯一区别：全局变量不能够通过delete操作符删除，而直接在window对象上定义的属性可以
  window.color='red';
  delete window.age;
  delete window.color;
  console.log(window.age);//26
  console.log(window.color);//undefined
  </script>
```

> 注意：
* ECMA中是没有window对象的，==window是DOM\BOM中的顶层对象==，其他所有的对象都是在window对象之下

```
<script type="text/javascript">
    /*
    还要注意：尝试访问未声明的变量会抛出错误，但是通过查询window对象，可以知道某个可能未经声明的变量是否存在
     */
    //这会抛出错误，因为oldValue未定义
    var newValue=oldValue;
    //这不会抛出错误，因为是一次属性查询
    var newValue=window.oldValue;
  </script>
```

* ECMAScript顶层对象是：global，这个对象在js中是被禁止访问的，浏览器基于该对象进行了扩展，扩展出来了一个window对象
> Window对象关系属性
* parent：如果当前窗口为frame，指向包含该frame的窗口的frame （frame）
* self ：指向当前的window对象，与window同意。 （window对象）
* top ：如果当前窗口为frame，指向包含该frame的top-level的window对象
* window ：指向当前的window对象，与self同意。
* opener ：当窗口是用javascript打开时，指向打开它的那人窗口（开启者）
> Window对象定位属性
* IE提供了window.screenLeft和window.screenTop对象来判断窗口的位置，但未提供任何判断窗口大小的方法。
* 用document.body.offsetWidth和document.body. offsetHeight属性可以获取视口的大小（显示HTML页的区域），但它们不是标准属性。
* Mozilla提供window.screenX和window.screenY属性判断窗口的位置。
* 它还提供了window.innerWidth和window.innerHeight属性来判断视口的大小
* window.outerWidth和window.outerHeight属性判断浏览器窗口自身的大小。
---
### window对象的方法
##### 窗体控制
>  moveBy(x,y)——从当前位置水平移动窗体x个像素，垂直移动窗体y个像素，x为负数，将向左移动窗体，y为负数，将向上移动窗体

> moveTo(x,y)——移动窗体左上角到相对于屏幕左上角的(x,y)点，当使用负数做为参数时会吧窗体移出屏幕的可视区域
>  resizeBy(w,h)——相对窗体当前的大小，宽度调整w个像素，高度调整h个像素。如果参数为负值，将缩小窗体，反之扩大窗体

>  resizeTo(w,h)——把窗体宽度调整为w个像素，高度调整为h个像素窗体滚动轴控制

>  scrollTo(x,y)——在窗体中如果有滚动条，将横向滚动条移动到相对于窗体宽度为x个像素的位置，将纵向滚动条移动到相对于窗体高度为y个像素的位置

>  scrollBy(x,y)—— 如果有滚动条，将横向滚动条移动到相对于当前横向滚动条的x个像素的位置(就是向左移动x像素)，将纵向滚动条移动到相对于当前纵向滚动条高度为y个像素的位置(就是向下移动y像素)窗体焦点控制

>    focus()—— 使窗体或控件获取焦点blur()——与focus函数相反，使窗体或控件失去焦点新建窗体

>    open()--通过open方法打开一个新的窗口，返回被打开的新窗口的window对象，默认为空白页：about:blank

```
  window.open(strUrl, target, [strWindowFeatures]);
  newWindow = window.open('a.html', '_blank','menubar=no,location=no,resizable=no,scrollbars=no,status=no');
  window.open('a.html', '_self');
  window.open('a.html', 'miaov');
  window.open('a.html');
  window.open();
```
*   open方法参数说明
    * strUrl：url,
    * target：新窗口的打开方式，类似a的target属性，默认新窗口：_blank
        *   _blank新窗口
        *   _self自己
        *  _parent上一级
        *   _top最顶层
        *   [frame_name]
    * strWindowFeatures：新窗口的特征，该配置不是所有浏览器都支持，有的浏览器需要修改配置才能使用 about:config
* 该方法会返回新窗口的window对象
- ==注意==：如果新窗口的url地址的域和当前页面的域不一样，那么是不能修改的

* 新窗口特征
    * height       	Number	设置窗体的高度，不能小于100
    * left	        Number	说明创建窗体的左坐标，不能为负值
    * location  	Boolean	窗体是否显示地址栏，默认值为no
    * resizable	    Boolean	窗体是否允许通过拖动边线调整大小，默认值为no
    * scrollbars	Boolean	窗体中内部超出窗口可视范围时是否允许拖动，默认值为no
    * toolbar   	Boolean	窗体是否显示工具栏，默认值为no
    * top       	Number	说明创建窗体的上坐标，不能为负值
    * status    	Boolean	窗体是否显示状态栏，默认值为no
    * width	        Number	创建窗体的宽度，不能小于100


> 关闭

*   close()——关闭窗体opener属性——新建窗体中对父窗体的引用，中文"开启者"的意思
*   newWindow.close();
*   不能关闭由非js打开的窗口（因为每个网站的域名不一样）

#### 对话框

> alert(str)—— 弹出消息对话框（对话框中有一个“确定”按钮）

> confirm(str)—— 弹出消息对话框（对话框中包含一个“确定”按钮与“取消”按钮）

> prompt(str,defaultValue)——弹出消息对话框（对话框中包含一个“确定”按钮、“取消”按钮与一个文本输入框），由于各个浏览器实现的不同，若没有第二个参数（文本框中的默认值）时也最好提供一个空字符串

### 状态栏
> window.defaultStatus 属性——改变浏览器状态栏的默认显示(当状态栏没有其它显示时)，浏览器底部的区域称为状态栏，用于向用户显示信息
window.status 属性——临时改变浏览器状态栏的显示

### JavaScript浏览器对象（BOM）中有关设备、浏览器屏幕高度和宽度的API介绍
> 一、设备的分辨率

```
window.screen.width × window.screen.height
```
* 台式机：1440 × 900 / 手机：360 × 640
> 二、浏览器的分辨率


```
window.screen.availWidth × window.screen.availHeight
```

* 台式机Chrome：1440 × 860 / 手机：360 × 640
* 设备和在设备上安装的浏览器只要不更改，它们的分辨率保持不变

在台式机设备中，浏览器分辨率的高度 = 设备分辨率的高度 - 40px；设备分辨率的宽度包含了滚动条宽度
> 三、窗口视口（能看到的网页区域）的宽高 ==常用到设置遮罩层==

```
window.innerWidth × window.innerHeight
```

 
* 台式机Chrome：1440 × 797 / 手机：360 × 518

 

* window.innerWidth在台式机设备中，包含滚动条宽度；window.innerHeight会随菜单和书签栏的隐藏、显示发生改变

* IE8不支持这两个属性

* 可以把这两个属性作为响应式布局的依据（在移动设备上无滚动条）
* ==BOM==中的的  
    *   client：可视区宽高，元素的inner，client = width/height + padding
         - clientWidth
        - clientHeight
    - offset：占位宽高，offset = width/height + padding + border
         - offsetWidth
        - offsetHeight
     - scroll：滚动内容宽高
         - scrollWidth
         - scrollHeight
---
> ==scrollTop/scrollLeft==不属于Window其他元素也有scrollTop/scrollLeft
* 当这个属性是html或者body的时候，是浏览器可视区 到 页面顶部的距离
* 滚动的是文档，所以scrollTop和scrollLeft是元素的不是窗口的
* ==document对象不是html这个元素:html => document.documentElement==
*  ==兼容==:
         console.log( document.documentElement.scrollTop || document.body.scrollTop );
* scrollTop和scrollLeft的值是==可读可写==的

```
document.documentElement.scrollTop = document.body.scrollTop = 1000;
```

* scrollX / scrollY
    *   后期增加的，低版本浏览器不支持，只读
    *   设置使用：scrollTo(x, y)
#### window事件
* window.onload
    *   当浏览器资源加载完成的时候触发
    *   资源：html，css，image等资源
    
```
window.onload = function() {
    console.log('加载完成了')
    }
```
* window.onresize事件
    *   当窗口的大小发生改变的时候触发

```
  var mask = document.querySelector('.mask');

        window.onresize = function() {
            //console.log('resize');
        }
```
* onscroll
    *   当窗口滚动条滚动的时候触发

```
window.onscroll = function() {
//            console.log(window.scrollY)
            mask.style.top = window.scrollY + 'px';
        }
        例子：
        
         var left = document.querySelector('.left');
        var right = document.querySelector('.right');

        var L = -100;
        var R = -100;
        var H = 100;

        window.onscroll = function() {

            if (L + window.scrollY < document.documentElement.clientWidth / 2) {
                left.style.left = L + window.scrollY + 'px';
                right.style.right = R + window.scrollY + 'px';
            } else {
                left.style.left = document.documentElement.clientWidth / 2 + 'px';
                right.style.right = document.documentElement.clientWidth / 2 + 'px';

                left.style.height = right.style.height = left.offsetHeight + 1 + 'px';
            }



        }
```
---
## 2、navigator浏览器
> Navigator 对象的属性

```
 * navigator.userAgent
    *   用户代理信息
    console.log(navigator.userAgent);
Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.132 Safari/537.36
```

* appCodeName 返回浏览器的代码名
* appName 返回浏览器的名称
* appVersion 返回浏览器的平台和版本信息
* browserLanguage 返回当前浏览器的语言
* cookieEnabled 返回指明浏览器中是否启用 cookie 的布尔值
* cpuClass 返回浏览器系统的 CPU 等级
* onLine 返回指明系统是否处于脱机模式的布尔值
* platform 返回运行浏览器的操作系统平台
* systemLanguage 返回 OS 使用的默认语言
* userAgent 返回由客户机发送服务器的 user-agent 头部的值
* userLanguage 返回 OS 的自然语言设置
## 3、History对象,在浏览器历史记录中导航
> History 对象的属性:length 返回浏览器历史列表中的 URL 数量

> History 对象的方法

* back() 加载 history 列表中的前一个 URL
* forward() 加载 history 列表中的下一个 URL
* go(num) 加载 history 列表中的某个具体页面

```
创建了一个新的由 state, title, 和 url设定的浏览器历史纪录.
 var button = document.querySelector('button');

    button.onclick = function() {
        var state = { 'page_id': 1, 'user_id': 5 };
        var title = 'Hello World';
        var url = '10.history-3.html';

        history.pushState(state, title, url);
    }
```
## location
> 地址定位、当前页面的URL信息
* 在js中提供了一个location对象，这个对象就是当前地址的详细信息
> URI Uniform Resource Identifier
   
* 统一资源标识符
    *  统一资源 : 在网络中进行传播的数据，包括HTML文档、图像、视频片段、程序等
    *  URL 
    *  URN
> URL  Uniform Resource Locator
    
*  统一资源定位符
*  基本URL包含模式（或称协议）、服务器名称（或IP地址）、路径和文件名：http://www.miaov.com/a/1.html
*   协议://用户名:密码@子域名.域名.顶级域名:端口号/目录/文件名.文件后缀?参数=值#标志 http://zmouse:123@video.miaov.com:8888/a/b/1.html?a=1#p1
> URN Uniform Resource Name
* 统一资源名称
--- 
#### 方法属性
>  location.href
* location中的完整url
    * 这个属性是可读可写的
    * 读：当前页面的url
    * 写：改变当前浏览器的url
> location.reload()
* reload：重载，重新加载当前页面，刷新

```
 document.onclick = function() {
            location.reload();

            // 还有另外一个中刷新的方式
            // location.href = location.href;
        }
```
> location.search
* 是什么
    * url中queryString的部分
    * queryString:查询字符串，是url中?后面的部分
* 注意：
    *  当search发生改变以后，虽然文件定位不变，但是会重新发送请求（刷新跳转）
    *  因为search的变化会重新发送请求，所有通常search作为请求的数据传递给后端使用
>  location.hash
*  url中#后面的部分
* hash的值变化不会发送请求，我们的页面代码不会重新执行
*  我希望hash变化的时候能够重新执行某些代码，这个时候，就需要用到 事件
        