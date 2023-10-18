# mianshi
面试问题记录
### 自我介绍

### js数据类型
基本数据类型：string、boolean、number、null、undefined、symbol、bigint<br/>
引用数据类型：Object、Array、function
### react状态管理工具
React-redux:store action reducer state store.getState store.dispatch provider content
<br />
1. 单一数据源
2. state只读
3. 使用纯函数进行更改

### new构造符做了什么
1. 创建一个新对象
2. 将构造函数的作用域赋值给新对象（这样this就指向了新对象）
3. 执行构造函数中的代码（为新对象添加实例属性和实例方法）
4. 返回新对象

### 开发中遇到的问题
1. 防抖、节流 输入搜索
2. 移动刘海屏适配问题 css 浏览器安全距离
3. 图片懒加载 oss平台 图片链接拼接参数  图片压缩
4. 代码风格统一  eslint  
5. 线上问题定位    埋点上报
6. 前端页面存在的安全漏洞，如 XSS 、CSRF 攻击等。 转译escapeHTML() 防止 HTML 中出现注入。输入内容长度控制、HTTP-only Cookie: 禁止 JavaScript 读取某些敏感 Cookie，攻击者完成 XSS 注入后也无法窃取此 Cookie。

### 受控组件 非受控组件

### 如何实现组件懒加载
16.6.0 react提供lazy方法 Suspense
这个方法的原理和缺陷
``` 
import React, { lazy, Suspense } from 'react';
const OtherComponent = lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <OtherComponent />
    </Suspense>
  );
}
```
### http1.1和http2.0
### css文档流
### css优化
1. 内联首屏关键css
2. 异步加载css
3. 文件压缩
4. 去除无用css
5. 有效使用选择器 保持简单，不要使用嵌套过多过于复杂的选择器。
6. 通配符和属性选择器效率最低，需要匹配的元素最多，尽量避免使用。
7. 不要使用类选择器和ID选择器修饰元素标签，如h3#markdown-content，这样多此一举，还会降低效率。
8. 不要为了追求速度而放弃可读性与可维护性
9. 避免不必要的重绘
10. 不要使用@import

### 浏览器标签页通信
localStorage、cookie、sharedWork、websocket
### this指向问题
This指向混乱 This严格模式下 指向undefined

### webpack
入口 出口、loader、plugin、devserver    entry、output
### 路由
react-router hash模式 history模式  replaceState popState等跳转方法    路由传参 动态传参 缓存 redux
路由拦截
### 数组去重方法
set、indexOf、sort、filter
### ES6新特性
1. 解构赋值
2. 数组解构
3. 对象解构
4. 模版字符串
5. 箭头函数
6. let const
7. symbol(表示独一无二的值 基本数据类型)
8. padStart、padEnd、数组的新方法（map、set、includes、foreach、some、every）
9. 对象拓展符
10. promise和proxy、async await
### promise三种状态
pending、resolve、reject
### 防抖节流
### 改变原数组的方法
1. pop(); 用于删除并返回数组最后一个元素 ...
2. push(); 向数组末尾添加一个或多个元素，并返回新的长度 ...
3. shift(); 删除并返回第一个元素的值 ...
4. unshift(); 向数组的开头添加一个或更多元素，并返回新的长度 ...
5. reverse(); 颠倒数组元素中的顺序 ...
6. sort(); 排序
### 如何判读一个空对象
1. JSON.stringify() 
2. for…in循环 
3. Object.getOwnPropertyNames()
4. Object.keys()  
5. 使用Object.entries()方法。 它返回一个包含对象的可枚举属性的数组。 如果它返回一个空数组
### 如何判断是一个对象
1. Object.prototype.tostring.call(obj) === '[object object]'
2. Object.constructor === Object
3. Instanceof
### 对象继承有哪些方式
1. 原型链继承
2. 借用构造函数继承
3. 实例继承
4. 组合继承：调用父类构造函数，继承父类的属性，通过将父类实例作为 子类原型，实现函数复用
5. 寄生组合继承
6. es6继承 class
### typescript 问题
TypeScript 是 JavaScript 的类型的超集，支持ES6语法，支持面向对象编程的概念，如类、接口、继承、泛型等
其是一种静态类型检查的语言，提供了类型注解，在代码编译阶段就可以检查出数据类型的错误
同时扩展了JavaScript 的语法，所以任何现有的JavaScript 程序可以不加改变的在 TypeScript 下工作

+ 类型批注和编译时类型检查 ：在编译时批注变量类型
+ 类型推断：ts 中没有批注变量类型会自动推断变量的类型
+ 类型擦除：在编译过程中批注的内容和接口会在运行时利用工具擦除
+ 接口：ts 中用接口来定义对象类型
+ 枚举：用于取值被限定在一定范围内的场景
+ Mixin：可以接受任意类型的值
+ 泛型编程：写代码时使用一些以后才指定的类型
+ 名字空间：名字只在该区域内有效，其他区域可重复使用该名字而不冲突
+ 元组：元组合并了不同类型的对象，相当于一个可以装不同类型数据的数组
### 数组的方法
+ concat()	连接两个或更多的数组，并返回结果。
+ copyWithin()	从数组的指定位置拷贝元素到数组的另一个指定位置中。
+ entries()	返回数组的可迭代对象。
+ every()	检测数值元素的每个元素是否都符合条件。
+ fill()	使用一个固定值来填充数组。
+ filter()	检测数值元素，并返回符合条件所有元素的数组。
+ find()	返回符合传入测试（函数）条件的数组元素。
+ findIndex()	返回符合传入测试（函数）条件的数组元素索引。
+ forEach()	数组每个元素都执行一次回调函数。
+ from()	通过给定的对象中创建一个数组。
+ includes()	判断一个数组是否包含一个指定的值。
+ indexOf()	搜索数组中的元素，并返回它所在的位置。
+ isArray()	判断对象是否为数组。
+ join()	把数组的所有元素放入一个字符串。
+ keys()	返回数组的可迭代对象，包含原始数组的键(key)。
+ lastIndexOf()	搜索数组中的元素，并返回它最后出现的位置。
+ map()	通过指定函数处理数组的每个元素，并返回处理后的数组。
+ pop()	删除数组的最后一个元素并返回删除的元素。
+ push()	向数组的末尾添加一个或更多元素，并返回新的长度。
+ reduce()	将数组元素计算为一个值（从左到右）。
+ reduceRight()	将数组元素计算为一个值（从右到左）。
+ reverse()	反转数组的元素顺序。
+ shift()	删除并返回数组的第一个元素。
+ slice()	选取数组的一部分，并返回一个新数组。
+ some()	检测数组元素中是否有元素符合指定条件。
+ sort()	对数组的元素进行排序。
+ splice()	从数组中添加或删除元素。
+ toString()	把数组转换为字符串，并返回结果。
+ unshift()	向数组的开头添加一个或更多元素，并返回新的长度。
+ valueOf()	返回数组对象的原始值。
+ Array.of()	将一组值转换为数组。
+ Array.at()	用于接收一个整数值并返回该索引对应的元素，允许正数和负数。负整数从数组中的最后一个元素开始倒数。
+ Array.flat()	创建一个新数组，这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成。
+ Array.flatMap()	使用映射函数映射每个元素，然后将结果压缩成一个新数组。