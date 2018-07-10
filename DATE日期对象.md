###Dater日期对象
> 日期对象用于处理日期和时间

> 创建Date对象的方式

* var d=new Date();当前时间
    * d.getYear();获取当前年份（2位）
    * d.getFullYear();获取完整年份
    * d.getMouth();获取当前月份（0-11）
    * d.get.Date();获取当前日（1-31）
    * d.getDay();获取当前星期几（0-6，0代表星期天）
    * d.getTime();获取当前秒数（1970。1.1开始的毫秒）简称时间戳
    * d.getHours();获取当前小时数（0-31）
    * d.getMinutes();获取当前分钟数（0-59）；
    * d.getSeconds();获取当前秒数（0-59）
    * d.getMillseconds();获取当前毫秒数（0-999）
    * d.toLocaleDateString();获取当前日期，such as 2018/4/7
    * d.toLocaleString();获取当前时间
    such as 上午11:49:34
    * d.toLocaleString();获取当前日期与时间
* new Date(value);
* new Date(dateString);
* new Date(year, month[, day[, hour[, minutes[, seconds[, milliseconds]]]]]);
---
注意：
* Note: 需要注意的是只能通过调用 Date 构造函数来实例化日期对象：以常规函数调用它（即不加 new 操作符）将会返回一个字符串，而不是一个日期对象。另外，不像其他JavaScript 类型，Date 对象没有字面量格式。
* Note: 当Date作为构造函数调用并传入多个参数时，如果数值大于合理范围时（如月份为13或者分钟数为70），相邻的数值会被调整。比如 new Date(2013, 13, 1)等于new Date(2014, 1, 1)，它们都表示日期2014-02-01（注意月份是从0开始的）。其他数值也是类似，new Date(2013, 2, 1, 0, 70)等于new Date(2013, 2, 1, 1, 10)，都表示时间2013-03-01T01:10:00。
* Note: 当Date作为构造函数调用并传入多个参数时，所定义参数代表的是当地时间。如果需要世界协调时，使用 new Date({{jsxref("Date.UTC()", "Date.UTC(...)")}}) 和相同参数
* ---
> 属性
* Date.prototype
    * 允许为Date实例化对象添加属性
* Date.length
    * Date.length的值是7.这是构造函数可接受的参数个数
---
> 方法
* Date.now()
    * 返回自1970-1-1 00：00：00
UTC(世界标准时间)至今所经过的毫秒数
* Date.parse()
    * 解析一个表示日期的字符串，并返回从时间戳
* Date.UTC()
    * 接受和构造函数最长形式的参数相同的参数(从2-7)；时间戳
---
> Date实例
* 所有的 Date 实例都继承自 Date.prototype。修改 Date 构造函数的原型对象会影响到所有的 Date 实例。
- Date.prototype方法==Getter==读操作
    * d.getYear();获取当前年份（2位）
    * d.getFullYear();获取完整年份
    * d.getMouth();获取当前月份（0-11）
    * d.get.Date();获取当前日（1-31）
    * d.getDay();获取当前星期几（0-6，0代表星期天）
    * d.getTime();获取当前秒数（1970。1.1开始的毫秒）简称时间戳
    * d.getHours();获取当前小时数（0-31）
    * d.getMinutes();获取当前分钟数（0-59）；
    * d.getSeconds();获取当前秒数（0-59）
    * d.getMillseconds();获取当前毫秒数（0-999）
    * d.toLocaleDateString();获取当前日期，such as 2018/4/7
    * d.toLocaleString();获取当前时间
    such as 上午11:49:34
    * d.toLocaleString();获取当前日期与时间
- Date.prototype方法==Setter==写操作
    * d.setDate();设置对象中月的某一天(1-31)
    * d.setFullYear();设置对象中的年份(四位数字)
    * d.setHours();设置对象中的小时数(0-23)
    * d.setMilliseconds();设置对象中的毫秒
    * d.setMinutes();设置对象中的分钟数
    * d.setSeconds();设置对象中的秒钟(0-59)
    * d.setTime();设置Date对象

---
###  拓展
> 格式化时间format
* var testDate = new Date(); 
    * var testStr =testDate.format("yyyy年MM月dd日hh小时mm分ss秒"); 
    * //=> testStr =  2015年01月20日 19小时21分03秒
> ago  多少小时前，多少分钟前，多少秒前
* new Date(1421313395359).ago(1411430400000)
//=> "3个月前"


* new Date(1421313395359).ago('1987-04-03')
//=> "28年前"

* new Date('2010-02-02').ago('1987-04-03')
//=> "23年前"
> toHHMMSS
* 时间转换,倒计时 '毫秒'.toHHMMSS(输出格式)
这个是基于 String 原型扩展出来的
    * var dt = (new Date().getTime()).toString()
dt.toHHMMSS('hh时mm分ss秒') //=> 34时11分52秒
> TZC
* 解决因时区变更，导致显示服务器时间不准确
    * //服务端传入前端一般为秒，前端时间戳为毫秒所以要乘以1000
new Date(1434701732*1000).TZC(8)