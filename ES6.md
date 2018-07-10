##### 申明变量Let和常量const
>let语法
* 块级作用域 以{}代码块作为作用域范围 只能在代码块里面使用
* 不存在变量提升： 先声明后使用，否则报错
* 暂时性死区：总之，在代码块内，使用let命令声明变量之前，该变量都是不可用的
* 不允许重复声明：不允许在相同作用域内，重复声明同一个变量，不能在函数内部重新声明参数
> consth语法（不变的量）
* 声明一个只读的常量。一旦声明，常量的值就不能改变,必须立即初始化
* 不允许重复声明
* 暂存死区（let声明的变量必须先声明后使用）
* 支持块级作用域
* 声明必须赋值，必须初始化
* 
#### 解构赋值
> 理解
* 解析(分解)结构，可以把数组（对象）进行分解，然后赋值
> 数组解构
* 数组的解构赋值，位置需要一一对应

```
数组：let [a,b,c]=[1,2,3]
嵌套数组解构：let [a,[b,c],d]=[1,[2,3],4](可用空位填充)
默认值:let [a,[b,c],d=5]=[1,[2,3],4](若有值，可替代默认值)

例：
         var arr = [1,2,3];
         var [a, b, c, d] = arr;
         console.log(a, b, c, d);
         var [e, f] = arr;
         console.log(e, f);

         var arr2 = [1, ['miaov','妙味'], 2];
         var [a, [a1, b1], c] = arr2;
         console.log(a, a1, b1, c);
```
> 非数组解构
* 对非数组的对象进行结构赋值，那么左侧变量的位置不在是一一对应的关系，而是key值对应

```
         var obj1 = {width:100,height:200};
        var width = 1;
        var height = 2;

        var {width: w, height: h} = obj1;
```
* 对象简洁表示法：当对象的key与value引用的变量名称一致，那么可以简写

```
 var v = 10;
        var obj2 = {
            value: v
        };
        // 如果obj2中的value和v是名称一致的话：
        var obj3 = {
            v: v
        };
        // 上面这个形式可以简写成下面的形式
        var obj4 = {
            v
        };
```
#### 属性名表达式
> 我们可以使用是一个表达式作为一个对象的属性名称
* 1.直接用标识符作为属性名：

```
obj.foo = true
```
* 2.用表达式作为属性名：
* 
```
obj['a'+'bc'] = 123

//相当于

obj['abc'] = 123
```

* 3.ES6 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。
* 
```
let key = 'foo';
let obj = {
    [key]: true,
    ['a'+'bc']: 123
};
复制代码
var lastWord = 'last word';

var a = {
  'first word': 'hello',
  [lastWord]: 'world'
};

a['first word'] // "hello"
a[lastWord] // "world"
a['last word'] // "world"
```

* 4.表达式用来定义方法名
* 
```
let obj = {
    ['say' + 'Something']() {
        return 'hello word';
    }
};

obj.saySomething(); // hello word
```

* 5.注意，属性名表达式与简洁表示法，不能同时使用，会报错。
* 
```
// 会报错
var foo = 'bar';
var bar = 'abc';
var baz = {[foo]};

//正确写法：
var foo = 'bar';
var baz = {[foo]: 'abc'};
```

* 6.注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心。
* 
```

const keyA = {a: 1};
const keyB = {b: 2};

const myObject = {
    [keyA]: 'valueA',
    [keyB]: 'valueB'
};

myObject // Object {[object Object]: "valueB"}
```

> 属性简洁表达式
* 当key与值（变量）名称相同的时候，可以简写

```
  var x = 1;
         var y = 2;
        
         var obj1 = {
             x: x,
             y: y
         };
         => 简写
         var obj2 = {
             x,y
         };
```
* 函数简写表达式
* 
```
 var obj3 = {
            fn: function() {

            }
        };
        // => 简写
        var obj4 = {
            fn() {
                
            }
        };
```
#### 实用方法
> Object.getPrototypeOf，Object.setPrototypeOf
* p1.__proto__======== Object.getPrototypeOf(获取原型)
> Proxy(秘书)=>这个特性就可以设置访问权限
*  一个构造函数，通过Proxy构造创建一个对象的代理对象

```
 var newObj = (function() {
            var obj = {
                x: 10,
                y: 100,
                z: 1000
            };

            return new Proxy(obj, {
                get(o, property) {
                    if (property != 'x') {
                        return o[property];
                    }
                }
            });
        })();

        console.log( newObj.x );
```
> 反射

```
  var obj = {x:1,y:2,z:3};

         for (var property in obj) {
             console.log( property );
         }

        console.log( Reflect.ownKeys(obj) );
```
> 函数（默认参数）
* es6可以通过形参来设置默认值
*   注意：有默认值的参数最好写在参数列表的最后面

```
 function fn(x, y) {
            //通过下面的方式来处理一个函数参数的默认值
            var x = x || 1;
            var y = y || 1;

            console.log(x * y);
        }
        fn();

        /*
        * es6可以通过形参来设置默认值
        *   注意：有默认值的参数最好写在参数列表的最后面
        * */
        function fn2(x=1, y=1) {
            console.log(x * y);
        }
        fn2();

        // 我们希望x是必传，y是可选，那么y这个参数就应该在x的后面
        function fn3(x, y=1) { // (y=1, x)
            console.log(x * y);
        }

        fn3(2);
```
> 函数（剩余参数）

```
 function fn(arr, ...data) {//剩余参数只能写在参数列表的最后面
            console.log(data);
            for (var i=0; i<data.length; i+=1) {
                arr.push(data[i]);
            }
            return arr;
        }

        console.log( fn(['a','b'], 1,2,3,4,5) );
```
> 扩展运算符
 *   ...
    *   与函数的剩余参数有点类似，但是功能正好是相反的
    *   函数参数中的 ... 表示剩余参数，把实参数据保存到 ... 后面的数组中变量中 1,2,3,4,5 => [1,2,3,4,5]
    *   扩展运算符，也就是非参数中的 ...，他的作用是==把类数组集合，拆分成实参列表== [1,2,3,4,5] => 1,2,3,4,5
        
```
  var arr = [10,20];

        // fn( arr[0], arr[1] );
        //fn(...arr); // fn(10,20)


        var arr1 = ['a','b',...arr];


        var arr2 = [1,4,54,23,423,41];

        console.log( Math.max(...arr2) );
```
> 函数=> 箭头函数
* 箭头函数的参数
    *   1， 如果箭头函数没有参数，那么需要使用一个小括号
    *   2, 如果箭头函数有参数
           * 1，有一个，()可写可不写
           * 2，有多个，()必须的
           
```
 var fn4 = () => {
            console.log(3);
        }
var fn5 = (a, b) => {
    console.log(3);
}
var fn6 = (a) => {
    console.log(3);
}
var fn7 = a => {
    console.log(3);
}
```
*  函数体
    *   如果函数体有且仅有一句，那么 {} 可以省略
    
```
var fn8 = a => console.log(a);
```
 * 函数返回值
    *   如果有没有 {} ，那么函数体的那仅有的一条语句的执行结果就是函数的返回值
    *   如果有 {} ，那么需要使用return返回了，如果没有return，那么默认返回undefined
    *   注意：如果仅有的一条语句是一个字面量对象,而且需要返回一个值，那么就必须加return

```
 var fn9 = a => a * 10;
        // function fn9(a) {
        //     return a * 10
        // }

        console.log( fn9(5) );

        // var fn10 = a => {v: a * 10};    //js不知道 {}是函数体的大括号，还是字面量对象的{}
        var fn10 = a => {
            return {v: a * 10}
        };
```
* 注意事项
    * 1. 箭头函数不能作为构造函数
    * 2. 箭头函数没有arguments
    * 3. 箭头函数的this，取决与声明期（普通函数的this取决于执行期）
    * 4. 箭头函数不能作为事件函数

```
 var lis = document.querySelectorAll('li');

        for (var i=0; i<lis.length; i+=1) {
            lis[i].onclick = function() {
                setTimeout(() => {
                    this.style.background = 'red';

                    // setTimeout(() => {
                    //     console.log(this);
                    // })

                }, 1000);
            }
        }
```
#### 数据结构
> set集合
* 集合，是js中新增一种数据结构，类似数组，但是Set中每一个数据是唯一的，不重复的
*  js提供了一个Set的构造函数来创建集合对象
* 属性及方法
    *   size: 属性，表示集合中数据的个数
    *   add(): 向集合中添加数据
    *   clear(): 清空集合
    *   delete(): 删除集合中指定的数据
    *   has(): 判断集合中是否存在某个指定的数据
    *   forEach(): 遍历集合
* 注意
    * 注意：不能直接从集合获取指定的数据，如果想操作集合中的数据，可以使用forEach，或者使用集合转数组的方式
> WeakSet
* WeakSet结构与Set类似，也是不重复的值的集合。	
* WeakSet是一个构造函数，可以传入一个类数组初始化默认值。
* WeakSet的==成员只能是对象==，而不能是其他类型的值
* WeakSet中的对象都是弱引用，即垃圾回收机制不考虑对该对象的引用
* WeakSet是不可遍历的
> Map
* ES6提供了map数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。
* Map也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。
    * 例[[key1,value1],[key2,value2]]
* 属性及方法
    *  map.size返回成员总数
    * map.get(key)通过key获取value
    * map.set(key,value)为Map的实例添加新键值对
    * map.has(key)查找key值是否存在。
    * map.delete(key)删除对应键值对
    * map.clear()清除所有成员
    * map.keys()遍历map的key值
    * map.values()遍历map的value值
    * map.entries()遍历map的key和value值
    * map.forEach(callback)遍历（与数组的forEach一样）第二个参数代表callback内的this指向。
#### 迭代器与迭代协议
>for in 与for of
* for in 根据对象的key来进行遍历
*  for of 根据对象的value来进行遍历（但不一定哦）
> 迭代器(函数)
* ：对象被迭代的时候调用的处理函数，一个对象是否能够被迭代，取决于该对象是否拥有迭代器
> [迭代协议及规则](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols)
 - 迭代器函数必须返回一个对象
 - 返回的对象中必须包含一个 next 方法
 - next方法必须返回一个对象
 - next方法返回的对象包含以下两个属性
     - value ：当前这次循环被迭代出来的值
     - done : 表示当前迭代是否已经完成，如果为true，表示完成了，终止循环，同时value会被忽略
     
```
obj1[Symbol.iterator] = function() {
            var keys = Object.keys(obj1);
            var len = keys.length;
            var n = 0;
            return {
                next() {

                    if (n < len) {
                        // 返回出去的值，可以根据自己的需求来定义
                        var result = {
                            value: {k: keys[n], v: obj1[keys[n]]},
                            done: false
                        };
                        n += 1;
                        return result;
                    } else {
                        return {
                            done: true
                        }
                    }


                }
            };
```
#### Generator
> Generator Function 生成器函数
*   有名函数
*   匿名函数
*   箭头函数
*   生成器函数
    * 在定义函数的时候，在function后面或者函数名的前面加上一个*
    * 生成器函数调用以后执行不是函数体本身，而是会执行内部生成器生成一个新的迭代器对象，然后调用迭代器对象下的next方法来实现执行函数调用
    * 配合yield语句，yield放在任意一条语句之前，那么yield会把整个函数拆分成多个执行单元，然后通过迭代器的next方法来调用每一个yield

```
function* fn2()        {
            // yield 1;
            // yield 2;
            // yield 3;
            // yield 4;


            for (var i=0; i<5; i+=1) {
                yield i;
            }

        }
          var f = fn2();
//         console.log(f);
//        console.log(f.next().value);
        setInterval(() => {
            console.log(f.next().value);
        }, 1000);//0 1 2 3 4 undfind
```
#### Promise异步处理
> Promise
* 构造函数，接收一个函数做为参数，这个函数就是要执行的异步操作
*  then方法是Promise中的异步操作完成以后，后续执行的方法
* then方法的执行需要Promise中的异步操作完成以后再去调用，但是默认情况下，Promise并不知道异步动作什么时候完成，需要我们在异步操作中去通知Promise事情完成得怎么样了
*   在Promise对象中有一个属性
    *  [[PromiseStatus]]：该属性是一个内部属性，外部不能直接访问，他有三个值，表示了当前Promise对象的完成状态
    * pending：未完成
    * resolved：已完成
    * rejected：已失败
*    当Promise的状态编程resolved，那么这个Promise对象的then方法中的函数才会被执行
*    该状态不能直接去修改，我们可以通过Promise为我们提供的几个方法来改变状态
*    在Promise构造函数的函数参数中会接收到两个传入的参数，这两个参数都是一个函数
*    第一个参数：是一个函数，调用该函数可以把Promise对象的状态改成resolved状态
*    第一个参数：是一个函数，调用该函数可以把Promise对象的状态改成rejected状态

```
 var p1 = new Promise(function(resolve, reject) {
            setTimeout(() => {
                console.log(1);
//                 resolve();
                 reject();
            }, 1000);
        });

        p1.then(function() {
            console.log(2);
        }, function() {
            console.log(3);
        });
```
> .then()
* 当Promise对象的状态改变的时候，就会执行当前Promise对象下所有then绑定的函数
* 注意：.then()完成后还是第一个，所以

```
var p = new Promise((resolve) => {
            setTimeout(() => {
                console.log(1);
                resolve();
            }, 1000);
        });
        p = p.then(() => {
            return new Promise((resolve) => {
                setTimeout(() => {
                    console.log(2);
                    resolve();
                }, 1000);
            });
        });
        p = p.then(() => {
            return new Promise((resolve) => {
                setTimeout(() => {
                    console.log(3);
                    resolve();
                }, 1000);
            });
        });
        p = p.then(() => {
            console.log(4);
        });
```

```
 function getRandom() {
            return new Promise((resolve) => {
                var n = Math.random();
                if (n < 0.5) {
                    resolve(n);
                }
            })
        }


        getRandom().then( v => {
            console.log(v);
        } );
```
> 错误处理
*   1. 通过then的第二个参数
    *  处理的当前这一次的错误
*   2. 通过catch捕获
    *  处理的整个流程中的错误
* 通过then处理失败：
    *   精确的捕获每一次失败的时候，同时失败不影响后续的任务
* 通过catch处理失败：
    *   统一捕获错误，当只要有错误就终止后续执行
> .finally
*   无论是成功还是失败都会执行的
*   如果一件事情无论是成功还是失败都要需要去做的，那么这个工作就可以放在finally中去完成，比如无论是登录成功还是登录失败都要记录日志

```
var p = new Promise((resolve, reject) => {

            if (Math.random() < .5) {
                resolve();
            } else {
                reject();
            }

        }).then(() => {
            console.log('成功');
        }).catch(() => {
            console.log('失败');
        }).finally(() => {
            console.log('无论成功还是失败');
        });
```
>  Promise.all()
*  这个方法是是一个静态方法，用来处理多任务的情况下的后续
* 用处
    * 当有多个异步任务要处理，同时后续的任务需要这多个任务全部完成以后再处理的情况下，我们使用 Promise.all
    *  all方法中去判断所有任务的状态，如果都完成了，并且都是resolved状态，就会执行all后面的then，只要有一个任务rejected了，那么就会执行then的第二个参数或者all后面的catch
    * 如果成功了，那么then接收到的参数是所有任务成功完成后的值，通过一个数组来保存
    
```
 var p1 = new Promise((resolve, reject) => {
            setTimeout(() => {
                var a = Math.random();
                // console.log(a);
                if (a < .5) {
                    resolve(a);
                } else {
                    reject('第一个任务失败');
                }
            }, 1000);
        });
        var p2 = new Promise((resolve, reject) => {
            setTimeout(() => {
                var a = Math.random();
                // console.log(a);
                if (a < .5) {
                    resolve(a);
                } else {
                    reject('第二个任务失败');
                }
            }, 1000);
        });
        
         Promise.all([p1, p2]).then(results => {
            console.log('都成功了', results);
        }).catch(err => {
            console.log(err);
        })
```
> Promise.race()
*   与all一样，可以处理多个任务，但是race只要有一个任务完成了就会执行后续的操作，而all所有的任务都完成的情况下才执行后续的任务

```
 var promise1 = new Promise(function(resolve, reject) {
            setTimeout(resolve, Math.random() * 1000, 'one');
        });

        var promise2 = new Promise(function(resolve, reject) {
            setTimeout(resolve, Math.random() * 1000, 'two');
        });

        Promise.race([promise1, promise2]).then(function(value) {
            console.log(value);
        });
```
> 案例

```
  button.onclick = function() {
            var str = 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526556435561&di=c3e2990ffd8a81d94f6e54fc90a06ad6&imgtype=0&src=http%3A%2F%2Fdl.bizhi.sogou.com%2Fimages%2F2013%2F08%2F01%2F354304.jpg';
            var str1 = 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526557331532&di=b57cee6aab2ff4d9459aee254ce75cf8&imgtype=jpg&src=http%3A%2F%2Fimg1.imgtn.bdimg.com%2Fit%2Fu%3D226758481%2C407956965%26fm%3D214%26gp%3D0.jpg';
            var str2 = 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526556435560&di=19d76c4d78cad26d814138447cfdd0a1&imgtype=0&src=http%3A%2F%2Fimg.xskup.com%2FfrontPage%2Fbg%2FbgFile%2F513%2F11.jpg';


            getImg([str, str1, str2]).then(imgs => {
                console.log(imgs);
            });

        };


        function getImg(urls) {
            var tasks = urls.map( url => {
                return new Promise( (resolve, reject) => {
                    // var img = document.createElement('img');
                    var img = new Image();  //等同上面

                    img.onload = function() {
                        resolve(img.width);
                    };
                    img.src = url;
                } );
            } );

            return Promise.all(tasks);
        }
```
####ES7新增异步处理，基于Promise
>  async/await-----------------await会等待async中的promise执行resolve方法时候才表示执行完成
* 可以在一个返回了Promise对象的函数前面加上 await 关键字，这样就不需要使用then了，但是await必须在一个异步的函数中进行调用

```
document.onclick = async function() {
            //var a = await fn(); //await会等待fn中的promise执行resolve方法时候才表示执行完成
        

            var str = 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526556435561&di=c3e2990ffd8a81d94f6e54fc90a06ad6&imgtype=0&src=http%3A%2F%2Fdl.bizhi.sogou.com%2Fimages%2F2013%2F08%2F01%2F354304.jpg';
            var str1 = 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526557331532&di=b57cee6aab2ff4d9459aee254ce75cf8&imgtype=jpg&src=http%3A%2F%2Fimg1.imgtn.bdimg.com%2Fit%2Fu%3D226758481%2C407956965%26fm%3D214%26gp%3D0.jpg';
            var str2 = 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1526556435560&di=19d76c4d78cad26d814138447cfdd0a1&imgtype=0&src=http%3A%2F%2Fimg.xskup.com%2FfrontPage%2Fbg%2FbgFile%2F513%2F11.jpg';

       
            var img = await getImg([str]);
            console.log(img);
            var img1 = await getImg([str1]);
            console.log(img1);
            var img2 = await getImg([str2]);
            console.log(img2);

        };



        function getImg(urls) {
            var tasks = urls.map( url => {
                return new Promise( (resolve, reject) => {
                    // var img = document.createElement('img');
                    var img = new Image();  //等同上面

                    img.onload = function() {
                        resolve(img.width);
                    };
                    img.src = url;
                } );
            } );

            return Promise.all(tasks);
        }
```
