# JS

JS高级知识  尚硅谷讲解

- [b站：JS高级知识](https://www.bilibili.com/video/av46266343?p=2)

看视频整理要点笔记:

----

- hello-Js
    - 1.JS数据类型
    - 2.兼容性（ES2015）
    - 3.变量
    - 4.函数——箭头函数
    - 5.函数的参数
    - 6.解构赋值
    - 7.数组
    - 8.字符串
    - 9.ES6的面向对象
    - 10.面向对应用——react
    - 11.json
    - 12.Promise
    - 13.generator-基础
    - 14.generator-yield是啥
    - 15.generator-实例
    - 16.ES7 预览

----

## 1.JS数据类型
- 分类
  - 基本类型
    - string:任意字符串
    - number任意数字
    - boolean::true/false
    - null:null
    - undefined:undefined
  - 对象类型
    - object:任意对象
    - function:一种特别的对象（可执行） 
    - Array:一种特别的对象（数组下表，内部数据是有序的）
- 判断
  - typeof
    - 可以判断：string、number、boolean\function
    - 不可判断：null与object，object与Array
  - ===
      - 可以判断：undefinded、null
  - instanceof
    - 判断对象的具体类型
```js
var b1={
  b2:[1,'ab',console.log],
  b3:function(){
  console.log(2);
  }
}
console.log(b1 instanceof object,b1 instanceof Array); // true false
cosole.log(b1.b2 instanceof Array,b1.b2 instanceof object); //true true
console.log(b1.b3 instanceof Function,b1.b3 instabceof object); //true true
console.log(typeof b1.b2); //object
console.log(typeof b1.b3==='function')
console.log(typeof b1.b3[2]==='function')

var a
console.log(a,typeof a,typeof a==='undefined',a===undefined) //undefined 'undefinded' true true
```
- undefinded与null的区别？
  - undefinded代表定义为赋值
  ```js
  var a
  console.log(typeof a) //undefinded
  ```
  - null定义并赋值，只是值为null
    ```js
  var a
  a = null
  console.log(typeof a) //null
  ```
- 什么时候给变量赋值为null?
  - 初始赋值，表明将要赋值为对象
  - 结束前，让对象成为垃圾对象（被垃圾回收器回收）
- 严格区别变量类型与数据类型
  - 数据类型
    - 基本类型
    - 对象类型
  - 变量的类型（变量内存值的类型）
    - 基本类型：保存的就是基本类型的数据
    - 引用类型；保存的是地址值
- 什么是数据？
  - 存储在内存中代表特定信息的东西，本质上是010101（二进制）
  - 数据的特点：可传递、可运算
  - 一切皆数据
  - 内存中的所有操作目标：数据
    - 算术预算
    - 逻辑运算
    - 赋值运算
    - 运行函数
- 什么是内存？
  - 内存条通电后产生的看存储数据的空间（临时的）
  - 内存中长生和死亡：内存条（电路板）==>通电==>产生内存空间==>处理数据==>断电==>内存空间和数据都小时
  - 一块内存的2个数据
    - 内存存储的诗句
    - 地址值
  - 内存分类
    - 栈：全局变量、局部
    - 堆：对象
- 什么是变量
  - 可变化的量，由变量名和变量值组成
  - 每个变量丢对应一小块内存，变量名用来查找对应的内存，变量值就是内存中保存的数据
- 内存、数据、变量三者之间的关系
  - 内存是用来存储数据的空间
  -变量是内存的标识
- var a = xxx，a内存中到底保存的是什么？
  - xxx是基本数据，保存的就是你这个数据
  - xxx是对象，保存的是对象地址值
  - xxx是一个变量，保存的xxx的内存内容（可能是基本数据，也可能是地址值）
- 关于引用变量赋值的问题
  - 2个引用变量指向同一个对象，通过一个变量修改对象内部数据，另一个变量看到的是修改之后的数据
  - 2个引用变量指向的同一个对象，让其中一个引用变量指向另一个对象，另一个应用变量依然指向前一个对象
- 在js调用函数时，是值传递还是引用传递
  - 理解1：都是值（基本/地址值）传递
  - 理解2：可能是指传递，也可能是引用传递（地址值）
- js引擎如何管理内存
  - 内存生命周期
    - 分配小内存空间，得到它的使用权
    - 存储数据，可以反复进行操作
    - 释放小内存空间
  - 释放内存
    - 局部变量：函数执行完自动释放
    - 对象：成为垃圾对象==>垃圾回收器回收
- 什么是对象？
  - 多个数据的封装体
  - 用来保存多个数据的容体
  - 一个对象代表现实中的一个事物
- 为什么要用对象？
  - 统一管理多个数据
- 对象的组成
  - 属性：属性名（字符串）和属性值想组成
  - 方法：一种特别的属性
- 如何访问对象内存的数据？
  - .属性名  编码简单，有事不能用
  - ['属性名']  编码麻烦，能通用
```js
    var p ={
    name:'Tom',
    age:12,
    setName:function(name){
        this.name = name
     },
     setAge.function(age){
     this.age = age}
    }
    p.setName('Bob')
    p['setAge'](12)
    console.log(p.name,p['age']
    )
```
- 什么时候必须使用['属性名']的方式
  - 属性名包含特殊字符：- 空格
  - 变量名不确定
  
  ```js
  var p = {}
  //1、给p对象添加一个属性：content type:text/json
  //p.content-type = 'text/json'//不能用
  p['content-type'] = 'text/json'
  
  //2、变量名不确定
  var propName = 'myAge'
  var value = 18
  //p.proName = value
  p['proName'] = value
  console.log(p[propName])//18
  
  ```
- 函数
  - 什么是函数
    - 实现特定功能的n条语句的封装体
    - 只有函数是可以执行的，其他类型数据是不能执行的
  - 为什么要使用函数
    - 提高代码复用性
    - 便于阅读交流
  - 如何定义函数
    - 函数声明
    - 表达式
  - 如何调用函数（执行）函数？
    - text（）：直接调用
    - obj.test():通过对象调用
    - new test():new调用
    - test.call/apply(obj):临时让test成为obj的方法进行调用
```js
function fn1(){ 、、函数声明

}
var fn2 = function(){
}//表达式


```

-  什么函数是回调函数？
  - 经过定义的
  - 没有调用的
  - 最终执行了的
- 常见的回调函数
  - dom事件回调函数
  - 定时器回调函数
  - ajax请求回调函数（后面讲）
  - 生命周期回调函数（后面讲） 
  ```js
  
  <button id="btn" >点击</button>
  <script>
    document.getElementById('btn').onclick = function(){  //dom事件的回调函数
    alert(this.innerHTML)}
    //定时器回调
    //超市定时器
    //循环定时器
    setTimeout(function(){  //定时器回调
    alert('到时间了')}，2000)
  </script>
  ```
- IIFE
  - 全称
    - Immediatly-Invoked Function Expression
  - 作用
    - 隐藏实现
    - 不会污染外部环境
    - 用它来编写js模板
  ```js
  (function(){ //匿名函数自调用
  var a = 3;
  console.log(a+3);
  })()
  console.log(a)
  (function(){
  var a =1;
  function test(){
  console.log(++a);}
  window.$ = function(){ //向外暴露一个全局函数
    return {
        test:test
     }
  }
  }){}
  $().test() //1.$是一个函数 2.$执行后返回的是一个对象
  ```
  
   
  

 
    
    
 
    
## 2.兼容性（ES2015）
- ES6(ES2015)
    - IE10+
    - Chrome
    - FireFox
    - 移动端
    - NodeJS
- 解决不兼容的办法:编译、转换
    - 在线转换
    - 提前编译
- Babel编译器
    - Babel是一个JavaScript的编译器
    - 一个广泛使用的转码器，能将ES6代码转换为ES5代码，使得能做现在的环境运行
    - 使用后，就不用担心ES6不兼容问题
## 3.变量
- var
    - 可以重复申明变量
    - 无法限制修改
    - 没有块级作用域
- let
    - 不能重复申明
    - 变量——可以修改
    - 块级作用域
- const
    -不能重复申明变量
    - 常量——不能修改
    - 块级作用域
    
## 4.函数——箭头函数
- 若只有一个参数，（）可以省
- 若只有一个return，{}可以省

## 5.函数的参数
- 参数扩展/数组展开
    - 收集参数
```js
 function show(a,b, ...args){}
 *Rest parameter必须是最后一个
```
   - 展开数组
```js
  ...arr   =>   1,2,3
 *展开后的效果，跟直接把数组的内容写在这儿一样
```
- 默认参数
   - 你给我设置值，那我接收，不设置值，我自己默认也有值
```js
 $('#div1').animate({width:'200px'})
 $('#div1').annimate({width:'200px'},1000)
```

## 6.解构赋值
- 左右两边结构必须一样
- 右边必须是个东西
- 声明和赋值不能分开（必须在一句话里完成）

## 7.数组
- map——映射（一个对一个）
    - [43,65,76,46,36,98,67,87,76,74,63]
    - [不及格,及格,及格,不及格,不及格,及格,及格,及格,及格,及格,及格]
- reduce——汇总（一堆中出现一个，算总数）
    - [2,3,4]
    -[9]
- filter——过滤器
- forEach——循环（迭代）

## 8.字符串
- 新方法
    - startsWith
    - endswith
- 字符串模板
    - 可以直接把东西塞到字符串里面    ${a}
    - 可以折行
  
## 9.ES6的面向对象
- class关键字，构造器和类分开了
- class里面直接加方法

## 10.面向对应用——react
 - 用于构建用户界面的 JavaScript 库
 - 组件化，一个组件就是一个 class
 - JSX == bable == browser.js
 
## 11.json
- JSON 对象
    - 对象（object）
    - 是 JavaScript 语言的核心概念，也是最重要的数据类型
    - 对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合
    - 对象的所有键名都是字符串, 所以加不加引号都可以
    - 如果键名是数值，会被自动转为字符串
    - 对象的每一个键名又称为“属性”（property），它的“键值”可以是任何数据类型
    - 如果一个属性的值为函数，通常把这个属性称为“方法”，它可以像函数那样调用
    - in 运算符用于检查对象是否包含某个属性（注意，检查的是键名，不是键值
    - for...in循环用来遍历一个对象的全部属性

- 对象 简写
    - key-value 一样时可以简写
    - 里面函数可以简写, 去掉
- 简写
    - 名字和值（key和vuale）一样的，只留一个
    - 方法 :function可以删
         - show :fucntion(){}
         - show(){}     
- Json标准写法
    - 只能用双引号
    - 所有的名字必须用应该抱起来
    - {"a":12,"b":34}
     
## 12.promise
- 异步：操作之间没有关系，同时进行多个操作
```js
ajax('/banners',function(banner_data){
    ajax('/hot',function(hot_data){
        ajax('dog',function(dog_data){
             ajax('cat',function(cat_data){
        
            },function(){
                alert("失败了");
            });
        },function(){
            alert("失败了");
        });
        
      },function(){
           alert("失败"）;
      });
     },function(){
        alert("失败了");
    });                   
```
- 异步：同时只能做一件事
```js
let banner_data =ajax_async("/banner");
let hot_data =ajac-async("/hot");
let dog_data =ajac-async("/dog");
let cat_data =ajac-async("/cat");
```
- prmise.all
    - 用消除异步一样的方式，来书写异步代码
    - 有了promise后的异步
```js
Promise.all([$.ajax(),$.ajax(),$.ajax()]).then(results={
    //对了
},err=>{
    //错了
});
```
- prmise.race(竞速)
   - Promse.race就是赛跑的意思
   - 哪个结果获得的快，就返回那个结果
   - 不管结果本身是成功状态还是失败状态
```js
Promise.race([
 $.ajax({url:'http://baidu.ww.com'});
 $.ajax({url:'http1://baidu.ww.com'});
 $.ajax({url:'http2://baidu.ww.com'});
 $.ajax({url:'http3://baidu.ww.com'});
 ]};

```
## 13.generator-基础
- 普通函数，一路运行到底，不能停
- generator，运行的中间可以停止，到哪停呢，用 yield 配合，交出执行权
- yield 有 放弃、退让、退位的意思
- 需要调用next()方法启动执行，需要遇到 yield 停, 踹一脚走一步
- generator函数前面加一个 `*` 两边可以有空格，或靠近函数或`function`
- 背后实际生成多个小函数，实现走走停停

## 14.generator-yield是啥
- `yield`
    - 既可传参，又可以返回
    - 第一个`next()`传参无效，只用来启动

- 如果函数前漏掉 `*`
    - 就是普通函数
    - 如果有`yield`会报错， `ReferenceError: yield is not defined`
    - yield 只能在Generator函数内部使用

```js
function * show() {
    console.log('1')
    var a = yield
    console.log('2')
    console.log(a)
}
// yield 传参
function* show2() {
    console.log('1')
    yield 10
    console.log('2')
}
var gen = show()
gen.next() // 1
gen.next() // 2 和 undefined 因为没有传参，yield没有返回值
var gen = show()
gen.next(10) // 1 第一次执行到yield，但没有执行赋值
gen.next(20) // 2 和 20

// yield 返回
var gen = show2()
var res1 = gen.next()
console.log(res1) // { value: 10, done: false }
var res2 = gen.next()
console.log(res2)
// { value: undefined, done: true } 最后的value需要return返回
```

## 15.generator-实列
- Promise 适合一次读一组
- generator 适合逻辑性的
```js
//带逻辑-generator
runner(function *(){
let userData = yield $.ajax({url:'getUserData',dataType:'json'});
if(usrData.type=='VIP'){
    let item = yield $.ajax({url:'getVIPItems',dataType:'json'});
    }else{
    let item = yield $.ajax({url:'getItems',dataType:'json'});
    }
    //
})
```

```js
// yield 实例，用同步方式写异步
    const koa =require('koa');
    const mysql = require('koa-mysql');
    let db = mysql.craetePool({host:'localhost',user:'root',password:'',database;''});
    let server = new koa();
    server.use(function *(){
    let data = yield db.query(`SELECT * From user_table`);
    this.body = data;
    });
    server.listen(8080);
```
## 16.ES7 &ES8 预览 
- 数组-include
   - 判断你数组数组是否包含某个东西
- 数组  key/values/entries
    - key=>所有的key拿出来
    ```js
      let arr = [3,5,8,43];
      for(let key of arr.keys()){
        alert(key);
      }//key输出值为0,1,2,3
    ```
   - values=>所有的values拿出来
   - entries=>所有的键值对拿出来
    ```js
        let arr = [3,5,8,43];
        for(let entries of arr.entries()){
          alert(entries);
        }//entries输出值为0,3;1,5;2,8;3,43
    ```
    
   - for...in————循环的东西是数组(json)的下表（key）
    ```js
      let arr = [1,5,6,9,6];
      for(let i in arr){
        alert(i);
      }//i输出值为0，1,2,3,4
      
      //json
      let json = {a:1,b:5,c:6,d:9,e:6};
      for(let i in json){
        alert(i);
      }//i输出值为a,b,c,d,e
    ```
   - for...of————循环的东西是数组(json对象是个不可迭代的对象，for...of不能用于json)的值（values）
      ```js
       let arr = [1,5,6,9,6];
        for(let i of arr){
            alert(i);
        }//i输出值为1,5,6,9,6
      ```
- 幂
   -求幂
 ```js
   alert(Math.pow(3,5));//以前
   alert(3**5);//现在
 ```
 - startsWith/endsWIth
 - padStart/padEnd(从开始的位置取5是内容不够，在前面补空格/从开始的位置取5位，要是内容不够，在前面补空格
 ```js
  console.log('a43'.padStart(从开始的位置取8（自定义）位，要是内容不够，在前面补空格/8
  console.log('a43'.padEnd(8));
 ```
- 语法容忍度
    -数组，函数参数后面多一个逗号可以忍
    
- async await
    - 不依赖于外部runner
    - 可以使用箭头函数
```js
  let reaData = async()=>{
      let data1 = await $.ajax({url:'arr.txt',dataType:'json'});
      let data2 = await $.ajax({url:'arr2.txt',dataType:'json'});
      let data3 = await $.ajax({url:'arr3.txt',dataType:'json'});
      // console.log(data1,data2,data3);
    }
    reaData();
```
