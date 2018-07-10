### transform
> 改变、变形、变化
* rotate:旋转
    * transform: rotate(value<unit>)
    * unit : 角度、弧度、梯度、圆度
    * 使元素以某个坐标点为圆点进行旋转
    *  deg 角度: 一个圆周，总共是360角度
    *  rad 弧度：一个圆周，总共是2π弧度
    *  grad 梯度：一个圆周，总共是400梯度
    *  turn 圆周: 一个圆周，或者说一圈
    *   默认是以元素的中心点为基准点，沿着Z轴进行旋转
    
```
 transform: rotate(90deg);
            transform: rotate(1rad);
            transform: rotate(100grad);
            transform: rotate(.25turn);
           
            rotateX()
            rotateY()
            rotateZ()
```
* scale:缩放
    *  scale(number)
         * number：倍数
         * transform: scale(.5);
* skew:拉伸、斜切
    * skew(deg)
 
```
    transform: skew(30deg, 30deg);
    transform: skewX(30deg);
    transform: skewY(30deg);
```

* translate: 位移
    * translate(Number)
    
```
    transform: translate(100px);
    transform: translateX(100px);
    transform: translateY(100px);
    
    需要3d环境
     transform: translateZ(100px);
```
* 多个属性同时存在的顺序问题
    *  transform如果有多个属性同时存在，一定要注意书写和解析顺序后写的先解析，先写的后解析
    *    无论做何种形式的变化，中心店不会改变，除非手动设置
* transform-origin - 元素变换的基点
    * 设置元素变换时的基点，默认 50% 50% 0
    *  x轴和y轴的值可以是数字，也可以是关键字
        * 关键字 left、right、top、bottom、center
    * 如果 value 使用的是值，那么按照顺序来(x -> y -> z)
    *  如果value使用的是关键字，那么关键字定义的没有顺序，并且关键字的优先
> 3D
* transform-style: preserve-3d
    *  定义: 元素的子元素怎样在三维空间中呈现
    *  flat : 指定子元素位于此元素所在平面内。默认值
    *  preserve-3d : 指定子元素定位在三维空间内。
* perspective: value;景深
* perspective-origin: left top;视点
* backface-visibility: hidden;
    * visible表示背面可见，允许显示正面的镜像
    * hidden : 表示背面不可见

> transition
* 给数值类的样式，在其样式值发生变化时添加一个过渡动画
* 用法：
    * transition-property 
        * 要动画的属性，不是所有属性都支持过度效果（只有数值类的属性） all||none||[attr]
    * transition-duration
        * 动画持续时间 (s||ms)
    * transition-timing-function
        *  动画形式，可选，默认 ease
                        linear、ease、ease-in、ease-out、ease-in-out、cubic-bezier(n,n,n,n)

    * transition-delay
        * 动画延迟时间

> transitionend事件

 * transitionend - 过渡完成之后的事件
元素有多个样式进行过渡时，每条样式过渡完都会触发 transitionend
 * 兼容
 * Element.addEventListener('webkitTransitionEnd', callback)
 * Element.addEventListener('transitionEnd', callback)
 * Element.removeEventListener('webkitTransitionEnd', callback)
 * Element.removeEventListener('transitionEnd', callback)

```
 box.addEventListener('transitionend', function(e) {
            // console.log('transitionend');

            // e.propertyName => 当前这次过渡完成对应的属性
            // console.log(e.propertyName);

            // if (e.propertyName == 'height') {
            //     console.log('后续动作');
            // }

        });
```
---
### animation


```
 @keyframes name {
                keyframes-selector {
                    css-styles;
                }
            }
            keyframes-selector : 关键帧的关键字
                - form(0%) to(100%)
                - 0-100% 百分比形式

            keyFrames必须配合css中animation来进行动画

            animation: animation-name animation-duration animation-timing-function animation-delay animation-iteration-count animation-direction

                - animation-name
                    要调用的 keyframes 的名字

                - animation-duration
                    完成整个动画所需要的时间(ms||s)

                - animation-timing-function
                    运动形式

                - animation-delay
                    运动延迟时间

                - animation-iteration-count
                    设置动画的播放次数 (infinite||number)

                - animation-direction
                    控制是否应该轮流反向播放动画 (normal||alternate)


    配合JS做
    
            animation-play-state
                - 控制动画暂停或者播放 (paused||running)

            animation-fill-mode
                - 控制动画开始之前或者结束之后的状态
                    - forwards : 动画结束之后 停留在 100%位置
                    - backwards : 动画开始前 停留在0% 的位置
                    - both : 以上两者同时存在
                    
    animation - 动画事件
    
            animationStart 事件，在动画开始时执行
            animationEnd 事件，在动画结束时执行
            animationIteration 事件，动画重复播放时执行

```
---
### 不同动画形式的特点

* transition 使用起来最方便，但是动画过程不受控制，中间过程也不可监控，也不可以自己执行
    
* animation 比transition麻烦，可以加载完执行，动画过程一定程度上可以控制
动画函数，实现的过程麻烦，动画形式丰富，动画过程可控





