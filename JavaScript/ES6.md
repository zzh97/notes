#### 1 let和const

##### 1.1 let

var是函数级作用域，而let是块级作用域

```javascript
// 打印出0-4
for (var i=0; i<5; i++) {
	console.log(i)
}
// 打印出5
console.log(i)

// 打印出0-4ja
for (let j=0; j<5; j++) {
	console.log(j)
}
// 报错：j is not defind
console.log(j)
```



当let的作用域结束时，便会寻找同名的var作用域

```javascript
<script>
// 打印出0-4
for (var i=0; i<5; i++) {
	console.log(i)
}
// 打印出5
console.log(i)

// 打印出0-4
for (let i=0; i<5; i++) {
	console.log(i)
}
// 打印出5（当let的作用域只在for中）
console.log(i)
</script>
```



将被let声明的变量，不能被使用（即无默认值undfined）

```
console.log(a) // undefined
var a = 'a'
console.log(b) // 报错：ReferenceError
let b = 'b'
```

注：这意味着它不能typeof



且let也不能重复声明

```javascript
var a = 'a'
var a = 'a2'
console.log(a) // 打印出a
let b = 'b'
let b = 'b2'
console.log(b) // 报错：has already been declared
```

注：上述做法皆是为了弥补Javascript的随意性



ES6允许在块内定义函数（ES5理论上不允许），且函数作用域会提升至该块的头部（即可以先调用后定义）

```javascript
if (true) {
    f() // 打印出f
    function f () {
        console.log ('f')
    }
}
```



总所周知，在Javascript中，顶层对象（window）里的属性与方法是可以直接使用的

而var声明其实就是把该变量绑定到了顶层对象中，但let不会这么做

```javascript
window.a = 1
console.log (a) // 打印出1

var b = 2
console.log (window.b) // 打印出2

let c = 2
console.log (window.c) // undefined
```

注：this指针就是为了方便取到上级对象而出现的

```javascript
console.log (this == window) // 打印出true

var a = {
    b: function () {
        console.log (this == a)
    }
}
a.b() // 打印出true
```



##### 1.1 const

const声明一个只读的常量，声明后不可改变其值

```javascript
const a = 1
a = 2 // 报错：Assignment to constant variable.
```



这也意味着，const声明时，一定要初始化

```javascript
const a // 报错：Missing initializer in const declaration
```



const与let作用域相同

```javascript
if (true) {
    const a = 1
}
console.log (1) // 报错：b is not defined
```



【重点】const的本质其实是保证地址不变（而非值不变），只是对于简单数据类型，表现出来的是值不变

```javascript
let a = 1 // 把1的地址赋给a
const b = a // 把a的地址赋给b
console.log(a, b) // 此时a=1，b=1
a = 2 // 把2的地址赋给a
console.log(a, b) // 此d时a=2，b=1（b指向的还是1的地址）

const c = {d: 3} // 把3的地址赋给d，并把d添加到{}中，最后把{}的地址赋给c
console.log (c.d) // 打印出3
c.d = 4 // 不会报错（因为只改变了d的指针/引用，而c仍指向{}）
console.log (c.d) // 打印出4

c.e = 5 // 不会报错（因为c仍指向{}）
console.log (c.e) // 打印出5
```



如果想要复杂数据类型也保证其值不变，可以这么做

```javascript
const c =  Object.freeze({d: 3}) // 冻结对象
c.d = 4 // 该行代码不会生效
console.log (c.d) // 打印出3
```

在严格模式下会报错

```javascript
"use strict" // 开启严格模式
const c =  Object.freeze({d: 3}) // 冻结对象
c.d = 4 // 报错：Cannot assign to read only property
```



#### 2 解构赋值

##### 2.1 数组式与对象式

先来看看它的基本用法

```javascript
// 普通赋值
let a = 1, b = 2
console.log (a, b) // 打印出1和2

// 解构赋值
let [c, d] = [3, 4]
console.log (c, d) // 打印出3和4
```

注：这种方式被称为数组式解构赋值



除此之外，还有对象式解构赋值

```javascript
// 不按顺序，靠键匹配
let { a, b } = { b: 2, a: 1 }
console.log (a, b) // 打印出1和2
```



解构赋值可以有默认值

```javascript
let [a = 1, b = 2] = []
console.log (a, b) // 打印出1和2

let { c = 3, d = 4 } = {}
console.log (c, d) // 打印出3和4
```



##### 2.2 圆括号与字符串

已声明的变量进行解构赋值，要小心

```javascript
let a, b
[a, b] = [1, 2]
console.log (a, b) // 打印出1和2
```

这个是没问题的，但这样是有问题的

```javascript
let a, b
{ a, b } = { a: 1, b: 2 } // 报错
```

想要用对象式，应该这样写

```javascript
let a, b
({ a, b } = { a: 1, b: 2 })
console.log (a, b) // 打印出1和2
```

注：圆括号是ES6为了处理`{x}`到底是解构赋值还是块里有个x，从而引入的符号



由于在JavaScript中String其实就是Array，所以我们也可以这么做

```javascript
let [a, b, c] = 'abc'
console.log (a, b, c) // 打印出a b c

let {length: len} = 'abc'
console.log (len) // 打印出3
```



##### 2.3 函数与分号问题

解构赋值可以使用在函数的参数和返回值中

```javascript
let f = function ([a, b]) {
    return [a+b, a-b]
}

let [c, d] =  f([1, 2])
console.log (c, d) // 打印出3和-1
```



需注意，虽然解释器会自动补分号，但在有二义性的情况下就不会

```javascript
let f = function (num) {
    return num
}

let a = f
(1)
console.log (a) // 打印出1

let b = f;
(1)
console.log (b) // 打印出ƒ (num) { return num }
```

所以，在解构赋值的时候，这么些也是错的

```javascript
let a = 1, b = 2
[a, b] = [b, a]
```

而要写成

```javascript
let a = 1, b = 2;
[a, b] = [b, a]
```

哎，所以以后最好还行加上分号吧（也利于代码压缩）

注：当然也有例外，比如return

```javascript
let a = function () {
    // 实际上是return;（return后会自动加分号）
    return 
    {
        b: 1
    }
}
console.log (a()) // undefined
```



##### 2.4 用处

变量置换

```javascript
// 这边结尾一定要加分号（原因见上方）
let a = 1, b = 2;
console.log (a, b); // 打印出1和2
[a, b] = [b, a]
console.log (a, b) // 打印出2和1
```



对于函数的扩展

```javascript
// 可以设置默认值
var f = function ({ a=1, b }) {
    return { a2: a * 2, b2: b * 2 };
}

// 可以无序
let { b2, a2 } = f({ b: 2})
console.log(a2, b2) // 打印出2和4
```



提取 JSON 数据

```
let josn = {
    a: 1,
    b: 2
}

let {a, b} = josn
console.log (a, b) // 打印出1和2
```



#### 3 字符串

##### 3.1 遍历

现在可以用for..of / for...in来变量String

```
// 打印出a b c d
for (let char of 'abcd') {
    console.log (char)
}

// 打印出0 1 2 3
for (let index in 'abcd') {
    console.log (index)
}
```

注：for..of遍历元素，for..in遍历下标，forEach只能用于数组且不能break和return



##### 3.2 模板

反引号中可以套公式，也可以写多行

```
let id = 1
console.log ('id: ' + id) // 打印出id: 1

id = 2
console.log (`id: ${id * 2}`) // 打印出id: 2 4

// 打印出
// 醉卧沙场君莫笑，
// 古来征战几人回。
console.log (`醉卧沙场君莫笑，
古来征战几人回。`) 
```



##### 3.3 新增方法

新增了includes方法，可以用来代替indexOf（某些情况）

还新增了repeat方法，用于复写

```
let a = 'abc'
console.log (a.indexOf('b')) // 打印出1
console.log (a.includes('b')) // 打印出true
console.log (a.repeat(3)) // 打印出abcabcabc
```



对ES5中的trim方法进行了扩展

```
let a = '  abc  '
a.trim() // 打印出"abc"
a.trimStart() // 打印出"abc  "
a.trimEnd() // 打印出"  abc"
```



#### 函数

参数与返回值（不在使用arguments）

箭头函数（this问题，不能new，即当作构造函数）

函数内严格模式

name

ES7参数最后可有逗号

ES9 catch可不要参数



#### 数组

[...array]（展开和值复制）

[...arr1, ...arr2] （取代concat，数组合并）

findIndex flat includes



#### 对象

class 继承 装饰器



#### 异步

##### Promise

由于异步函数的存在，比如获取远程的资源（受网络、资源大小等因素影响）

使得不同的异步函数，返回的时间也不同

```
let getA = (next) => {
    let data = 'A'
    setTimeout(() => {
        next(data)
    }, 500)
}

let getB = (next) => {
    let data = 'B'
    setTimeout(() => {
        next(data)
    }, 400)
}

let getC = (next) => {
    let data = 'C'
    setTimeout(() => {
        next(data)
    }, 300)
}

// 我想要ABC，但打印出CBA
getA(data => {
    console.log(data)
})

getB(data => {
    console.log(data)
})

getC(data => {
    console.log(data)
})
```



故，想要使它们安装指定的顺序执行（先穿袜子再穿鞋）

便要回调嵌套，这就导致了回调地狱

```
let getA = (next) => {
    let data = 'A'
    setTimeout(() => {
        next(data)
    }, 500)
}

let getB = (next) => {
    let data = 'B'
    setTimeout(() => {
        next(data)
    }, 400)
}

let getC = (next) => {
    let data = 'C'
    setTimeout(() => {
        next(data)
    }, 300)
}

// 打印出ABC，却出现回调地狱（代码丑）
getA(data => {
    console.log(data)
    getB(data=>{
        console.log (data)
        getC (data=>{
            console.log (data)
        })
    })
})
```



为了解决回调地狱，Promise诞生了

```
const promise = new Promise((resolve, reject) => {
    // treu自行替换成条件
    if (true) {
        // 成功后
        resolve(value)
    } else {
        // 失败后
        reject(value)
    }
})
```



用Promise改造getA/B/C

```
let getA = () => {
    return new Promise((resolve, reject) => {
        let data = 'A'
        setTimeout(() => {
            resolve(data)
        }, 500)
    })
}

let getB = () => {
    return new Promise((resolve, reject) => {
        let data = 'B'
        setTimeout(() => {
            resolve(data)
        }, 400)
    })
}

let getC = () => {
    return new Promise((resolve, reject) => {
        let data = 'c'
        setTimeout(() => {
            resolve(data)
        }, 300)
    })
}

// then方法返回的是一个新的Promise，故可采用链式写法
let a = getA()
.then((data) => {
    console.log (data)
    return getB()
})
.then((data) => {
    console.log (data)
    return getC()
})
.then((data) => {
    console.log (data)
})
```



##### Generator

##### async 



#### 模块

import export