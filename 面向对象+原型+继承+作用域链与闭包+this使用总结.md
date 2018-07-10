### 一、面向对象
> 1、什么是对象
*  面向对象就是把构成问题事物分解成多个对象，建立对象不是为了完成某个步骤，而是描述某个事物在这个解决问题的步骤中的行为。
    * 面向对象是一种程序思维
    * 面向对象是一种编程方法
    * 面向对象不只是针对一门编程语言
> 2、 面向对象与面向过程的区别
* 面向过程过程侧重整个问题的解决步骤，着眼局部或者具体
* 面向对象侧重具体的功能，让某个对象具有这样的功能。更加侧重于整体。

```
各自的优缺点：
  ​
      面向过程的优点：
          流程化使得编程任务明确，在开发之前基本考虑实现的方法和最终结果；
          效率高，面向过程强调代码的短小精悍，善于结合数据结构来开发高效率程序；
          流程明确，具体步骤清楚，便于节点分析。
                  
      面向过程的缺点：
          需要深入的思考，耗费精力，代码重用性低，扩展能力差，维护起来难度比较高，
          对复杂业务来说，面向过程的模块难度较高，耦合度也比较高。
  ​
      面向对象的优点：
          结构清晰，程序便于模块化，结构化，抽象化，更加符合人类的思维方式；
          封装性，将事务高度抽象，从而便于流程中的行为分析，也便于操作和自省； 
          容易扩展，代码重用率高，可继承，可覆盖；
          实现简单，可有效地减少程序的维护工作量，软件开发效率高。
  ​
      面向对象的缺点是：
          效率低，面向对象在面向过程的基础上高度抽象，从而和代码底层的直接交互非常少机会，从而不适合底层开发和游戏甚至多媒体开发；
          复杂性，对于事务开发而言，事务本身是面向过程的，过度的封装导致事务本身的复杂性提高。
```
> 3、 面向对象的实现方式
* 面向对象的实现主流有两种方式：==基于类的面向对象==和==基于原型的面向对象==
* 面向对象的三大特征
    * 封装
        * 也就是把客观事物封装成抽象的类或具体的对象，并且类或对象可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。
    * 继承
        * 也就是把客观事物封装成抽象的类或具体的对象，并且类或对象可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。
    * 多肽
        * 不同实例的相同方法在不同情形有不同表现形式。多态机制使具有不同内部结构的对象可以共享相同的外部接口。
* 基于类的面向对象
    * 典型的语言：Java、C#——————对象（object）依靠 类（class)来产生
* 基于原型的面向对象（JS不包括ES6及以上——————ES6以上的Class相当于语法糖）
    *  典型的语言：JavaScript——————对象（object）则是依靠 构造器（constructor）利用 原型（prototype）构造出来的
> 4、多种创建对象的实现方式
* 1、使用new Object()创建
* 2、工厂模式创建
    * 工厂模式是软件工程领域一种广为人知的设计模式，这种模式抽象了创建具体对象的过程，考虑到在 ECMAScript 中无法创建类，开发人员就发明了一种函数，用函数来封装以特定接口创建对象的细节。
* 3、构造函数模式创建
    * 为了解决对象类型识别问题，又提出了构造函数模式。这种模式，其实在我们创建一些原生对象的时候，比如Array、Object都是调用的他们的构造函数。
    
```
<script>
    function Person (name, age, sex) {
        this.name = name;

        this.age = age;
        this.sex = sex;
    }
    Person.prototype.eat=function(){
        console.log(this.name + " Eat food");
    }
    var p1 = new Person("Jack", 20, "man");
    p1.eat();   //Jack Eat food
    var p1 = new Person("Mark", 30, "man");
    p1.eat();   //Mark Eat food
    alert(p1 instanceof Person);//true 判断P1的原型是否在Person的原型链上
</script>
```
> 5、 构造函数与普通函数的区别
* 1、他们都是函数。构造函数也是函数，也可以像普通的函数一样进行调用。 做普通函数调用的时候，因为没有创建新的对象，所以this其实指向了window对象。

```
function Person(){
      this.name = "Jack"; // 把name属性添加到了window对象上面
      alert(this === window);  //如果不作为构造方法调用，则 是true
  }
  Person();  // 把构造函数当做普通方法调用。这个时候内部的this指向了weindow
  alert(window.name);  //Jack
  function Human(){
      this.name = "Mark";
      alert(this instanceof window);  // false
      alert(this instanceof Human);  //true
  }
  var h = new Human();  //当做构造函数来调用，创建一个对象
  alert(h.name);
```
* 2、构造函数和普通函数仅仅也仅仅是调用方式的不同。也就是说，随便一个函数你如果用new 的方式去使用，那么他就是一个构造函数。
* 3、为了区别，如果一个函数想作为构造函数，作为国际惯例，最好把这个构造函数的首字母==大写==。
---
### 原型的理解
> 1、什么是原型与原型链（ji继承的实现方式）
* 原型就是JavaScript中的继承的继承，JavaScript的继承就是基于原型与原型链的继承。
* prototype，对象是通过构造函数创建出来的，如果某个类型所对应的对象有一些共用的数据，那么为了节省内存空间，方便维护管理，js把这些对象所公用的内容存储在一个统一的位置，这类对象又可能很方便的去调用他。
* js把某个类型的对象所公用的数据保存在这类的构造函数下的一个指定属性下面，这个属性是构造函数的属性，名称是：prototype，他的值是一个对象，用来保存这类对象所有公有数据的
为了能够让对象找到公有数据，所在在对象创建的时候，会把prototype同时赋值给对象，这个属性是：proto，也就是：当一个对象被构造函数创建出来的时候，会自动添加一个属性__proto__，他指向构造函数的prototype，所以对象.__proto__就是这个对象的构造函数的.prototype，我们可以通过 对象.__proto__调用到构造函数的prototype
* 虽然我们可以通过__proto__调用到构造函数的prototype了，但是js觉得有点复杂了，所以把这个调用进行了简化，当我们去调用一个对象属性或者方法的时候，会按照一种规则进行查找，首先会在对象自身上进行查找，如果找不到，会自动去这个对象__proto__上去查找
> 2、 与原型有关的属性及方法
* 2.1 prototype 
    * 存在于构造函数中 (其实任意函数中都有，只不过不是构造函数的时候prototype我们不关注而已) ，他指向了这个构造函数的原型对象。



![image](http://o7cqr8cfk.bkt.clouddn.com/public/16-11-10/6663492.jpg)
* 2.2 constructor属性
    * constructor属性存在于原型对象中，它指向了构造函数
    
    * 我们根据需要，可以为Person.prototype 属性指定新的对象，来作为Person的原型对象。
    
    * 但是这个时候有个问题，新的对象的constructor属性则不再指向Person构造函数了。
```

  <script type="text/javascript">
      function Person () {
      }
      alert(Person.prototype.constructor === Person); // true
      var p1 = new Person();
      //使用instanceof 操作符可以判断一个对象的类型。  
      //typeof一般用来获取简单类型和函数。而引用类型一般使用instanceof，因为引用类型用typeof 总是返回objece。
      alert(p1 instanceof Person);    // true
      alert(typeof p1); // object
  </script>
```
* 2.3 __proto__属性
    *  用构造方法创建一个新的对象之后，这个对象中默认会有一个不可访问的属性 [[prototype]] , 这个属性就指向了构造方法的原型对象。
    *  但是在个别浏览器中，也提供了对这个属性[[proto]]的访问(chrome浏览器和火狐浏览器。ie浏览器不支持)。访问方式：p1.__proto__
    * 尽量不要用这种方式去访问，因为操作不慎会改变这个对象的继承原型链。
> 3、 组合使用原型模型和构造函数模型来创建对象
* 3.1 原型模型创建对象的缺陷
    *  原型中的属性是共享的。就是说，用同一个构造函数创建的对象去访问原型中的属性的时候，大家都是访问同一个对象，如果一个对象对原型的属性进行更改，则会反映到所有对象上面。

    * 这个共享特性对方法(属性值是函数的属性)又是非常合适的。所有的对象共享方法是最佳状态。这种特性在c#和Java中是天生存在的。
* 3.2 使用构造函数创建对象的缺陷
    * 在构造函数中添加的属性和方法，每个对象都有自己独有的一份，大家不会共享。这个特性对属性比较合适，但是对方法又不太合适。因为对所有对象来说，他们的方法应该是一份就够了，没有必要每人一份，造成内存的浪费和性能的低下。

```
<script type="text/javascript">
      function Person() {
          this.name = "Jack";
          this.age = 20;
          this.eat = function() {
              alert("Eat food");
          }
      }
      var p1 = new Person();
      var p2 = new Person();
      //每个对象都会有不同的方法
      alert(p1.eat === p2.eat); //fasle
  </script>
```
* 3.3 使用组合模式解决以上问题
    * 原型模式适合封装方法，构造方法模式适合封装属性，综合两种模式的优点就有了组合模式。

```
 <script type="text/javascript">
        //在构造方法内部封装属性
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }
        //在原型对象内封装方法
        Person.prototype.eat = function (food) {
            alert(this.name + "Eat" + food);
        }
        Person.prototype.play = function (playName) {
            alert(this.name + "Play" + playName);
        }
        
        var p1 = new Person("Jack", 20);
        var p2 = new Person("Mark", 30);
        p1.eat("apple");
        p2.eat("orange");
        p1.play("football");
        p2.play("games");
    </script>
```
> 4、动态原型模型创建对象
*  3.3组合模式，也并非完美无缺，有一点也是感觉不是很完美。把构造方法和原型分开写，总让人感觉不舒服，应该想办法把构造方法和原型封装在一起，所以就有了动态原型模式* * 动态原型模式把所有的属性和方法都封装在构造方法中，而仅仅在需要的时候才去在构造方法中初始化原型，又保持了同时使用构造函数和原型的优点。

```
<script type="text/javascript">
        //构造方法内部封装属性
        function Person(name, age) {
            //每个对象都添加自己的属性
            this.name = name;
            this.age = age;
            /*
                判断this.eat这个属性是不是function，如果不是function则证明是第一次创建对象，
                则把这个funcion添加到原型中。
                如果是function，则代表原型中已经有了这个方法，则不需要再添加。
                perfect！完美解决了性能和代码的封装问题。
            */
            if(typeof this.eat !== "function"){
                Person.prototype.eat = function () {
                    alert(this.name + " Eat good");
                }
            }
        }
        var p1 = new Person("Jack", 40);
        p1.eat();   
    </script>
```
* 组合模式和动态原型模式是JavaScript中使用比较多的两种创建对象的方式。==建议==尽量使用动态原型模式，以便解决了组合模式下的封装不彻底
 ---
### 3、JS继承
##### 3.1 继承的概念

☞ 继承是所有的面向对象的语言最重要的特征之一。大部分的oop语言的都支持两种继承：接口继承和实现继承。

☞ 对JavaScript来说，没有类和接口的概念(ES6之前)，所以只支持实现继承，而且继承在 原型链 的基础上实现的。等了解过原型链的概念之后，你会发现继承其实是发生在对象与对象之间。这是与其他编程语言很大的不同。
##### 3.2 原型链的概念

☞ 在JavaScript中，将原型链作为实现继承的主要方法。其基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法

* 构造函数、原型(对象)和对象之间的关系。每个构造函数都有一个属性 prototype 指向一个原型对象，每个原型对象也有一个属性 constructor 指向函数，通过new 构造函数() 创建出来的对象内部有一个不可见的属性[[prototype]]指向构造函数的原型。当每次访问对象的属性和方法的时候，总是先从p1中找，找不到则再去p1指向的原型中找。

```
//下面的代码完成了Son继承Father的过程。
<script type="text/javascript">
      //定义一个构造函数。
      function Father () {
          // 添加name属性.  默认直接赋值了。当然也可以通过构造函数传递过来
          this.name = "马云";
      }
      //给Father的原型添加giveMoney方法
      Father.prototype.giveMoney = function () {
          alert("我是Father原型中定义的方法");
      }
      //再定义一个构造函数。
      function Son () {
          //添加age属性
          this.age = 18;
      }
      //关键地方：把Son构造方法的原型替换成Father的对象。  因为原型是对象，任何对象都可以作为原型
      Son.prototype = new Father();
      //给Son的原型添加getMoney方法
      Son.prototype.getMoney = function () {
          alert("我是Son的原型中定义的方法");
      }
      //创建Son类型的对象
      var son1 = new Son();
  ​
      //发现不仅可以访问Son中定义属性和Son原型中定义的方法，也可以访问Father中定义的属性和Father原型中的方法。
      //这样就通过原型完成了类型之间的继承。 
      // Son继承了Father中的属性和方法，当然还有Father原型中的属性和方法。
      son1.giveMoney();
      son1.getMoney();
      alert("Father定义的属性：" + son1.name);
      alert("Son中定义的属性：" + son1.age);
  ​
  </script>
  //完成继承的示意图
 
```

* 完成继承的示意图（默认顶端示意图）
    * ![image](http://o7cqr8cfk.bkt.clouddn.com/blog/20161111/123921677.png)
> 原型链（并非完美无缺）在继承中的缺点
* 1.父类型的属性共享问题
    *  在原型链中，父类型的构造函数创建的对象，会成为子类型的原型。那么父类型中定义的实例属性，就会成为子类型的原型属性。对子类型来说，这和我们以前说的在原型中定义方法，构造函数中定义属性是违背的。子类型原型(父类型对象)中的属性被所有的子类型的实例所共有，如果有个一个实例去更改，则会很快反应的其他的实例上。
    *  
```
<script type="text/javascript">
      function Father () {
          this.girls = ["Andy", "Lucy"];
      }
      function Son () {
          //这里加上Father.call(this)解决问题
      }
      // 子类的原型对象中就有一个属性 girls ，是个数组
      Son.prototype = new Father();   
      var son1 = new Son();
      var son2 = new Son();
      //给son1的girls属性的数组添加一个元素
      son1.girls.push("Lily");
      //这时，发现son2中的girls属性的数组内容也发生了改变
      alert(son2.girls);  // "Andy", "Lucy", "Lily"
  </script>
```
>  向父类型的构造函数中传递参数问题

☞ 在原型链的继承过程中，只有一个地方用到了父类型的构造函数，Son.prototype = new Father();。只能在这个一个位置传递参数，但是这个时候传递的参数，将来对子类型的所有的实例都有效。

☞ 如果想在创建子类型对象的时候传递参数是没有办法做到的。

☞ 如果想创建子类对象的时候，传递参数，只能另辟他法。

##### 3.3 借用构造函数调用继承
> 借用构造函数调用 继承，又叫伪装调用继承或冒充调用继承。虽然有了继承两个字，但是这种方法从本质上并没实现继承，只是完成了构造方法的调用而已。

☞ 使用 call 或 apply 这两个方法完成函数借调。这两个方法的功能是一样的，只有少许的区别(暂且不管)。功能都是更改一个构造方法内部的 this 指向到指定的对象上。

```
 <script type="text/javascript">
      function Father (name,age) {
          this.name = name;
          this.age = age;
      }
      //如果这样直接调用，那么father中的this只的是 window。 因为其实这样调用的： window.father("李四", 20)
      // name 和age 属性就添加到了window属性上
      Father("Jack", 20);
      alert("name:" + window.name + "\nage:" + window.age);  //可以正确的输出
  ​
      //使用call方法调用，则可以改变this的指向
      function Son (name, age, sex) {
          this.sex = sex;
          //调用Father方法(看成普通方法)，第一个参数传入一个对象this，则this(Son类型的对象)就成为了Father中的this
          Father.call(this, name, age);
      }
      var son = new Son("Mark", 30, "man");
      alert("name:" + son.name + "\nage:" + son.age + "\nsex:" + son.sex);
      alert(son instanceof Father); //false
  </script>
```
* 函数借调的方式还有别的实现方式，但是原理都是一样的。但是有一点要记住，这里其实并没有真的继承，仅仅是调用了Father构造函数而已。也就是说，son对象和Father没有任何的关系。
* Father的原型对象中的共享属性和方法，Son没有办法获取。因为这个根本就不是真正的继承。
##### 3.4 组合继承
> 组合函数利用了原型继承和构造函数借调继承的优点，组合在一起。成为了使用最广泛的一种继承方式。

```
<script type="text/javascript">
      //定义父类型的构造函数
      function Father (name,age) {
          // 属性放在构造函数内部
          this.name = name;
          this.age = age;
          // 方法定义在原型中
          if((typeof Father.prototype.eat) != "function"){
              Father.prototype.eat = function () {
                  alert(this.name + " Eat food");
              }
          }  
      }
      // 定义子类类型的构造函数
      function Son(name, age, sex){
          //借调父类型的构造函数，相当于把父类型中的属性添加到了未来的子类型的对象中
          Father.call(this, name, age);
          this.sex = sex;
      }
      //修改子类型的原型为父类型的对象。这样就可以继承父类型中的方法了。
      Son.prototype = new Father( );
      var son1 = new Son("Jack", 30, "man");
      alert(son1.name);
      alert(son1.sex);
      alert(son1.age);
      son1.eat();
  </script>
```
### 4、作用域链与比闭包
##### 4.1 匿名函数
> 什么是匿名函数
* 声明一个函数没有函数名的就是匿名函数
* 有名函数就是具名函数
> 匿名函数应用场景
* 1、给标签绑定事件的时候
* 2、定时器的时候
* 3、给对象定义方法的时候
* 4、匿名函数的自调用（function（）{}）（）
##### 4.2 变量的作用域
> 变量的作用域指的是，变量起作用的范围。也就是能访问到变量的有效范围。依据作用域的范围可分为并分为：

* 1：全局变量
* 2：局部变量
> 全局变量
* 定义在函数外部的变量就是全局变量。全局变量的作用域是当前文档，也就是当前文档所有的JavaScript脚本都可以访问到这个变量。

*  所有的全局变量的声明都会提前到JavaScript的前端声明。也就是所有的全局变量都是先声明的，并且早于其他一切代码。
*  但是赋值的位置不会改变

> 局部变量
* 在函数内声明的变量，叫局部变量！表示形参的变量也是局部变量！
* 局部变量的作用域是局部变量所在的整个函数的内部。 在函数的外部不能访问局部变量。
> js中有没有块级作用域
* js中没有块级作用域

```
 <script type="text/javascript">
    var m = 5;
    if(m == 5){
      var n = 10;
    }
    alert(n); //10
  </script>
```
* 只有定义方法内部的变量才是局部变量
* 即使我们把变量的声明放在 if、for等块级语句内，也会进行声明提前的操作！
##### 4.3 作用域链——————作用域的深入理解
> 执行环境

* 执行环境（ execution context ）是 JavaScript 中最为重要的一个概念。执行环境定义了变量或函数有权访问的其他数据，决定了它们各自的行为。每个执行环境都有一个与之关联的 变量对象（variable object），环境中定义的所有变量和函数都保存在这个对象中。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。

* 全局执行环境是最外围的一个执行环境。在 Web 浏览器中，全局执行环境被认为是 window 对象，因此所有全局变量和函数都是作为 window 对象的属性和方法创建的。对全局执行环境变量来说，变量对象 就是window对象，对函数来说，变量对象就是这个函数的 活动对象 （ 活动对象是在函数调用时创建的一个内部变量 ）

* 每个函数都有自己的执行环境，当执行流进入一个函数时，函数的执行环境就会被推入一个执行环境栈中。而在函数执行之后，栈将执行结束的函数的执行环境弹出，把控制权返回给之前的执行环境。
> 作用域链
* 作用域链与一个执行环境相关，作用域链用于在变量查找。
* 在JavaScript中，函数也是对象，实际上，JavaScript里一切都是对象。函数对象和其它对象一样，拥有可以通过代码访问的属性和一系列仅供JavaScript引擎访问的内部属性。其中一个内部属性是[[Scope]]，由ECMA-262标准第三版定义，他就指向了这个函数的作用域链。作用域链中存储的是与每个执行环境相关 变量对象 (函数内部也是活动对象)。
* 当创建一个函数( 声明一个函数 )后，那么会创建这个函数的作用域链。这个函数的作用域链在这个时候只包含一个变量对象(window)
```
<script type="text/javascript">
      function sum(num1, num2){
        
          var sum = num1 + num2;
          return sum;
        
      }
  </script>
```
* 说明：函数 sum 的作用域链示意图：

![image](http://o7cqr8cfk.bkt.clouddn.com/public/16-11-11/19437930.jpg)
* 函数创建的时候，这个时候作用域链中只有一个
变量对象 (window)

* 当执行下面代码的时候

```

  <script type="text/javascript">
      function sum(num1, num2){
          
          var sum = num1 + num2;
          
          return sum;
      }
      var sum = sum(3, 4);
  </script>
```
* 当调用 sum 函数时，会首先创建一个 “执行环境”，这个 执行环境 有自己的作用域链，这个作用域链初始化为 sum 函数的 [[scope]] 所包含的对象。然后创建一个 与这个执行环境相关的 变量对象( 活动对象 ) ，这个 变量对象 中存储了在这个函数中定义的所有参数、变量和函数。把 变量对象 存储在作用域中的顶端。 以后在查找变量的时候，总是从作用域链条的顶端开始查找，一直到作用域链条的末端。
 ![image](http://o7cqr8cfk.bkt.clouddn.com/public/16-11-11/31917762.jpg)
* 
在sum中访问一个变量的时候，总是从作用域链的顶端开始查找，如果找到就得到结果，如果找到不到就一直查找，直到作用域链的末端。



因为在方法内的存在变量和函数的声明提前现象，所以函数一旦执行 函数的活动对象(变量对象)中总是保存了这个函数中声明的所有变量和函数。



如果在函数中==又定义了一个内部函数(还没有执行)==，则这个时候内部函数的作用域，是包含了外部函数的作用域。
一旦内部函数开始执行则把自己的活动对象==添加到了这个作用域的顶端==。


```
 <script type="text/javascript">
      function sum(num1, num2){
          var sum = num1 + num2;
          function inner (a) {
          }
          return sum;
      }
      var sum = sum(3, 4);
  </script>
```
内部函数的作用域：
![image](http://o7cqr8cfk.bkt.clouddn.com/public/16-11-11/25437750.jpg)
##### 4.5闭包

```
<script type="text/javascript">
      function createSumFunction(num1, num2){
          return function () {
              return num1 + num2;
          };
      }
      var sumFun = createSumFunction(3, 4);
      var sum = sumFun();
      alert(sum);//7
  </script>
```
在上面的代码中，createSumFunction函数返回了一个匿名函数，而这个匿名函数使用了createSumFunction函数中的局部变量(参数)，即使createSumFunction这个函数执行结束了，由于作用域链的存在，他的局部变量在匿名函数中仍然可以使用，这个匿名函数就是闭包。

​ 闭包是指有权访问另一个函数作用域中的变量的函数。

​ 闭包是一种特殊的对象。它由两部分构成： 函数，以及创建该函数的环境 。环境由闭包创建时在作用域中的任何局部变量组成。在我们的例子中，sumFun 是一个闭包，由 匿名 函数和闭包创建时存在的num1和num2 两个局部变量组成。
##### 4.6闭包的应用
>1、返回外部函数的局部变量

```
  <script type="text/javascript">
      function outer () {
          var num = 5;
          //定义一个内部函数
          function inner () {
              //内部函数的返回值是外部函数的一个局部变量
              return num;
          }
          //把局部变量的值++
          num++;
          // 返回内部函数
          return inner;
      }
      var num = outer()();  // 6
      alert(num);  
  </script>
```
> 2、使用函数自执行和闭包封装函数
* 封装一个增删改查的对象

```

  <script type="text/javascript">
      var person = (function () {
          //声明一个对象，增删改查均是针对这个对象
          var personInfo = {
              name : "李四",
              age : 20
          };
          //返回一个对象，这个对象中封装了一些对personInfor操作的方法
          return {
              //根据给定的属性获取这个属性的值
              getInfo : function (property) {
                  return personInfo[property];
              },
              //修改一个属性值
              modifyInfo : function (property, newValue) {
                  personInfo[property] = newValue;
                  
              },
              //添加新的属性
              addInfo : function (property, value) {
                  personInfo[property] = value;
                  
              },
               //删除指定的属性
              delInfo : function (property) {
                  delete personInfo[property];
                  
              }
          }
      })();
      alert(person.getInfo("name"));
      person.addInfo("sex", "男");
      alert(person.getInfo("sex"));
  </script>
```
> 3、 for循环中的运用
* 除开this.index=i

```
<body>
      <input type="button" value="按钮1"    >
      <input type="button" value="按钮2"    >
      <input type="button" value="按钮3"    >
      <script type="text/javascript">
          var btns = document.getElementsByTagName("input");
          for (var i = 0; i < 3; i++) {   
              //因为匿名函数已经执行了，所以会把 i 的值传入到num中，注意是i的值，所以num
              (function (num) {
                  btns[i].onclick = function () {
                      alert("我是第" + (num + 1) + "个按钮");
                  }
              })(i);
          }
      </script>
</body>
```


### 5、this使用总结
> 1、this使用总结

```
 <script>
     /*
      * 默认绑定：
      *   当直接调用一个函数的时候，就是默认绑定
      *       1、非严格模式下，默认绑定到window上
      *
      * 隐式绑定：
      *   当使用 对象.方法() 这种方式调用，称之为隐式绑定
      *   this绑定到前面的那个对象上
      *
      * new 绑定：
      *   使用new来调用构造函数的方式
      *   this是绑定在新创建的那个对象上
      *
      * 显示绑定：
      *   call，apply：
      *       都是一锤子买卖，仅仅这一次调用的时候使用了显示绑定，对原函数没有如何的影响
      *
      *       call和apply的区别：就是参数的传递方式
      *           call：一个一个的传递
      *           apply：把要传递的参数封装到一个数组中去传递
      *
      *   bind：固定绑定   es6新增
      *       调用函数对象的bind方法，返回一个固定this绑定的新的函数
      *       对原来的函数没有影响
      *
      *
      *
      *   优先级：bind > call,apply > new > 隐式
      */
  ​
  ​
     //1、默认绑定
     function  foo() {
         console.log(this);//this指 obj   谁调用指向谁
     }
  ​
  ​
     //2、隐式绑定
     var name = "Mark";
     var obj = {
         name : "Jack",
         foo : foo,
         foo1 : function () {
             console.log(this.name);//this指 window
         }
     }
     obj.foo();//{name: "Jack", foo: function, foo1: function}
     var foo1 = obj.foo1;
     foo1();//Mark
  ​
  ​
     //3、new 绑定
     function  foo2() {
         this.name = "Lucy";
         console.log(this);//this 指向foo2    foo2 {name: "Lucy"}
     }
     var obj2 = new foo2();
     console.log(obj2);//this 指向foo2        foo2 {name: "Lucy"}
  ​
      var foo3 = obj.foo1;
      foo3();//Mark
  ​
      var obj3 = new foo;//foo {}
      console.log(obj3);//foo {}
  ​
  ​
     //4、显示绑定
  ​
     //call  apply
      function  foo4(a,b) {
          console.log(this.name,a,b);
      }
      foo4.call({name:"Jack"},10,20)//Jack 10 20
      foo4.apply({name:"Mark"},[20,10])//Mark 20 10
  ​
      //apply求max
      var arr = [23,65,2,45,3,57,4567];
      console.log(Math.max.apply(Math,arr)); //max = 4567
  ​
      //定义Math 求和的方法
      Math.sun = function () {
          return Array.prototype.reduce.call(arguments,function (sun,ele) {
              return sun + ele;
          },0)
      }
      console.log(Math.sun.apply(Math,arr));//sum = 4762
  ​
      //bind
      var obj4 = {
          name : "Jack"
      }
      function  foo5() {
          console.log(this.name);
      }
      var f = foo5.bind(obj4);//这种绑定方式优先级最高
      f();//Jack
  ​
      var obj5 = {
          name : "Mark",
          foo6 : f
      }
      obj5.foo6()//Jack
  </script>
```
> 绑定丢失问题

```
<script>
     /*
      * 回调函数的this绑定丢失问题:this会绑定到window
      *
      *   定时器
      *
      *
      * 显示绑定丢失问题
      *   显示绑定传入null、undefined时，this就成了默认绑定
      *
      */
  ​
     //定时器绑定丢失
     var name = "Jack";
     var obj = {
         name : "Mark",
         show : function () {
             setInterval(function () {
                 console.log(this.name);// 此时this指向window
             },1000)
         }
     }
     obj.show();//Jack++
  ​
     //解决方法一
     var obj1 = {
         name : "Mark",
         show : function () {
             var self = this;
             setInterval(function () {
                 console.log(self.name);// 此时this指向obj1
             },1000)
         }
     }
     obj1.show();//Mark++
  ​
     //解决方法二
     var obj2 = {
         name : "Joe",
         show : function () {
             setInterval(function () {
                 console.log(this.name);// 此时this指向obj2
             }.bind(this),1000)
         }
     }
     obj2.show();//Mark++
  ​
      //显示绑定丢失
      function foo() {
         console.log(this.name);
      }
      var f = foo.bind(undefined);// 此时this指向window
      f();//Jack
  </script>
```
