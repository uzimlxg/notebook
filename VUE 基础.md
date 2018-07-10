### Vue
> 是什么？
* Vue  是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。
*MVVM
    *   Model：数据
    *   View：视图（模板）
    *   ViewModel：视图数据
        *
* MVC
    *   Model：数据
    *   View：视图（模板）
    *   Controller：控制器
### Vue基础
#### 1、数据与页面内容绑定
> el
* 把Vue的实例对象与页面中的元素进行绑定（挂载），他决定了Vue实例对象能够操作页面中的哪些元素

```
         <div id="app">
            <h1>App</h1>
        </div>
        let app = new Vue({
            el: '#app'
        });
```
>  template
*   vue实例对象结构内容，vue的实例的模板会被Vue内部解析以后覆盖掉Vue实例对象挂载的元素，Vue实例解析后的内容会替换掉挂载元素在内的所有内容，所以el选项不推荐设置body和html为挂载点
* 如果template选项不存在，那么el所指定的元素的内容（包括自己的）将作为 template 选项的内容
* 如果 template 选项与内容同时存在，则 template 的优先级高于页面中的内容

```
 <div id="app">
        <h1>App</h1>
</div>
 let app = new Vue({
            // el: document.body,
            el: '#app',

             template: `
             <div id="app">
                 <h1>App</h1>
             </div>
             `
        });
```
> data
* 一个应用不能只有结构和样式，还应该有数据，那么这个 data 选项就是用来存储一个Vue实例中所需要用到的数据的，data 选项的值可以是对象，也可以是一个函数，
* ==注意==：这个函数必须返回一个对象，组件中必须是函数

```
let app = new Vue({
            el: '#app',
            // 直接赋值一个对象
            data: {
                name: 'miaov'
            },

            // 赋值一个函数，这个函数在Vue初始化的时候会被执行，执行后的结果返回给data，如果data是根据一系列的逻辑处理产生的，那么data可以设置成一个函数，在函数执行逻辑产生data
            // data() {
            //     return {
            //         name: 'miaov'
            //     }
            // }
        });
```
> 模板语法
* Vue中提供的一套内置的语法，这个语法可以在模板中使用，可以很方法在结构中去完成各种数据的输出以及逻辑的处理
    - 插值表达式
    - Vue模板中使用的一种特殊的字符串，他的作用是解析表达式，他会把语法中表达式的结果进行计算，然后显示
    - 语法结构
    - {{表达式}}
*  new Vue() => 读取template（没有的话会读取el指定的内容） => 解析读取到template，=> 渲染解析的结果到页面指定位置

 * 我们可以在template中调用data中的数据，这个数据不需要加data，其实模板中调用的是这个实例下的数据，换句话就是template中的变量，==前面默认是 this==，而模板中==this指向就是该实例的对象==
 
 *  注意：Vue实例是一个封闭空间，不能够直接访问全局下的属性与方法，在Vue实例化会把一些常用的数据和方法挂载到实例对象下，但是不是所有的
 
* XSS
    *   从安全方面考虑，内容会在渲染的时候做一些特殊的处理，html标签等内容会原样输出，而不是解析
> 指令
* 是Vue模板中使用的一种特殊的语法
     - 指令是以html标签属性的方式存在
     - 指令是以v-开始的一套自定义属性系统
     - 指令会影响当前这个指令的元素渲染的结果
     - Vue提供了一些内置的指令，同时我们也可以自定义自己的指令
    
* v-html
    *   把内容作为html解析
    *   指令是作为属性出现的
    *   指令可以接收值，指令的值是一个表达式，值会被vue作为js解析
#### 2、数据与元素绑定
> v-bind——>绑定数据到元素的属性
* <标签 v-bind:要绑定的属性名称="属性值"></标签>
    *   没有通过v-bind设置的属性，属性值就是普通的字符串
    *   通过v-bind设置的属性，值是作为js表达式进行解析执行的
* 简写方式
    *  <标签 :要绑定的属性名称="属性值"></标签>
* ==注意==：
    * 1、针对class和style属性vue会有一些特殊的处理，通过v-bind绑定的class和style的值，除了可以使用普通的字符串，还可以使用数组和对象的形式来设置
    * 2、在指令的值中不能使用 {{}} 语法

```
<div id="app">
        <h1>App</h1>
        <h2 class="classname">{{name}}</h2>
        <h2 v-bind:class="classname">{{name}}</h2>
        <h2 :class="classname">{{name}}</h2>

        <h2 :style="'color:red;border: 1px solid red'">{{name}}</h2>
        <h2 :style="{color: 'red', border: '1px solid red'}">{{name}}</h2>

        <h2 :class="'box box1'">{{name}}</h2>
        <h2 :class="['box', 'box1']">{{name}}</h2>
        <h2 :class="{'box': true, 'box1': false}">{{name}}</h2>

        <div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>

</div>
```
> 条件渲染
* v-if
    * 根据指令的值有条件对内容进行渲染
    * 当条件为真，则添加元素，当条件为假，则删除元素
*  v-show
    * 和上面的v-if类似，但是他不是删除和添加，而是隐藏和显示
    * 当元素内容会根据用户操作频繁的变更，那么使用v-show更合适，如果该内容只是根据数据初始化存在还是存在，那么使用v-if更好
* v-else
* v-else-if
> 列表渲染
* v-for => for in, for of  of和in一样

```
<ul>
            <li v-for="user,index of users">
                {{index}} - {{user.username}} - {{user.age}}
            </li>
        </ul>

        <hr />

        <h2>{{users[0].username}}</h2>

        <ul>
            <li v-for="user,key,index of users[0]">
                {{index}} - {{key}} - {{user}}
            </li>
        </ul>
        
           let app = new Vue({
            el: '#app',
            data: {
                users: [
                    {username: '莫涛', age: 30},
                    {username: '童斌', age: 28}
                ]
            }
        });
```
* key
    * 默认情况，vue渲染的时候会进行一定的优化处理，更大可能的去复用元素，而不是修改DOM节点（删除，移动），这个虽然会对渲染性能有提升，但是会发生数据在变化以后与原来的节点产生了脱节，特别在v-for中，这样的情况更加明显，所以为了解决这个问题，引入了key
    * vue为元素准备了一个自定义的属性：key，我们可以给这个key进行赋值，key的值必须是唯一的
    *  因为数组中的下标也不是与数据是强绑定的关系，所以不推荐使用数组的下标来作为key


```
<div v-if="loginType === 'username'">
            <label>Username</label>
            <input ：key="username" placeholder="Enter your username">
        </div>
        <div v-else>
            <label>Email</label>
            <input ：key="email" placeholder="Enter your email address">
        </div>
 let app = new Vue({
            el: '#app',
            data: {
                arr: [1,2,3],
                // 如果数据不满足要求，我们可以改造数据的结构
                arr2: [
                    {k: 0, v: 1},
                    {k: 1, v: 2},
                    {k: 2, v: 3},
                    {k: 3, v: 4}
                ],
                arr3: [],
                loginType: 'username'
            }
        });
```
* v-if与v-of
    * v-for与v-if在同一级上，v-for的优先级高于v-if，即使先写的v-if
    * 解决方案
        * 可以把v-if提升层级（结构），当然这里必须条件是arr3的，而不是item的


```
  <!--
            可以把v-if提升层级（结构），当然这里必须条件是arr3的，而不是item的
        -->
        <ul v-if="arr3.length > 0">
            <li v-for="item in arr3">
                {{ item }}
            </li>
        </ul>
  <!--
            可以把v-if提升层级（结构），当然这里必须条件是arr3的，而不是item的
        -->
        注意：这里的自定义标签，等到渲染后可以把标签删除
        <ul>
            <template v-if="arr3.length > 0">
                <li v-for="item in arr3">
                    {{ item }}
                </li>
            </template>
        </ul>
```
#### 事件
> 在vue中事件的绑定是通过行间的方式来实现的，同时vue提供了一个指令来处理事件绑定
* v-on
    * 在vue指令系统中，完整指令使用方式如下：
    
   <标签 v-指令名称:指令属性.指令修饰符.指令修饰符...="指令值（表达式）"></标签>
   
    * v-bind:id
    *    不是所有标签都有属性和修饰符，具体看当前这个指令的实现
*  v-on
    *   简写:@
    *   属性:要绑定的事件名称
 
    * 函数也需要和数据一样挂载到vue的实例对象中，但是vue为我们提供了一个专门挂载函数的位置：methods选项
    * ==注意==：methods中的函数不能使用箭头函数，箭头函数绑定到了声明的位置，默认情况下vue会把methods中的函数中的this指向该vue实例对象
    * methods下的函数也会像data中的数据一样，被挂载到vue实例对象中
    
```
<div id="app">

        <button v-on:click="isShow = !isShow">按钮</button>
        <button @click="showHide">按钮</button>
        <div v-show="isShow">内容</div>

    </div>
    
 let app = new Vue({
            el: '#app',
            data: {
                isShow: true
            },
            methods: {
                fn() {
                    // this => app
                    // console.log(this);
                },
                fn2() {
                    // 可以通过this访问到fn
                    // this.fn();
                },

                showHide() {
                    this.isShow = !this.isShow;
                }
            }
        });
```
* 事件对象
    *  如果一个方法绑定到了某个元素的事件上，那么默认情况下，该函数的第一个参数就是事件对象
    * 如果事件函数不需要传入额外的参数，那么可以省略()
    * 如果需要传入参数，则需要通过括号的方式来调用，但是一旦使用了()，那么事件对象就需要手动传入了，在模板中可以使用 $event 来引用事件对象

```
<div id="app">

        <button @click="getType">按钮</button>

        <button @click="getType1(1, $event)">按钮1</button>
        <button @click="getType1(2, $event)">按钮2</button>

</div>
let app = new Vue({
            el: '#app',
            data: {
            },
            methods: {
                getType(e) {
                    console.log(e);
                },
                getType1(v, e) {
                    console.log(v);
                    console.log(e);
                }
            }
        });

```

* 事件修饰符
 
    .stop

    .prevent
    
    .capture
    
    .self
    
    .once
    
    .passive
    
```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```


* 按键修饰符
    
    .enter

    .tab
    
    .delete (捕获“删除”和“退格”键)
    
    .esc
    
    .space
    
    .up
    
    .down
    
    .left
    
    .right
    
    可以通过全局 config.keyCodes 对象自定义按键修饰符别名：

    Vue.config.keyCodes.f1 = 112

* 系统修饰符
    
    .ctrl

    .alt
    
    .shift
    
    .meta
    
* .exact 修饰符允许你控制由精确的系统修饰符组合触发的事件。


```
<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
<button @click.ctrl="onClick">A</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>

<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```
* 鼠标修饰符
 
    .left

    .right
    
    .middle
#### 数据流
> 单向绑定
* 数据->视图
* 数据变化了，视图就会更新
> 双向绑定
* 数据<->视图
* 数据变化了，视图会更新，视图更新，数据也会变化
> 在vue中除了v-model方式绑定的数据是双向，其他的都是单向的
* 单向：

    * v-bind
    * v-text
    * v-html
    * {{}}
* 双向：
    * v-model
    * <自定义组件或指令>
>  v-model
*   通过v-model绑定的数据是双向的，注意：v-model数据不一定都是绑定到了value属性了
    * input:text => value
    * input:radio => checked
    * input:checkbox => checked
    * select => value
    * 如果是自定义的，我们可以自己去实现v-model绑定到什么属性上
