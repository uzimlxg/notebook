## jQuery
> jQuery foundation : jQuery基金会，旗下有很多的一些开源产品
- Sizzle<jQuery选择器引擎模块>
    > Sizzle来源于jQuery，并且jQuery是一个基于DOM操作的类库
    
    > 实现了css选择器的一个元素选择的库,[地址](https://sizzlejs.com/)
    
    > 特点
        * 快（从右到左查找）————> 而传统的选择器是从左到右进行查找的
        
    > Sizzle的实现
       
     * 1，首先调用Sizzle(selector, context)方法
     *  2， 调用select(selector, context, results, seed) 方法
     * 3 , 调用 compile 方法
     * 4，matcher方法
- Mocha <单元测试>
    * 安装 （npm i mocha -g）
    * 测试脚本案例
        * 写出需要测试的脚本
        ```
        // add.js
        function add(x, y) {
          return x + y;
        }
        
        module.exports = add;
        ```
        * 测试脚本
            * 注意事项<通常，测试脚本与所要测试的源码脚本同名，但是后缀名为.test.js（表示测试）或者.spec.js（表示规格）。比如，add.js的测试脚本名字就是add.test.js。>
        ```
        // add.test.js
        var add = require('./add.js');
        var expect = require('chai').expect;
        
        describe('加法函数的测试', function() {
          it('1 加 1 应该等于 2', function() {
            expect(add(1, 1)).to.be.equal(2);
          });
         });
         ```
        * 上面这段代码，就是测试脚本，它可以独立执行。测试脚本里面应该包括一个或多个describe块，每个describe块应该包括一个或多个it块。
        * describe块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数。
        * it块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"1 加 1 应该等于 2"），第二个参数是一个实际执行的函数。
        
- Lodash [工具库](https://lodash.com)
    *  对原生的一些操作做了优化与扩展（Array，Date等内置对象数据操作），并实现了模块化
    *  内部封装了诸多对字符串、数组、对象等常见数据类型的处理函数
- ESLint语法检测工具
    * 全局安装 npm install -g eslint
    * 初始化————————> eslint --init
    
#### jQuery是什么？
> jQuery 是一个高效、精简并且功能丰富的 JavaScript 工具库.它提供的 API 易于使用且兼容众多浏览器，这让诸如 HTML 文档遍历和操作、事件处理、动画和 Ajax 操作更加简单。
#### jQuery语法
> 基础语法格式是：$(selector).action()
* $符号定义 ：代表jQuery对象，也可以直接用jQuery,如：jQuery(selector).action()
* 选择符（selector）：“查询”和“查找” HTML 元素，比如，id为btn1的<button>元素
* jQuery 的 action() ：执行对元素的操作,比如控件的隐藏与显示等
> 注意
* jQuery的符号代表$,因为在别的地方可能也同样用到$，这时如果与jQuery碰到一起，就产生了冲突。
* 因此在设计的时候，jQuery为此创建了一个方法。在文档加载完成前，调用jQuery.noConflict(),我们也可以为此定义一个jQuery的全局变量。

```
var jq = jQuery.noConflict();
```
#### 1 、入口函数
> jQuery入口函数与js入口函数的区别：

* jQuery的入口函数是在 html所有标签都加载之后，就会去执行。

* Js的window.onload事件是等到所有内容，包括外部图片之类的文件加载完后，才会执行

```
 $(document).ready(function(){});

 $(function(){});
```

#### 2、选择器
> 基本选择器

符号 | 说明 | 用法 
---|---|---
$(“#demo”) | id选择器 | $(“#demo”).css(“background”,”red”)
$(“.liItem”) | 类选择器 | $(“.liItem”). css(“background”,”red”);
$(“div”)|标签选择器|$(“div”). css(“background”,”red”);
$(“*”)|通配符选择器|$(“*”). css(“background”,”red”)
$(“.liItem,div”)|并集选择器|$(“.liItem,div”). css(“background”,”red”)

> 层级选择器

符号 | 说明 | 用法
---|--- | ---
空格 | 后代选择器选择所有的后代元素 | $(“div span”). css(“background”,”red”);
> |子代选择器选择所有的子代元素 | $(“div > span”). css(“background”,”red”)
+ |紧邻选择器选择紧挨着的下一个元素 | $(“div + p”). css(“background”,”red”)
~ | 兄弟选择器选择后面的所有的兄弟元素| $(“div ~ p”). css(“background”,”red”)

> 过滤选择器

符号 | 说明 | 用法
---|---|---
:eq(index) | index是从0开始的一个数字，选择序号为index的元素。选择第一个匹配的元素。 | $(“li:eq(1)”). css(“background”,”red”)
:gt(index) | 选择序号大于index的元素 |$(“li:gt(2)”). css(“background”,”red”)
:lt(index)|选择小于index 的元素|$(“li:lt(2)”). css(“background”,”red”)
:odd|选择所有序号为奇数行的元素|$(“li:odd”). css(“background”,”red”)
:even|选择所有序号为偶数的元素|$(“li:even”). css(“background”,”red”)
:first|选择匹配第一个元素|$(“li:first”). css(“background”,”red”)
:last|选择匹配的最后一个元素|$(“li:last”). css(“background”,”red”)
> 属性选择器

符号 | 说明 | 用法
---|---|---
$(“a[href]”) | 选择所有包含href属性的元素 | $(“a[href]”). css(“background”,”red”)
$(“a[href=’itcast’]”)|选择href属性值为itcast的所有a标签 | $(“a[href=’itcast’]”). css(“background”,”red”)
$(“a[href!=’baidu’]”)|选择所有href属性不等baidu的所有元素，包括没有href的元素|$(“a[href!=’baidu’]”). css(“background”,”red”)
$(“a[href^=’web’]”)|选择所有以web开头的元素|$(“a[href^=’web’]”). css(“background”,”red”)
$(“a[href$=’cn’]”)|选择所有以cn结尾的元素|$(“a[href$=’cn’]”). css(“background”,”red”)
$(“a[href*=’i’]”)|选择所有包含i这个字符的元素，可以是中英文|$(“a[href*=’i’]”). css(“background”,”red”)
$(“a[href][title=’我’]”)|选择所有符合指定属性规则的元素，都符合才会被选中|$(“a[href][title=’我’]”). css(“background”,”red”)
> 筛选选择器

符号 | 说明 | 用法
---|--- | ---
.eq(index) | index是从0开始的一个数字，选择序号为index的元素。 | $(“li”).eq(1). css(“background”,”red”)
.first( ) | 选择匹配第一个元素 |$(“li”).first(). css(“background”,”red”)
.last( )|选择匹配的最后一个元素|$(“li”).last(). css(“background”,”red”)
.parent( )|选择父亲元素|$(“li”).parent(). css(“background”,”red”)
.siblings( )|选择所有的亲兄弟元素，不包括自己|$(“li”).sibling(). css(“background”,”red”)
.find( )|查找所有的后代元素|$(“li”).find(). css(“background”,”red”)
.prevAll()|选择这个元素之前的所有亲兄弟元素|…
.nextAll()|选择这个元素之后的所有亲兄弟元素|…
#### 3、动画
> 显示与隐藏

```
1          $(selector).show(speed,callback);

2          $(selector).hide(speed,callback);

3          $(selector).toggle(speed,callback);
```
* speed：隐藏/显示的速度，可以取以下值："slow"、"fast" 或毫秒

* callback：隐藏或显示完成后所执行的函数
> 滑动

```
1          $(selector).slideDown(speed,callback);

2          $(selector).slideUp(speed,callback);

3          $(selector).slideToggle(speed,callback);
```
> 淡入淡出

```
1          $(selector).fadeIn(speed,callback);

2          $(selector).fadeOut(speed,callback);

3          $(selector).fadeToggle(speed,callback);

4          $(selector).fadeTo(speed,opacity,callback);
```
* opacity：必选参数，将淡入淡出效果设置为给定的不透明度
> 自定义动画

```
1          $(selector).animate({params},speed,callback);
           $('button').on('click', function(){
                    $('div').animate({
                        left: 200
                    }, {
                        easing: 'easeOutBack',
                        complete: function() {
                            console.log('ok')
                        }
                    });
                })
```
* 必需的 params 参数定义形成动画的 CSS 属性。

* 可选的 speed 参数规定效果的时长。它可以取以下值："slow"、"fast" 或毫秒。

* 可选的 callback 参数是动画完成后所执行的函数名称。

* 操作多个属性
> 停止动画

```
1          $(selector).stop(stopAll,goToEnd);
```
* 可选的 stopAll 参数规定是否应该清除动画队列。默认是 false。

* 可选的 goToEnd 参数规定是否立即完成当前动画。默认是 false。

* stop(true)              所有动画不执行

* stop(false,true)       动画立即执行完毕，这种用法使用较多

#### 5、html
> 操作DOM
* text() - 设置或获取所选元素的文本内容

* html() - 设置或获取所选元素的内容（包括 HTML 标记）

* val() - 设置或获取表单字段的值

* attr()- 设置或获取属性的值

   * 有一个参数就是设置，没有参数就是获取！

* removeAttr ()- 移除属性

#### 6、操作样式
> 操作样式
* addClass()             给指定的元素添加样式类名

* removeClass()        给指定的元素移除样式类名

* toggleClass ()         给指定的元素切换样式类名

* hasClass ()             判断是否有样式类名

 * attribute & property
    * attribute : 标签上的，html
    * property : 对象上的，js
* checked
    *   attribute : 标签上的checked属性
    *   property : js对象上的属性
* 在jq中attr操作的attribute，prop操作的是js中的对象

> 操作元素
* 1.在内部添加

    * $(“div”).append(node)          // 在div内部元素的结尾追加元素node

    * node.appendTo(“div”)           // 把node追加到div内部元素的结尾

    * $(“div”).prepend(node)         // 在div内部元素的开头追加元素node

    * node.prependTo(“div”)         // 把node追加到div内部元素的开头

* 2.在外部添加

    * $(“div”).before(node)           // 在div后面添加兄弟节点node

    * $(“div”).after(node)              // 在div前面添加兄弟节点node

* 3.删除

    * remove() - 删除被选元素及其子元素（自杀）

    * empty() - 删除被选元素的子元素，不包括被选元素！

    * 删除被选元素的子元素用html(“”)更加高效！

* 4.复制

    * clone()- 如果加参数true就是深层复制，会把之前绑定的事件也给复制

    * replaceWith()-替换节点

> 尺寸
* 1.宽度和高度

    * width()

    * height()

    * innerWidth()

    * innerHeight()

    * outerWidth()

    * outerHeight()

    * .height()方法和.css(“height”)的区别：
        * 返回值不同：.height()方法返回的是数字类型(20)；
    * .css(“height”)返回的是字符串类型(20px)

* 2.坐标值

    * offset()           //获取和设置元素在当前窗口的相对偏移，返回的是一个对象，设置值后自动变成相对定位       Object {top: 50, left:8}

    * position()       //只能获取元素相对于父亲的偏移，返回的是一个对象，不能设置值

    * 获取值：offset().left     offset().top     position() .left        position() .top

    * 设置值：$("p").offset({left:txtLeft,top:txtTop});

    * 区别：

    * 使用position()方法时事实上是把该元素当绝对定位来处理，获取的是该元素相当于最近的一个拥有绝对或者相对定位的父元素的偏移位置。使用position()方法时如果其所有的父元素都为默认定位（static）方式，则其处理方式和offset()一样，是当前窗口的相对偏移。

    * 使用offset()方法不管该元素如何定位，也不管其父元素如何定位，都是获取的该元素相对于当前视口的偏移。

* 3.滚动条

    * scrollTop()     //获取或者设置垂直方向上到页面顶端的距离

    * scrollLeft()     // 获取或者设置水平方向上到页面左端的距离

    * scroll()           // 触发滚动事件：$(selector).scroll(function(){…});       

##### 事件绑定机制
> bind
* 语法格式：.bind( eventType, [ eventData ], handler )

    参数说明
    
    第一个参数：事件类型
    
    第二个参数：传递给事件响应方法的数据对象，可以省略。
    
    事件响应方法中获取数据方式：e.data
    
    第三个参数：事件响应方法  

```
1  $("p").bind("click",function(e){

2        //事件响应方法

3     });
```
> one方式
* 语法格式：one( events [, data ], handler )

* 只绑定一次事件
> delegate方式
* 语法格式：$(selector).delegate( selector, eventType, handler )

    语法说明：
    
    第一个参数:selector， 子选择器
    
    第二个参数：事件类型
    
    第三个参数：事件响应方法 

```
1          $(".parentBox").delegate("p","click", function(){

2             //为 .parentBox下面的所有的p标签绑定事件

3          });
```
> on方式<统一所有事件处理方法>

* 语法格式：$(selector).on( events, [ selector ],[ data ], handler )

    参数介绍：
    
    第一个参数：events，事件名
    
    第二个参数：selector,类似delegate
    
    第三个参数: 传递给事件响应方法的参数
    
    第四个参数：handler，事件处理方法
* 注意事项
    * jq事件函数中的this : 触发该事件的原生Element对象
    
    ```
     $('li').on('click', function() {
                 console.log(this);
             });
    ```
    * $p.css = 'abc';
        * //尽量避免直接给jq对象添加自定义的属性和方法，jq为我们提供了一个专门用户存储自定义数据的方式 .data()
        *  $p.data('css', 'abc');
    * $p.remove(); //同时移除事件和数据
        * $p.detach();

```
1          //绑定一个方法

2          $( "#dataTable tbodytr" ).on( "click", function() {

3             console.log( $( this ).text() );

4          });

5           

6          //给子元素绑定事件

7          $( "#dataTable tbody").on( "click", "tr", function() {

8            console.log( $( this ).text() );

9          });

10       

11      //绑定多个事件的方式

12      $( "div.test" ).on({

13         click: function() {

14           $( this ).toggleClass( "active");

15         },

16      mouseenter: function() {

17           $( this ).addClass( "inside" );

18         },

19      mouseleave: function() {

20           $( this ).removeClass( "inside");

21          }

22       });
```
> 解绑事件
* unbind解绑 bind方式绑定的事件( 在jQuery1.7以上被 on和off代替)
    * $(selector).unbind(); //解绑所有的事件
    * $(selector).unbind("click"); //解绑指定的事件
* undelegate解绑delegate事件
    * $( "p" ).undelegate(); //解绑所有的delegate事件
    * $( "p" ).undelegate( "click" ); //解绑所有的click事件
* off解绑on方式绑定的事件
    * $( "p" ).off();
    * $( "p" ).off( "click", "**" ); // 解绑所有的click事件，两个*表示所有
    * $( "body" ).off( "click", "p", foo );


```
1              案例1：

2              var foo = function() {

3                // Code to handle some kind of event

4              };

5           

6              // ... Now foo will be called whenparagraphs are clicked ...

7              $( "body" ).on("click", "p", foo );

8           

9              // ... Foo will no longer be called.

10          $( "body" ).off("click", "p", foo );

11       

12          案例2：（了解）解绑命名空间的方式：

13          var validate = function() {

14            // Code to validate form entries

15          };

16       

17          // Delegate events under the".validator" namespace

18          $( "form" ).on("click.validator", "button", validate );

19       

20          $( "form" ).on("keypress.validator", "input[type='text']", validate );

21       

22          // Remove event handlers in the".validator" namespace

23          $( "form" ).off( ".validator");
```

> 触发事件

* 简单事件触发：$(selector).click();//触发 click事件

* trigger方法触发事件：$( "#foo" ).trigger( "click" );

* triggerHandler触发事件响应方法，不触发浏览器行为：$("input" ).triggerHandler( "focus" );


> event对象的简介
 *   jq中的事件对象其实是jq封装的一个对象，但是该对象下有一个属性：originalEvent，保存了原生的原生对象
        *   在jq的事件函数中return false被jq处理过了，return false 既可以阻止默认行为还可以阻止冒泡
* event.data              //传递的额外事件响应方法的额外参数

* event.currentTarget      //在事件响应方法中等同于this，当前Dom对象

* event.target             //事件触发源，不一定===this

* event.pageX        

* event.pageY

* event.stopPropagation() //阻止事件冒泡

* e.preventDefault();        //阻止默认行为

* event.type             //事件类型：click，dbclick...

* event.which           //鼠标的按键类型：左1 中2 右3





















































