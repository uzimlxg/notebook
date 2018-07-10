####  组件是什么？
> vue中==核心概念==，也是现代网页开发中的很重要的概念，vue、react、angular都支持组件，原生的js也是支持的（还没有正式确定）
* 特点
    * 复用
    * 独立
> 简单理解
* 把结构、样式、行为通过某种方式进行包装，形成一个具有独立功能小模块
    * UI组件（也包含功能组件）
    * 功能组件
> 组件的创建
*  Vue.component(组件名称，组件配置)
* 组件名称
    * 定义组件名称的方式有两种
        * kebab-case：烤串命名
        * PascalCase：驼峰命名
    * ==注意==:因为组件是通过标签的方式来使用的，组件的名称必须符合标签名称的规范
* 组件配置
    * template：组件的结构
    
> 组件的使用
* 组件是通过 html 标签的形式来进行复用（使用）的
* 我们创建一个组件其实就是创建了一个自定义的html标签
* 其实 new Vue 得到的就是一个组件，只是该组件是整个vue实例的根组件    
``` 
        <div id="app">

        <miaov></miaov>

        <abc></abc>
        <!--html不区分大小写，大写的ABC其实还是abc-->
        <ABC></ABC>
        <a-b-c></a-b-c>

    </div>
        Vue.component('miaov', {
            template: `<h1>miaov</h1>`
        });
        /*
        * html不区分大小写，但是在js中是区分了的
        * 但是为了与html进行关联，所以使用的时候驼峰命名转烤串命名使用
        * */
        Vue.component('ABC', {
            template: `<h1>ABC</h1>`
        });

        Vue.component('abc', {
            template: `<h1>abc</h1>`
        });
```
#### 组件的分类
> 全局组件
* 在不同Vue的实例中都可以使用的
> 局部组件
* 注册在某个单独的组件内部

> 局部组件选项——> components选项

* 注册局部组件
```
/*
        * 全局注册
        * */
        Vue.component('miaov', {
            template: `<h1>miaov</h1>`
        });


        const app1 = new Vue({
            el: '#app1',
            components: {
                //  注册一个局部的组件，key就是组件的名称，值也就是对象就是组件的配置
                m1: {
                    template: `<h2>我是m1</h2>`,
                    components: {}
                }
            }
        });
```
#### 组件的复用
> 如果我们希望组件能够具备更大的复用性，那么组件中的数据应该是有时候是可变的，通过使用组件传入参数

> 函数，我们可以在调用的时候，通过()传递参数，因为组件是通过html标签的方式来调用，那么组件需要接收的参数就是通过标签的属性来传入的

* 首先需要给组件定义形参，通过组件配置 props 来定义形参，也就是定义组件可以接收哪些参数
* ==注意==：组件不能直接访问父级的作用域，组件内部作用域是封闭的，外部不能直接访问，内部也不能直接访问外部

> 根节点：每一个组件的模板有且仅有一个根节点

```
     <div id="app1">
        <list v-for="list in lists" :title="list.title" :data="list.data"></list>
    </div>
 
 Vue.component('list', {
            props: ['title', 'data'],   //组件接收一个title参数，外部可以通过title属性传入
            template: `
                <div>
                    <h2>{{title}}</h2>
                    <ul>
                        <li v-for="v in data">{{v}}</li>
                    </ul>
                </div>
            `
        });
        const app1 = new Vue({
            el: '#app1',
            data: {
                // title1: '用户',
                // title2: '课程',
                // data1: ['张三','李四'],
                // data2: ['HTML','CSS']

                lists: [
                    {title: '用户', data: ['张三','李四']},
                    {title: '课程', data: ['HTML','CSS']}
                ]
            }
        });
```

#### 组件数据
> 全局数据与局部数据
* this.v 其实就是 外部的n，vue中禁止组件内部直接去修改外部数据，外部的数据可能不止被当前的这个组件所单独使用，如果能直接修改外部传入的数据，那么就会影响到使用该外部数据的其他组件
> 组件的内部还有一个存放组件数据的data
*  组件使用的外部数据存储在props中
 *  组件使用的内部数据存储在data中
 * 在组件内部，能够直接修改data中的数据，但是不能直接修改props中数据
> data选项中注意事项
*  组件中data选项必须是一个函数
*  该函数会在组件初始化的时候自动被调用
* 该函数的返回值将作为data的值
* 函数必须返回一个对象
> ==注意==
*  data中的值和props中的值都会被挂载到该组件下面，props中的key不能与data中key重复
* 
```
 <div id="app">
        <list :n="n" :min="0" :max="8"></list>
        <list :n="n" :min="0" :max="20"></list>
    </div>
    <script src="js/vue.js"></script>
    <script>
        Vue.component('list',{
            props:['min','max','n'],
            data(){
                return{
                    v:this.n
                }
            },
            template:`
            <div class="num">
                <button @click="mins">-</button>
                <input type="text" :value="v">
                <button @click="next">+</button>
            </div>

            `,
            methods:{
                mins(){
                    console.log(this.min)
                    if(this.v>this.min){
                        this.v-=1;
                    }
                },
                next(){
                    if(this.v<this.max){
                        this.v+=1;
                    }
            }
        }})
        let app=new Vue({
            el:'#app',
            data:{
                n:0
            }
        })
```
>  组件中的数据props
* 名称命名与组件命名的命名规则是使用是一样的
* 如果不使用v-bind传入的值就是普通的字符串，如果希望传入各种不同的类型的数据（表达式）：使用v-bind来绑定传入或者使用简写的
* props验证
    * 如果我们需要对传入的prop进行验证或者设置默认值等操作就需要用到porps验证
    * props接收的是一个数组，数组中存的接收的属性名称，是字符串类型，如果需要对每个传入的属性进行验证，那么属性就不能直接设置成字符串类型
    * 格式
        * 
```
props: {
                 属性名: 值的类型,
                 // 多个可能的类型
                 属性名: [值的类型1, 值的类型2],
                // 可选或必填
                 属性名: {
                     type: 值的类型 | [值的类型1, 值的类型2],
                     // 是否必须设置
                     required: true,
                     // 设置默认值
                     // 默认值既可以直接设置，也可以是一个函数，该函数返回值将作为默认值
                     default: 0,
                     default() {return 0}
                 },
                 // 验证的规则既可以是上面默认的那些设置，也可以自定义
                 属性名: {
                     validator() {
                         //该方法会在接收到对应的属性的时候调用，返回一个布尔值，如果返回true表示验证通过，否则不通过
                     }
                 }
             }
```
#### 组件通信
> 子级能够使用传入的数据，但是不能私自去更改传入的数据，但是这个数据并不是不能该，而是需要由这个数据所有人去决定，子级只能向数据拥有者提出修改要求，这也就是vue中的组件数据通信规则，==数据流==
* 组件外部到组件内部：  父到子
    * 通过props
* 组件内部到外部：子到父
    * 通过事件
        *在vue中，提供了一套自定义事件系统，组件都实现了事件特性
        *  在组件内部可以通过组件的一个方法：$emit() 来触发一个自定义的事件
        * 父级就可以监听该事件，并为该事件绑定一个事件函数，因为组件在vue中是通过元素的方式来使用的，那么监听一个组件的事件，其实就是和监听元素事件的处理方式是一样的
        
        *  $emit(自定义的事件名称, 传入给监听函数的数据)
        * 监听函数的第一个参数就是这个$emit方法第二个参数
> v-model 
*  v-model其实就是v-bind+@input+input()的一种简化操作
* 使用规则
    *  v-model默认绑定到组件的==value==属性，如果要使用v-model，那么组件就必须有一个value属性
    * 触发的事件必须是 input 事件
    
    *  如果我们使用v-model去绑定一个值，那么当组件内部触发input事件的，vue会自动的去帮助我们监听input事件，并修改n的值为input事件的第二个参数的值
    * v-model用来确定input事件发生的时候，修改的是那个外部值
    
* 注意：一个组件只能绑定一个v-model


* 总结：
    * 1、 v-bind_input自定义事件_@input

    * 2、 v-model_绑到组件里的value_Vue监听触发input事件
    
    * 3、 model选项将{ prop?: string, event?: string }

#### 组件的生命周期
>   生命周期钩子
* 生命周期：从开始到结束的过程，组件生命周期就是组件创建到销毁的过程
    * vue为了能够让我们在一组组件运行过程对它进行更多的控制，所以在组件的运行过程嵌入一些函数的调用，当组件运行到某个状态的时候，就会触发指定函数调用，我们把这个嵌入点称为钩子，嵌入点执行的函数称为钩子函数
![image](https://cn.vuejs.org/images/lifecycle.png)

*  beforeCreate
    * 数据监听和event/watcher事件配置之前被调用，——此时组件的选项还未挂载，无法获得data中的数据，methods中的方法
*   created
    * 实例已经创建完成之后被调用。这一步完成以下操作：
        * 数据观测，属性和方法的运算，watch/event事件回调。
        * 挂载阶段还没有开始，$el属性是不可见的
    * 一个常用的生命周期，可以调用methods与data中的数据，并且修改可以通过Vue响应式绑定体体现在页面上，获取computed中的计算属性等等
    * 注意：ajax请求最好不在这里发，在组件路由beforeRouteEnter中发
*    beforeMount
    * 在挂载开始之前被调用：相关的redenr函数首次被调用
*    mounted
    * 挂载完成后调用
*    beforeUpdate
    * 数据更新时调用，发生在虚拟DOM重新渲染和打补丁之前，可以在这个钩子里进一步更改状态，这不会触发附加的重渲染过程。
*    updated
    * 数据DOM重新渲染和打补丁，这是DON已经更新，现在可以执行以依赖DOM进行一些操作
    * 注意：在这里更改数据的时候有可能导致更新无限渲染
*    activated
        组件被激活的时候触发
*    deactivated
        组件被冻结的时候触发
*     beforeDestroy
    * 实例销毁之前被调用，在这里仍然完全可用
    * 用处
        * 1、可以用this来获取实例
        *  2、 一般在这里进行重置操作。例如：清除组件里的定时器，监听DOM事件
*    destroyed
    * Vue实例销毁后被调用，调用后Vue实例指示的所有东西将会解绑定，所有的事件监听器会被移除，所有的的子实例也会被销毁
*    errorCaptured
    * (err: Error, vm: Component, info: string) => ?boolean
    * 当捕获一个来自子孙组件的错误时被调用。此钩子会收到三个参数：错误对象、发生错误的组件实例以及一个包含错误来源信息的字符串。此钩子可以返回 false 以阻止该错误继续向上传播。
    
#### 插糟
> 在自定义组件中，被组件包含的内容会被组件解析后的模板给覆盖了，为了保留嵌套内容所需要的位置，从而使用插槽
> 插槽解决的问题
*  解决组件嵌套的问题
* 利用插槽解决传递复杂的结构数据

> <slot>
* 其实vue在解析组件自身的模板之前，会把当前组件嵌套内容保存了起来，我们可以通过一个 vue 内置的一个自定义组件来获取到保存的内容
 能够把当前组件的模板与组件嵌套的内容进行合并
 * 为了能够把渲染页面与处理逻辑把template中的内容放在模块中
    * 模板中设置id名，在template：id
* 有名插槽
    * 给需要嵌套的标签加上slot属性取个名字<div slot="id"></div>
    * 再在模块中设置slot标签<slot name="id"></slot>
    * ==注意==：不设置指定的name，将会被作为默认插槽，默认插槽有且只有一个

#### watch选项<侦听器>
> 当某个数据发生变化的时候，vue会自动处理解析，但是，我们可能还需要在数据发生变化，做一些其他方面的事情，这个我们就可以通过watch这个选项来进行处理了
> 书写格式

```
 watch: {
                q(newVal) {
                    //当数据中的q值发生变化的时候，watch中对应的方法就会被执行
                    // newVal 接收到的就是q的当前最新的值
                    // console.log(newVal);

                    var script = document.createElement('script');
                    script.src = 'https://suggest.taobao.com/sug?code=utf-8&q='+ this.q +'&callback=abc';
                    document.body.appendChild(script);
                }
            }
```
#### computed计算属性
*  当应用中有一种数据是根据已有数据根据某个条件筛选或者过滤得到的，那么我们可以使用计算属性来完成这个工作
* 在computed定义的就是数据，数据的名称就是showUsers，他的值是通过对应的函数执行得到的，当我们去调用showUsers这个数据的时候，computed中对应的showUsers方法就会被执行，返回值会被赋值给showUsers数据，当计算属性中依赖的数据发生了改变，那么计算属性的值就会重新计算

```
<ul>
    <li v-for="con in showUsers">{{con}}</li>
</ul>  


data:{
    users:{
        
    }
}
conmputed:{
    showUsers(){
        return this.users....
    }
}
```
#### 自定义指令
> 全局指令
* Vue.directive(指令的名称，指令的配置)
> 局部指令
*  组件的配置项中，directives:{指令名称:{指令配置}}
> ==注意==：
* 指令在使用的时候，必须加v-的前缀，但是在声明的时候不需要
> 指令的配置就是指令提供一套钩子函数
* bind
    * 只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置
* inserted
    * 被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)
* update
    * 当组件上的数据发生改变的时候，组件更新的时候
* componentUpdated
    *  当组件更新完成以后触发
* unbind
    * 把指令总组件中删除的时候触发
    
> 钩子函数的参数
* 钩子函数执行的时候，vue传给钩子函数的数据
    * el : 指令当前     绑定的元素（DOM对象）
    *  binding : 一个对象，包含以下属性：
        * rawName：指令的完整的名称
        * name：指令名，不包括 v- 前缀
        * arg: 参数部分的内容
        *  指令的值有两种表示方式
            * value 解析后的值
            * expression 原始值，字符串  未解析 
* ref类似id属性
    * 给元素添加一个ref属性
    * 然后在组件内部就可以通过this$refs获取指定ref元素
 ####  过滤器
 > Vue.filter(过滤器名称，过滤器配置-函数)
* 全局过滤器
    * Vue.filter(format,value管道符上一步的结果)
    * Vue.filter(format,(value,a)=>{}  a就是参数，可传的参数
* 组件选项内的本地过滤器
```
     filters: {
        capitalize: function (value) {
             return value.charAt(0).toUpperCase() + value.slice(1)
                     }
                }

 ```
 ---
 例：
```
  <div id="app">
        <input type="text" v-model="message" />
        <!--管道符的上一步的结果作为下一步函数的第一个参数-->
        <h1>{{message|format}}</h1>
        <h1>{{newMessage}}</h1>
        <h2>{{1001|currency('￥')}}</h2>
        <h2>{{1001|currency('$')}}</h2>
        <!--d(c(b(a('1'))))-->
        <!--'1'|a|b|c|d-->
        {{obj}}
    </div>
    <script>

        Vue.filter('format 过滤器名称', value => {
            // value 就是管道符的上一步的结果
            return value.split('').reverse().join('').toUpperCase();
        });
        // 第一个参数是上一次的结果，a后续的一些参数
        Vue.filter('currency', (value, a) => {
            // console.log(a)
            return a + (value / 100).toFixed(2);
        });
        const app = new Vue({
            el: '#app',
            data: {
                message: 'Hello Miaov',
                obj: {
                    x: 1
                }
            },
            computed: {
                newMessage() {
                    return this.message.split('').reverse().join('').toUpperCase();
                }
            }
        });

    </script>
```
> Vue.use( plugin )
* 用法：
    * 安装 Vue.js 插件。如果插件是一个对象，必须提供 install 方法。如果插件是一个函数，它会被作为 install 方法。install 方法调用时，会将 Vue 作为参数传入。
    * 当 install 方法被同一个插件多次调用，插件将只会被安装一次。
    *   当我们需要操作数据以后后面紧接着要操作数据对应dom的时候，使用$nextTick，这个方法接收一个函数，这个函数将会在当前这次渲染结束以后执行

            
            
            