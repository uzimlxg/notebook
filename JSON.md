## json
#### 什么叫Json
* 数据交换的格式，本质上是字符串，只是这个字符串借鉴了js中对象这样数据格式进行组织
* js提供了对JSON这种数据组织格式的解析
* 是存储和交换文本信息的语法。类似 XML。
* JSON 比 XML 更小、更快，更易解析。
* JSON 使用 JavaScript 语法来描述数据对象，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。
---
##### 语法规则
* 数据在名称/值对中
* 数据由逗号分隔
* 花括号保存对象
* 方括号保存数组
* key必须使用双引号

-  JSON 名称/值对
    - 名称/值对包括字段名称（在双引号中），后面写一个冒号，然后是值："firstName" : "John"
 >  JSON 对象
```
        -  JSON 对象在花括号中书写：
        -  对象可以包含多个名称/值对：
            { "firstName":"John" , "lastName":"Doe" }
            这一点也容易理解，与这条 JavaScript 语句等价：
            firstName = "John"
            lastName = "Doe"
```

    
    
    
>   JSON数组

```
         -JSON 数组在方括号中书写：
        "employees": [
        { "firstName":"John" , "lastName":"Doe" },
        { "firstName":"Anna" , "lastName":"Smith" },
        { "firstName":"Peter" , "lastName":"Jones" }
        ]
        在上面的例子中，对象 "employees" 是包含三个对象的数组。每个对象代表一条关于某人（有姓和名）的记录。
    
```

> JSON在javascript中的使用语法

```
var employees = [
{ "firstName":"Bill" , "lastName":"Gates" },
{ "firstName":"George" , "lastName":"Bush" },
{ "firstName":"Thomas" , "lastName": "Carter" }
];

1.可以像这样访问 JavaScript 对象数组中的第一项：
    employees[0].lastName;//返回的内容是：Gates
2.可以像这样修改数据：   
    employees[0].lastName = "Jobs";

```
---
##### JSON使用
> 把 JSON 文本转换为 JavaScript 对象
- JSON 最常见的用法之一，是从 web 服务器上读取 JSON 数据（作为文件或作为 HttpRequest），将 JSON 数据转换为 JavaScript 对象，然后在网页中使用该数据。
- 为了更简单地为您讲解，我们使用字符串作为输入进行演示（而不是文件）。

> 怎样操作json
* 我们可以通过js提供的一个JSON对象来操作这样的数据
* JSON.parse()
* 把JSON解析成对象/数组
* JSON.stringify()
* 把对象/数组解析成JSON

```
JSON转对象/数组
var json3 = '{"x": 1}';
var json4 = '{"a":1,"b":"miaov","c":true,"d":null,"e": undefined}';//JSON不接收undefined值
var json5 = '[1,"miaov",true, {"x": 100}]';

console.log(JSON.parse( json3 ));
console.log(JSON.parse( json4 ));
console.log(JSON.parse( json5 ));

对象/数组转成JSON
 var obj1 = {
             x: 1,
             y: true,
             z: undefined,
             arr: ['a','b','c', {username:'张三'}]
         };
 var json6 = JSON.stringify(obj1);
 console.log(json6);
```





