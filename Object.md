### Object
> Object() 可以创建对象

> Object.assign(target, ...sources)==把源对象添加到目标对象==
*  target 目标对象
* sources 源对象
* ==注意== 地址引用
> Object.create()
*   创建一个新对象__proto__
> Object.keys(obj)
*   返回指定对象的所有key，以数组的形式返回
>Object.values(obj)
*   返回指定对象的所有value，以数组的形式返回
>  Object.entries(obj)
*   返回指定对象的所有key与value，以数组的形式返回
> Object.freeze
* 阻止修改现有属性的特性和值，并阻止添加新属性。
> Object.defineProperty(obj, prop, descriptor)
* 给对象设置属性
    * obj : 要设置属性的对象
    * prop : 要设置的属性的名称
    * descriptor : 要设置的属性的描述，特征
* descriptor
    *   描述符：属性的描述，也可称为属性的属性，descriptor包含下面这些描述：
    * value：用于描述属性的值
    * writable：描述属性是否可写，默认是false
    * configurable: 描述属性是否可以被删除
    * enumerable: 描述属性是否可被枚举（for...in)
*  当一个属性通过 . 或者 [] 来设置的话，那么默认writable、configurable、enumerable值都是true，通过defineProperty来设置默认都是false
* 属性还有两个比较特殊的描述
    *  get
    *  set
        *   我们把这两个描述称为寄存器，用来描述属性被设置或被获取的时候行为，get与set不能与上面的四个描述同时存在，get与set是函数
        *   当我们去访问一个对象属性的时候，就会触发这个属性的get函数，如果我们去设置一个属性，那么就会触发这个属性的set函数
> obj.hasOwnProperty(prop)
*   判断prop是不是obj的自有属性或方法
    
```
var arr = [1,2,3];
        console.log( arr.hasOwnProperty('length') );    //true

        console.log( arr.hasOwnProperty('push') );  //false
```
> obj.constructor
*   获取对象的构造函数

```
 var arr = [1,2,3];
        var date = new Date();

        console.log( arr.constructor );//ƒ Array() { [native code] }
        console.log( date.constructor );//ƒ Date() { [native code] }
```
> obj.toString()
*   把obj转成字符串形式，很多的一些其他构造会==重写==toString方法，所以不同对象toString的内容不一定都是 [object Object]

```
var date = new Date();
 console.log( date.toString() );//Wed May 09 2018 00:03:32 GMT+0800 (中国标准时间)
  Date.prototype.toString = function() {
        return '...';//改变输出
    }
```
>  instanceof
*   运算符，二元

```
var arr = [1,2,3];

        console.log( arr instanceof Array );//true
        console.log( arr instanceof Date );//false
        console.log( arr instanceof Object );//true
```
> in操作符
* in操作符用来判断一个属性是否存在于这个对象中。但是在查找这个属性时候，先在对象本身中找，如果对象找不到再去原型中找。换句话说，只要对象和原型中有一个地方存在这个属性，就返回true

```
<script type="text/javascript">
      function Person () {
          
      }
      Person.prototype.name = "Jack";
      var p1 = new Person();
      p1.sex = "man";
      alert("sex" in p1);     // 对象本身添加的，所以true
      alert("name" in p1);    //原型中存在，所以true
      alert("age" in p1);     //对象和原型中都不存在，所以false
      
  </script>
```
### 判断数据类型的方式总结
> Type of()
* 一般用来测试简单数据类型和函数的类型。如果用来测试对象，则会一直返回object，没有太大意义。
> instanceof 
* ：用来测试一个对象是不是属于某个类型。结果味boolean值。
>  isPrototypeOf( 对象 ) 
* ：这是个 原型对象 的方法，参数传入一个对象，判断参数对象是不是由这个原型派生出来的。 也就是判断这个原型是不是参数对象原型链中的一环。