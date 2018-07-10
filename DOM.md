###DOM
> 文档对象模型
* 通过操作对象来操作文档
*  该模型下提供了很多关于文档操作的方法
* 把文档这种的结构转成对象这种结构，文档中每个标签就类似对象中的每个属性
* 这种结构有一个名词：树 tree

```
# DOM
> Document Object Model，操作
> CURD

# 得到一个DOM对象

- 创建
    - createElement()
    - createTextNode()
- 获取
    - getElementById()
    - getElementsByTagName()
    - getElementsByClassName()
    - querySelector()
    - querySelectorAll()
    - firstChild
    - lastChild
    - childNodes
    - previousSibling
    - nextSibling
    - parentNode
- 克隆
    - cloneNode()

# 操作DOM对象

- 获取对象中信息
    - 属性
        - nodeType
        - nodeValue
        - nodeName
    - 样式
        - style
        - offsetLeft
        - offsetWidth
    - 内容
        - innerHTML
```
> 树结构中的每个数据称为：节点Node-元素
* 节点与节点之间存在各种关系
    * 父子关系
    * 兄弟关系
    * 子父关系
> 节点除了有关系，还有类型
* 在DOM树中，除了有标签类型的节点，还有其他类型的节点,只要是节点类型的，那么都会有一个属性 nodeType
>Node的一些操作属性

* Node.nodeName 节点名称
* Node.nodeType 节点类型
* Node.nodeValue 节点的值
* Node.childNodes 节点集合
* Node.firstChild 第一个节点
* Node.lastChild 最后一个节点
* Node.textContent 节点内容
* Node.nextSibling 下一个兄弟节点
* Node.previousSibling 上一个兄弟节点
* Node.ownerDocument 所属的文档对象
* Node.prentNode 父节点
* Node.prentElement 父元素节点
---
## DOM操作
### DOM得
##### 创建 
> createElement()
* 因为节点有很多种类，那么就会对应着不同的节点创建的方法
    * 创建元素节点      document.createElement() createElement只有document对象下才有，其他的对象是没有该方法的
    - 创建文本节点   document.createTextNode()
    - 创建注释节点
    document.createComment()
* document对象是DOM中的最顶层对象 * document中所有节点都必须由document对象来创建
```
* attribute & property
        * attribute: html属性
        * property: 对象属性
        * 属性与属性的区别
        checkbox1.setAttribute('checked', '');
```
*  创建一个指定tagName的元素对象
    * createElement方法必须是document对象调用
    * 创建出来的是js中一个元素对象，这个对象默认和页面中元素没有关系的，我们需要通过后续的一些方法把这个对象渲染到页面中指定的位置
```
        var div = document.createElement('div');

```
> Node.appendChild(element)添加

*   Node 是一个节点，作为element父级
*   把element作为子节点追加到Node的最后
* 注意：
    *  * innerHTML==刷新元素==
            *   获取元素的html内容
            *   注意：它只是获取了html内容
            *   我们通过innerHTML的方式来更改结构的时候，页面中的页面看起来是没有变化，但是其实是用新的html覆盖了原来的html，只是他们结构样式是一样
 
```
<div id="box">
        <!--<p onclick="console.log('p标签被点击了')">这是原有的内容</p>-->
        <p>这是原有的内容</p>
    </div>

    <button>使用innerHTML的方式来添加新内容</button>
    <button>使用createElement的方式来添加新内容</button>
    <button>操作已经存在在页面中的元素</button>
    
var box = document.querySelector('#box');
var p = document.querySelector('p');
var buttons = document.querySelectorAll('button');
buttons[0].onclick = function () {
        box.innerHTML += '<div>这是新添加的内容</div>';
        }
buttons[1].onclick = function() {
            var div = document.createElement('div');
            div.innerHTML = '这是新添加的内容';
            div.style.color = 'red';
            div.onclick = function() {
                console.log('....')
            };
            box.appendChild(div);
        };

buttons[2].onclick = function() {
    document.body.appendChild(p);
};
```
> var dupNode = node.cloneNode(deep);
* dupNode
克隆生成的副本节点
*   Node是要被克隆的节点，返回克隆后的节点
*   deep: 是否采用深度克隆,如果为true,则该节点的所有后代节点也都会被克隆,如果为false,则只克隆该节点本身.

```
var box = document.querySelector('#box');
        var p = document.querySelector('p');
        var buttons = document.querySelectorAll('button');

        p.onclick = function() {
            console.log('p标签被点击了');
        };

        buttons[0].onclick = function () {
            // document.body.appendChild(p);
            var newP = p.cloneNode(true);
            newP.onclick = function() {
                console.log('新的p标签');
            };
            document.body.appendChild(newP);
        };
```
> var insertedElement = parentElement.insertBefore(newElement, referenceElement);
* 把newNode插入到parentNode下面的referenceNode前面
* insertedElement 是被插入的节点，即 newElement
* parentElement  是新插入节点的父节点
* newElement 是被插入的节点
* referenceElement 在插入newElement之前的那个节点

```
parentNode.insertBefore(newNode, referenceNode);
把newNode插入到parentNode下面的referenceNode前面

例
        var box = document.querySelector('#box');
        var p = document.querySelector('p');
        var buttons = document.querySelectorAll('button');

        p.onclick = function() {
            console.log('p标签被点击了');
        };

        buttons[0].onclick = function () {
            buttons[0].parentNode.insertBefore(p, buttons[0]);
        };
```
> replaceChild
* parentNode.replaceChild(newChild, oldChild);
    * 使用newChild替换oldChild

```
例
        var box = document.querySelector('#box');
        var p = document.querySelector('p');
        var buttons = document.querySelectorAll('button');

        p.onclick = function() {
            console.log('p标签被点击了');
        };

        buttons[0].onclick = function () {
            buttons[0].parentNode.replaceChild(p, buttons[0]);
        };
```
> parentNode.removeChild(Child);
 * 删除child
 
```
 var box = document.querySelector('#box');
        var p = document.querySelector('p');
        var buttons = document.querySelectorAll('button');

        p.onclick = function() {
            console.log('p标签被点击了');
        };

        buttons[0].onclick = function () {
            box.removeChild(p);
        };
```
> 其他的一些DOM操作
* node.contains( otherNode )比较节点的位置关系
    * node 是否
    * otherNode 是否是node的后代节点.
    * 如果 otherNode 是 node 的后代节点或是 node 节点本身.则返回true , 否则返回 false.
    * https://developer.mozilla.org/zh-CN/docs/Web/API/Node/contains
* node.compareDocumentPosition( otherNode )
    *   node是要和otherNode比较位置的节点.
    *   otherNode是被和node比较位置的节点.
    *   返回值是otherNode节点和node节点的位置关系.
    *   https://developer.mozilla.org/zh-CN/docs/Web/API/Node/contains
 * element.hasChildNodes()
    *   判断是否有子节点

```
例
    <div id="div1">
        <p id="p1"></p>
    </div>
    <p id="p2"></p>
    
        var div1 = document.querySelector('#div1');
        var p1 = document.querySelector('#p1');
        var p2 = document.querySelector('#p2');

        console.log( div1.contains(p1) );   //true
        console.log( div1.contains(p2) );   //false

        console.log( div1.compareDocumentPosition(p1) );
        console.log( div1.compareDocumentPosition(p2) );
        
        console.log(div1.hasChildNodes());//true
        console.log(p2.hasChildNodes());//false
```
---

### DOM样式操作
* 对一个DOM节点的样式进行操作
    *   element.style
    *   element.currentStyle
    *   getComputedStyle(element)
    *   element.clientWidth/clientHeight
     //width/height + padding
    *   element.offsetWidth/offsetHeight// width/height + padding + border
    *   element.scrollWidth/scrollHeight
//内容的宽高
    *   element.offsetLeft/offsetTop
  
    //获取element到定位父级的偏移值，如果没有父级，那么返回的是该元素到页面的距离
  *   element.scrollLeft/scrollTop
* 注意
    * element.getAttribute(属性名称)
    * element.setAttribute(属性名称, 属性值)
    * element.removeAttribute(属性名称)
    * 上面三个方法是用来操作标签上的属性(不是元素对象上的)
    * 特殊情况
```
var img = document.querySelector('img');
        // 对象属性property的值可能是根据元素的attribute来获取的，但是有的属性会做一些额外处理
        console.log(img.src);//http://localhost:63342/%E5%A6%99%E5%91%B3%E4%BA%8C%E6%9C%9F/4.17/logo.png
        console.log( img.getAttribute('src') );//logo.png
```
* 获取元素到页面的绝对距离
    * element.offsetParent（实际中父级会一层套一层）
        *  获取element的==定位父级==
    * getBoundingClientRect()//解决offsetParent复杂递归
        *  获取元素的矩形信息
        *   注意：相对于可视区的

```
  console.log(div3.getBoundingClientRect());
        console.log( div3.getBoundingClientRect().top + document.documentElement.scrollTop );
```
### 表格
*  一个表格最少需要一个tbody，如果没有，浏览器在渲染的时候会自动的添加，在js中获取的时候需要格外注意，最好是写html的时候，手动的加上
* 针对表格dom提供了一些的特殊操作
    *   tBobies
    *   tHead
    *   tFoot
    *   rows
    *   cells

```
 console.log( table.tBodies );

 console.log( table.tBodies[0].rows[0].cells[0] );

 console.log( table.children[0].children[0].children[0] );
```
