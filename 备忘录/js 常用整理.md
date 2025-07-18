#技巧 #javascript #js

### toLocaleString()

```ad-note 
title: 介绍
- toLocaleString() 方法返回这个数字在特定语言环境下的表示字符串。
- 语法：`numObj.toLocaleString([locales [, options]])`
```

```js
let number = 123456789
number.toLocaleString() // 123,456,789

number = 12345.6784
number.toLocaleString() // 12,345.678

number = 12345.6785
number.toLocaleString() // 12,345.679

// nu 扩展字段要求编号系统，e.g. 中文十进制
number.toLocaleString('zh-Hans-CN-u-nu-hanidec') //  一二三,四五六.六七九
```

- & 参考资料：[MDN - Number.prototype.toLocaleString()](https://mdn.io/Number.prototype.toLocaleString())

### Math 常用的属性方法

```ad-warning 
title: 注意
`Math`不是一个构造器。`Math`的所有属性与方法都是静态的。
```

##### Math.PI

```ad-note
`Math.PI`表示一个圆的周长与直径的比例，约为 3.14159。
```

##### Math.abs()

```ad-note
`Math.abs()`函数返回给定数字的绝对值。
```

```js
Math.abs('-1') // 1
Math.abs(-2) // 2
Math.abs(null) // 0
Math.abs('string') // NaN
Math.abs() // NaN
```

##### Math.ceil()

```ad-note
`Math.ceil()`函数返回大于或等于一个给定数字的最小整数。既`向上取整`。
```

```js
Math.ceil(0.95) // 1
Math.ceil(1.05) // 2
Math.ceil(-1.05) // -1
Math.ceil(1) // 1
```

##### Math.floor()

```ad-note
`Math.floor()`返回小于或等于一个给定数字的最大整数。既`向下取整`。
```

```js
Math.floor(45.95) // 45
Math.floor(45.05) // 45
Math.floor(45) // 45
Math.floor(-45.05) // -46
Math.floor(-45.95) // -46
```

##### Math.max()

```ad-note
`Math.max()`函数返回一组数中的最大值。如果给定的参数中至少有一个参数无法被转换成数字，则会返回`NaN`。如果没有参数，则结果为 `-Infinity`。
```

```js
Math.max() // -Infinity
Math.max(3, -1, 1, 2, 3, 4, 5) // 5
Math.max(3, -1, 1, 2, 3, 4, 5, '', false) // 5
Math.max(3, -1, 1, 2, 3, 4, 5, '', false, undefined) // NaN

const arr = [3, -1, 1, 2, 3, 4, 5]
Math.max.apply(null, arr) // 5
Math.max(...arr) // 5
```

```ad-note
`Math.min()`函数返回一组数中的最小值。如果给定的参数中至少有一个参数无法被转换成数字，则会返回`NaN`。如果没有参数，结果为 `Infinity`。
```

```js
Math.min() // Infinity
Math.min(3, -1, 1, 2, 3, 4, 5) // -1
Math.min(3, -1, 1, 2, 3, 4, 5, '', false) // -1
Math.min(3, -1, 1, 2, 3, 4, 5, '', false, undefined) // NaN

const arr = [3, -1, 1, 2, 3, 4, 5]
Math.min.apply(null, arr) // -1
Math.min(...arr) // -1
```

##### Math.pow()

```ad-note
`Math.pow(x, y)`函数返回基数 x 的指数 y 次幂，即 x<sup>y</sup>。<span style="color:red">等价于 `x**y`。</span>
```

```js
Math.pow(2, 10) // 1024
2 ** 10 // 1024
Math.pow(4, 0.5) // 2
Math.pow(4, -0.5) // 0.5
Math.pow(-7, 0.5) // NaN
```

##### Math.random()

```ad-note
`Math.random()`函数返回一个浮点数, 伪随机数在范围从 0 到小于 1，也就是说，从 0（包括 0）往上，但是不包括 1（排除 1），然后您可以缩放到所需的范围。
```

```js
Math.random()
Math.floor(Math.random() * 3)
```

##### Math.round()

```ad-note
`Math.round()`函数返回一个数字四舍五入后最接近的整数。
```

```js
Math.round(20.49) // 20
Math.round(20.5) // 21
Math.round(-20.5) // -20
Math.round(-20.51) // -21
Math.round(-20.49) // -20
```

##### Math.sqrt()

```ad-note
`Math.sqrt()`函数返回一个数的平方根。y^2 = x。如果参数 number 为负值，则返回 `NaN`。
```

```js
Math.sqrt(9) // 3
Math.sqrt(2) // 1.414213562373095
Math.sqrt(1) // 1
Math.sqrt(0) // 0
Math.sqrt(-1) // NaN
Math.sqrt(-0) // -0
```

##### Math.trunc()

```ad-note
- `Math.trunc()`函数会将数字的小数部分去掉，只保留整数部分。<font color="#c00000">等价于 ~~（无 +0、-0 区分）。</font>
- `Math.trunc()`的执行逻辑很简单，仅仅是删除掉数字的小数部分和小数点，不管参数是正数还是负数。传入该方法的参数会被隐式转换成数字类型。
```

```js
Math.trunc(13.37) // 13
Math.trunc(42.84) // 42
Math.trunc(0.123) //  0
Math.trunc(-0.123) // -0
Math.trunc('-1.123') // -1
Math.trunc(Number.NaN) // NaN
Math.trunc('foo') // NaN
Math.trunc() // NaN

~~-0.95 // 0
~~0.95 // 0
~~-1.05 // -1
~~-1.95 // -1
~~45.95 // 45
~~45.05 // 45
```

- & [MDN - Math](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)

### Object 常用的属性方法

##### Object.assign()

```ad-note
用于将所有可枚举属性的值从一个或多个源对象分配到目标对象。它将返回目标对象。
```

```js
const o1 = { a: 1 }
const o2 = { b: 2 }
const o3 = { c: 3 }

const obj = Object.assign(o1, o2, o3)
console.log(obj) // { a: 1, b: 2, c: 3 }
console.log(o1) // { a: 1, b: 2, c: 3 }
```

##### Object.defineProperty()

```ad-note
直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
```

```js
const obj = {} // 创建一个新对象

// 在对象中添加一个属性与数据描述符的示例
Object.defineProperty(obj, 'a', {
  value: 37,
  writable: true,
  enumerable: true,
  configurable: true
})
```

##### Object.defineProperties()

```ad-note
- 直接在一个对象上定义新的属性或修改现有属性，并返回该对象。
- 该方法与Object.defineProperty相似，只不过该方法可以一次性操作多个属性。
```

```js
const obj = {}
Object.defineProperties(obj, {
  property1: {
    value: true,
    writable: true
  },
  property2: {
    value: 'Hello',
    writable: false
  }
})
// {property1: true, property2: 'Hello'}
```

##### Object.create()

```ad-note
创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。
```

```js
let o
// 创建一个原型为null的空对象
o = Object.create(null)

o = {}
// 以字面量方式创建的空对象就相当于:
o = Object.create(Object.prototype)

o = Object.create(Object.prototype, {
  // foo会成为所创建对象的数据属性
  foo: {
    writable: true,
    configurable: true,
    value: 'hello'
  },
  // bar会成为所创建对象的访问器属性
  bar: {
    configurable: false,
    get() { return 10 },
    set(value) {
      console.log('Setting `o.bar` to', value)
    }
  }
})
// {foo: 'hello'}
```

##### Object.keys()

```ad-note
返回一个由一个给定对象的自身可枚举属性组成的数组，数组中属性名的排列顺序和正常循环遍历该对象时返回的顺序一致。
```

```js
const obj = { name: 'javascript', age: 20 }
Object.prototype.history = 'lang'

Object.keys(obj) // ['name', 'age']
Object.keys(['a', 'b', 'c']) // ['0', '1', '2']
Object.keys({ 100: 'a', 2: 'b', 7: 'c' }) // ['2', '7', '100']
Object.keys('foo') // ['0', '1', '2']
```

##### Object.values()

```ad-note
返回一个给定对象自身的所有可枚举属性值的数组，值的顺序与使用for...in循环的顺序相同（区别在于 for...in 循环枚举原型链中的属性）。
```

```js
const obj = { name: 'javascript', age: 20 }
Object.prototype.history = 'lang'

Object.values(obj) // ['javascript', 20]
Object.values({ 100: 'a', 2: 'b', 7: 'c' }) // ['b', 'c', 'a']
```

##### Object.entries()

```ad-note
返回一个给定对象自身可枚举属性的键值对数组，其排列与使用 for...in 循环遍历该对象时返回的顺序一致（区别在于 for-in 循环还会枚举原型链中的属性）。
```

```js
const obj = { name: 'javascript', age: 20 }
Object.prototype.history = 'lang'

Object.entries(obj) // [['name', 'javascript'],['age', 20]]
// 对象转Map
new Map(Object.entries(obj)) // Map(2) {'name' => 'javascript', 'age' => 20}
```

##### Object.is()

```ad-note
判断两个值是否为同一个值。
```

```js
Object.is('foo', 'foo') // true
Object.is(window, window) // true

Object.is('foo', 'bar') // false
Object.is([], []) // false

const foo = { a: 1 }
const bar = { a: 1 }
Object.is(foo, foo) // true
Object.is(foo, bar) // false

Object.is(null, null) // true

// 特例
Object.is(0, -0) // false
Object.is(0, +0) // true
Object.is(-0, -0) // true
Object.is(Number.NaN, 0 / 0) // true
```

##### Object.getOwnPropertyNames()

```ad-note
返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括Symbol值作为名称的属性）组成的数组。
```

```js
Object.getOwnPropertyNames(['a', 'b', 'c']).sort() // ["0", "1", "2", "length"]

// 类数组对象
const obj = { 0: 'a', 1: 'b', 2: 'c' }
Object.getOwnPropertyNames(obj).sort() // ["0", "1", "2"]

// 使用Array.forEach输出属性名和属性值
Object.getOwnPropertyNames(obj).forEach((val, idx, array) => {
  console.log(val + ' -> ' + obj[val])
})
// 输出
// 0 -> a
// 1 -> b
// 2 -> c

// 不可枚举属性
const my_obj = Object.create({}, {
  getFoo: {
    value() { return this.foo },
    enumerable: false
  }
})
my_obj.foo = 1

console.log(Object.getOwnPropertyNames(my_obj).sort()) // ["foo", "getFoo"]
```

##### Object.getOwnPropertySymbols()

```ad-note
返回一个给定对象自身的所有 Symbol 属性的数组。
```

```js
let obj = {}
const a = Symbol('a')
const b = Symbol.for('b')

obj[a] = 'localSymbol'
obj[b] = 'globalSymbol'

const objectSymbols = Object.getOwnPropertySymbols(obj)

console.log(objectSymbols.length) // 2
console.log(objectSymbols) // [Symbol(a), Symbol(b)]
console.log(objectSymbols[0]) // Symbol(a)

// 拓展
// 静态方法 Reflect.ownKeys() 返回一个由目标对象自身的属性键组成的数组。
obj = { name: 'javascript', age: 20 }
Object.defineProperties(obj, {
  history: {
    value: 'lang'
  },
  foo: {
    value: Symbol('foo')
  },
})
obj // {name: 'javascript', age: 20, history: 'lang', foo: Symbol(foo)}
Reflect.ownKeys(obj) // ['name', 'age', 'history', 'foo']
// 等价于
Object.getOwnPropertyNames(obj).concat(Object.getOwnPropertySymbols(obj))
// ['name', 'age', 'history', 'foo']
```

- & [数据类型 Object - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object)
- & [内置对象 Reflect - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect)
- & [比较 Reflect 和 Object 方法 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/Comparing_Reflect_and_Object_methods)

### for…in 和 for…of

##### [for...in](https://mdn.io/zh/for...in)

```ad-note
以任意顺序遍历一个对象的除Symbol以外的可枚举属性，包括继承的可枚举属性。
```

```js
const obj = { name: 'javascript', age: 20 }
Object.prototype.history = 'lang'

for (const i in obj) {
  console.log(i, obj.hasOwnProperty(i))
}
// name true
// age true
// history false
```

##### [for...of](https://mdn.io/zh/for...of)

```ad-note
- 可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments 对象等等）上创建一个迭代循环；
- 语句可以使用 hasOwnProperty() 加一层过滤以达到 Object.keys() 的效果。
```

### 数值数组去重

```ad-warning 
title: 注意
`Set()` 的成员值都是唯一的，可以过滤重复的 `Number`、`String`、`Boolean`、`undefined`、`null`、`NaN`， 无法过滤重复的 `Object`。
```

```js
const arr = [1, 2, 5, 3, 3, 1, 4, 9, 7, 1, 5]

console.log([
  ...new Set([
    1,
    1,
    '3',
    '3',
    Number.NaN,
    Number.NaN,
    undefined,
    undefined,
    null,
    null,
    true,
    true,
    {},
    {},
  ]),
])
// [1, "3", NaN, undefined, null, true, {}, {}]
```

##### 通过 `Set()` 和 扩展运算符

```js
[...new Set(arr)]
// [1, 2, 5, 3, 4, 9, 7]
```

##### 通过 `Array.from()`

```js
Array.from(new Set(arr));
// [1, 2, 5, 3, 4, 9, 7]

// 拓展：
[...new Set([1, 1, '3', '3', Number.NaN, Number.NaN, undefined, undefined, null, null, true, true, {}, {}])]
// [1, "3", NaN, undefined, null, true, {}, {}]
```

##### 通过 `Array.prototype.filter()` 和 `Array.prototype.indexOf()`

```js
function unique(_arr) {
  return _arr.filter((item, index, array) => (array.indexOf(item) === index))
}
unique(arr) // [1, 2, 5, 3, 4, 9, 7]
```

##### 通过 `Array.prototype.reduce()` 和 `Array.prototype.includes()`

```js
function unique(_arr) {
  return _arr.reduce((result, item) => {
    return result.includes(item) ? result : [...result, item]
  }, [])
}
unique(arr) // [1, 2, 5, 3, 4, 9, 7]
```

### 对象数组去重

```js
const objArr = [
  { id: 1, name: '小米' },
  { id: 2, name: '小米2' },
  { id: 5, name: '小东' },
  { id: 2, name: '小米2' },
  { id: 1, name: '小米' },
  { id: 8, name: '小红' },
  { id: 10, name: '小西' },
  { id: 12, name: '小明' },
  { id: 8, name: '小红' }
]
```

##### 通过 `Array.prototype.reduce()`

```js
Array.prototype.uniqueArr = function (key) {
  if (!Array.isArray(this))
    return
  const temp = {}
  return this.reduce((result, next) => {
    temp[next[key]] ? '' : (temp[next[key]] = true) && result.push(next)
    return result
  }, [])
}
objArr.uniqueArr('id')
```

##### 通过 `Array.prototype.filter()` 和 `Set()`/`Map()`

```js
Array.prototype.uniqueArr = function (key) {
  if (!Array.isArray(this))
    return
  const set = new Set()
  return this.filter((item) => {
    return !set.has(item[key]) && set.add(item[key])
  })
  // let map = new Map();
  // return this.filter(item=>{
  //   return !map.has(item[key]) && map.set(item[key], 1);
  // })
}
objArr.uniqueArr('id')
```

### 数组扁平化

```tip 提示
`Array.prototype.join()` 和 `Array.prototype.toString()` 都可以将多维数组转成普通字符串。
```

```js
const arr = [1, [2, 3], [4, 5]]
arr.join() // '1,2,3,4,5'
arr.toString() // '1,2,3,4,5'
```

##### 通过 `Array.prototype.concat()` 和 扩展运算符

```js
const arr = [1, [2, 3], [4, 5]];
[].concat(...arr)
// [1, 2, 3, 4, 5]
```

##### 通过 `Array.prototype.join()`/`Array.prototype.toString()` 和 `String.prototype.split() `

```js
const arr = [1, [2, 3], [4, 5], [6, [7, 8, [9, 10]]]]
arr.join().split(',').map(Number)
arr.toString().split(',').map(Number)
// [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 通过 ` Array.prototype.flat()`

```js
const arr = [1, [2, 3], [4, 5], [6, [7, 8, [9, 10]]]]
arr.flat() // [1, 2, 3, 4, 5, 6, [7, 8, [9, 10]]]
arr.flat(2) // [1, 2, 3, 4, 5, 6, 7, 8, [9, 10]]
arr.flat(Infinity) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 通过 `Array.prototype.reduce()`

```js
const arr = [1, [2, 3], [4, 5], [6, [7, 8, [9, 10]]]]
function flatten(_arr) {
  return _arr.reduce((result, item) => {
    return result.concat(Array.isArray(item) ? flatten(item) : item)
  }, [])
}
flatten(arr) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

- & [数组扁平化](https://zhuanlan.zhihu.com/p/344241682)、[Array.prototype.flat()](https://mdn.io/zh/Array.prototype.flat())
