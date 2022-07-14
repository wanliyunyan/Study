# ES

## ES2016

### Array.prototype.includes()

```js
arr.includes(valueToFind[, fromIndex])
// fromIndex 可选 从fromIndex 索引处开始查找 valueToFind。如果为负值（即从末尾开始往前跳 fromIndex 的绝对值个索引，然后往后搜寻）。默认为 0。
const arr = ['es6', 'es7', 'es8']
console.log(arr.includes('es7')) // true
console.log(arr.includes('es7', 1)) // true
console.log(arr.includes('es7', 2)) // false
console.log(arr.includes("es7", -1)); // fsle
console.log(arr.includes("es7", -2)); // true
```
#### 注意点
- 查找字符串是区分大小写的。
- 只能判断简单类型的数据。
- 能识别NaN，indexOf是不能识别NaN的

### 幂运算符 **

```js
console.log(Math.pow(2, 10)); // 1024
console.log(2 ** 10); // 1024
```

## ES2017

### Object.entries()
Object.entries() 方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历属性的键值对数组。
```js
const obj = {
  name: "jimmy",
  age: 18,
  height: 188,
};
console.log(Object.entries(obj)); // [ [ 'name', 'jimmy' ], [ 'age', 18 ], [ 'height', 188 ] ]
console.log(Object.entries([1, 2, 3])); // [ [ '0', 1 ], [ '1', 2 ], [ '2', 3 ] ]
```

### Object.getOwnPropertyDescriptors()
Object.getOwnPropertyDescriptors()  方法用来获取一个对象的所有自身属性的描述符。
```js
const obj = {
  name: "jimmy",
  age: 18,
};
const desc = Object.getOwnPropertyDescriptors(obj);
console.log(desc);  
// 打印结果
{
  name: {
    value: 'jimmy',
    writable: true,
    enumerable: true,
    configurable: true
  },
  age: { 
   value: 18, 
   writable: true,
   enumerable: true, 
   configurable: true 
  }
}
```

- value表示当前对象的默认值
- writable表示对象属性是否可以修改
- enumerable表示当前这个属性是否可以出现在对象的枚举属性中
- configurable表示如果该值为 false，则该属性不能被删除（对于访问器属性则不能被修改），并且除了 [[Value]] 和 [[Writable]] 以外的特性都不能被修改。

那这些对象的属性我们怎么设置和修改他们呢，我们可以使用es5的 Object.defineProperty()
```js
const obj = {};
Object.defineProperty(obj, "name", {
  value: "jimmy",
  writable: true,
  configurable: true,
  enumerable: true,
});
Object.defineProperty(obj, "age", {
  value: 34,
  writable: true,
  configurable: true,
  enumerable: true,
});
console.log(obj); // { name: 'jimmy', age: 34 }

const obj = {};
Object.defineProperty(obj, "name", {
    value: "jimmy",
    writable: false,
    configurable: false,
    enumerable: true,
});
console.log(obj); // { name: 'jimmy' }
obj.name = "chimmy";
console.log(obj); // { name: 'jimmy' }
delete obj.name
console.log(obj); // { name: 'jimmy' }

```
当设置enumerable: false时，表示对象的属性不可被枚举，这时打印对象为空，遍历对象的键也为空。


### String.prototype.padStart
把指定字符串填充到字符串头部，返回新字符串。
```js
str.padStart(targetLength [, padString])
// targetLength
// 当前字符串需要填充到的目标长度。如果这个数值小于当前字符串的长度，则返回当前字符串本身。

// padString 可选
// 填充字符串。如果字符串太长，使填充后的字符串长度超过了目标长度，则只保留最左侧的部分，其他部分会被截断。此参数的默认值为 " "

'abc'.padStart(10);         // "       abc"
'abc'.padStart(10, "foo");  // "foofoofabc"
'abc'.padStart(6,"123465"); // "123abc"
'abc'.padStart(8, "0");     // "00000abc"
'abc'.padStart(1);          // "abc"

```
#### 应用场景
数字替换(手机号，银行卡号等）
```js
const tel = '18781268679'
const newTel = tel.slice(-4).padStart(tel.length, '*')
console.log(newTel) // *******5678
```

### String.prototype.padEnd
把指定字符串填充到字符串尾部，返回新字符串。

```js
'abc'.padEnd(10);          // "abc       "
'abc'.padEnd(10, "foo");   // "abcfoofoof"
'abc'.padEnd(6, "123456"); // "abc123"
'abc'.padEnd(1);           // "abc"
```

### async/await
在不阻塞主线程的情况下使用同步代码实现异步访问资源的能力，并且使得代码逻辑更加清晰。
#### 注意点
- await 只能在 async 标记的函数内部使用，单独使用会触发 Syntax error。
- await后面需要跟异步操作，不然就没有意义。

## ES2018

### Object Rest & Spread
如果存在相同的属性名，只有最后一个会生效

#### 注意
如果属性的值是一个对象的话，该对象的引用会被拷贝，而不是生成一个新的对象。
```js
const input = {
  a: 1,
  b: 2,
  c: 3
}

let { a, ...rest } = input
// 当对象 key-value 不确定的时候，把必选的 key 赋值给变量，用一个变量收敛其他可选的 key 数据，这在之前是做不到的。注意，rest 属性必须始终出现在对象的末尾，否则将抛出错误。
```

### for await of
异步迭代器(for-await-of)：循环等待每个Promise对象变为resolved状态才进入下一步。


## ES2019

### Object.fromEntries()

```js
Object.fromEntries([
    ['foo', 1],
    ['bar', 2]
])
// {foo: 1, bar: 2}

// Map -> Object
const map = new Map()
map.set('name', 'jimmy')
map.set('age', 18)
console.log(map) // {'name' => 'jimmy', 'age' => 18}

const obj = Object.fromEntries(map)
console.log(obj)
// {name: "jimmy", age: 18}


const course = {
    math: 80,
    english: 85,
    chinese: 90
}
const res = Object.entries(course).filter(([key, val]) => val > 80)
console.log(res) // [ [ 'english', 85 ], [ 'chinese', 90 ] ]
console.log(Object.fromEntries(res)) // { english: 85, chinese: 90 }

// 取search
// let url = "https://www.baidu.com?name=jimmy&age=18&height=1.88"
// queryString 为 window.location.search
const queryString = "?name=jimmy&age=18&height=1.88";
const queryParams = new URLSearchParams(queryString);
const paramObj = Object.fromEntries(queryParams);
console.log(paramObj); // { name: 'jimmy', age: '18', height: '1.88' }

```

### Array.prototype.flat()

```js
let newArray = arr.flat([depth])
// depth 可选 指定要提取嵌套数组的结构深度，默认值为 1。

// flat()  方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

const arr1 = [0, 1, 2, [3, 4]];
console.log(arr1.flat());  //  [0, 1, 2, 3, 4]
const arr2 = [0, 1, 2, [[[3, 4]]]];
console.log(arr2.flat(2));  //  [0, 1, 2, [3, 4]]

//使用 Infinity，可展开任意深度的嵌套数组
var arr4 = [1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]];
arr4.flat(Infinity); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// `flat()`方法会移除数组中的空项:
var arr5 = [1, 2, , 4, 5];
arr5.flat(); // [1, 2, 4, 5]

```

### Array.prototype.flatMap()
flatMap() 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。从方法的名字上也可以看出来它包含两部分功能一个是 map，一个是 flat（深度为1）。

```js
var new_array = arr.flatMap(function callback(currentValue[, index[, array]]) {
    // 返回新数组的元素
}[, thisArg])
// callback
// 可以生成一个新数组中的元素的函数，可以传入三个参数：
// currentValue 当前正在数组中处理的元素
// index 可选 数组中正在处理的当前元素的索引。
// array 可选   被调用的map数组
// thisArg可选 执行callback函数时使用的this值。

const numbers = [1, 2, 3]
numbers.map(x => [x * 2]) // [[2], [4], [6]]
numbers.flatMap(x => [x * 2]) // [2, 4, 6]
```

### trimStart()
trimStart() 方法从字符串的开头删除空格，trimLeft()是此方法的别名。
```js
let str = '   foo  '
console.log(str.length) // 8
str = str.trimStart() // 或str.trimLeft()
console.log(str.length) // 5
```

### String.prototype.trimEnd()
trimEnd() 方法从一个字符串的右端移除空白字符，trimRight 是 trimEnd 的别名。
```js
let str = '   foo  '
console.log(str.length) // 8
str = str.trimEnd() // 或str.trimRight()
console.log(str.length) // 6
```

### 可选的Catch
```js
try {
    console.log('Foobar')
} catch {
    console.error('Bar')
}
```

### JSON.stringify() 增强能力

JSON.stringify 在 ES10 修复了对于一些超出范围的 Unicode 展示错误的问题。因为 JSON 都是被编码成 UTF-8，所以遇到 0xD800–0xDFFF 之内的字符会因为无法编码成 UTF-8 进而导致显示错误。在 ES10 它会用转义字符的方式来处理这部分字符而非编码的方式，这样就会正常显示了。

```js
// \uD83D\uDE0E  emoji 多字节的一个字符
console.log(JSON.stringify('\uD83D\uDE0E')) // 打印出笑脸

// 如果我们只去其中的一部分  \uD83D 这其实是个无效的字符串
// 之前的版本 ，这些字符将替换为特殊字符，而现在将未配对的代理代码点表示为JSON转义序列
console.log(JSON.stringify('\uD83D')) // "\ud83d"
```

### 修订 Function.prototype.toString()
以前函数的toString方法来自Object.prototype.toString(),现在的 Function.prototype.toString() 方法返回一个表示当前函数源代码的字符串。以前只会返回这个函数，不包含注释、空格等。

```js
function foo() {
    // es10新特性
    console.log('imooc')
}
console.log(foo.toString()) 
// 打印如下
// function foo() {
//  // es10新特性
//  console.log("imooc");
// }
```

## ES2020

### 空值合并运算符（Nullish coalescing Operator）
（ ?? ）是一个逻辑操作符，当左侧的操作数为 null或者undefined时，返回其右侧操作数，否则返回左侧操作数。
```js
const foo = undefined ?? "foo"
const bar = null ?? "bar"
console.log(foo) // foo
console.log(bar) // bar
```

与逻辑或操作符（||）不同，逻辑或操作符会在左侧操作数为假值时返回右侧操作数。也就是说，如果使用 || 来为某些变量设置默认值，可能会遇到意料之外的行为。比如为假值（例如'',0,NaN,false）时。见下面的例子。
```js
const foo = "" ?? 'default string';
const foo2 = "" || 'default string';
console.log(foo); // ""
console.log(foo2); // "default string"

const baz = 0 ?? 42;
const baz2 = 0 || 42;
console.log(baz); // 0
console.log(baz2); // 42
```

#### 注意点
将 ?? 直接与 AND（&&）和 OR（||）操作符组合使用是不可取的。
```js
null || undefined ?? "foo"; // 抛出 SyntaxError
true || undefined ?? "foo"; // 抛出 SyntaxError
```

### 可选链 Optional chaining
操作符(?.)允许读取位于连接对象链深处的属性的值，而不必明确验证链中的每个引用是否有效。?.操作符的功能类似于.链式操作符，不同之处在于，在引用为null或者undefined 的情况下不会引起错误，该表达式短路返回值是undefined。
```js
const street2 = user?.address?.street
const num2 = user?.address?.getNum?.()
console.log(street2, num2)
```
#### 注意点
可选链不能用于赋值
```js
let object = {};
object?.property = 1; // Uncaught SyntaxError: Invalid left-hand side in assignment
```

### globalThis
现在globalThis提供了一个标准的方式来获取不同环境下的全局this 对象（也就是全局对象自身）。不像window或者self这些属性，它确保可以在有无窗口的各种环境下正常工作。所以，你可以安心的使用globalThis，不必担心它的运行环境。


### BigInt
BigInt 是一种内置对象，它提供了一种方法来表示大于 2的53次方 - 1 的整数。这原本是 Javascript中可以用 Number 表示的最大数字。BigInt 可以表示任意大的整数。
```js
const bigInt = 9007199254740993n
console.log(bigInt)
console.log(typeof bigInt) // bigint

// `BigInt`和[`Number`]不是严格相等的，但是宽松相等的。
console.log(1n == 1) // true
console.log(1n === 1) // false

// `Number`和`BigInt`可以进行比较。
1n < 2 //  true
2n > 1 //  true

const bigIntNum = BigInt(9007199254740993n)
console.log(bigIntNum)

let number = BigInt(2);
let a = number + 2n; // 4n
let b = number * 10n; // 20n
let c = number - 10n; // -8n
console.log(a);
console.log(b);
console.log(c);

```

#### 注意点
BigInt不能用于 [Math] 对象中的方法；不能和任何 [Number] 实例混合运算，两者必须转换成同一种类型。在两种类型来回转换时要小心，因为 BigInt 变量在转换成 [Number] 变量时可能会丢失精度

### String.prototype.matchAll()
方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。
```js
const regexp = /t(e)(st(\d?))/g;
const str = 'test1test2';

const array = [...str.matchAll(regexp)];
console.log(array[0]);  // ["test1", "e", "st1", "1"]
console.log(array[1]); // ["test2", "e", "st2", "2"]


```

### Promise.allSettled()
我们都知道 Promise.all() 具有并发执行异步任务的能力。但它的最大问题就是如果其中某个任务出现异常(reject)，所有任务都会挂掉，Promise直接进入reject 状态。
场景：现在页面上有三个请求，分别请求不同的数据，如果一个接口服务异常，整个都是失败的，都无法渲染出数据
我们需要一种机制，如果并发任务中，无论一个任务正常或者异常，都会返回对应的的状态，这就是Promise.allSettled的作用
```js
const promise1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise1");
      //   reject("error promise1 ");
    }, 3000);
  });
};
const promise2 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise2");
      //   reject("error promise2 ");
    }, 1000);
  });
};
const promise3 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      //   resolve("promise3");
      reject("error promise3 ");
    }, 2000);
  });
};

//  Promise.all 会走到catch里面
Promise.all([promise1(), promise2(), promise3()])
  .then((res) => {
    console.log(res); 
  })
  .catch((error) => {
    console.log("error", error); // error promise3 
  });
  
// Promise.allSettled 不管有没有错误，三个的状态都会返回
Promise.allSettled([promise1(), promise2(), promise3()])
  .then((res) => {
    console.log(res);  
    // 打印结果 
    // [
    //    {status: 'fulfilled', value: 'promise1'}, 
    //    {status: 'fulfilled',value: 'promise2'},
    //    {status: 'rejected', reason: 'error promise3 '}
    // ]
  })
  .catch((error) => {
    console.log("error", error); 
  });

```

### Dynamic Import
import()可以在需要的时候，再加载某个模块。
```js
button.addEventListener('click', event => {
  import('./dialogBox.js')
  .then(dialogBox => {
    dialogBox.open();
  })
  .catch(error => {
    /* Error handling */
  })
});
```

## ES2021

### &&=
```js
x &&= y // 当x为真时，x=y
```

### ||=
```js
x ||= y // 当x为假时，x=y
```

### ??=
```js
x ??= y // 当x是nullish(null 或 undefined)时，x=y
```

### String.prototype.replaceAll()
replaceAll()  方法返回一个新字符串，新字符串中所有满足 pattern 的部分都会被replacement 替换。pattern可以是一个字符串或一个RegExp，replacement可以是一个字符串或一个在每次匹配被调用的函数。
```js
'aabbcc'.replaceAll('b', '.'); // 'aa..cc'
```
### 数字分隔符
```js
let budget = 1_000_000_000_000;
budget === 10 ** 12 // true

// 这个数值分隔符没有指定间隔的位数，也就是说，可以每三位添加一个分隔符，也可以每一位、每两位、每四位添加一个。
123_00 === 12_300 // true
12345_00 === 123_4500 // true
12345_00 === 1_234_500 // true

// 小数
0.000_001

// 科学计数法
1e10_000
```

#### 注意
- 不能放在数值的最前面（leading）或最后面（trailing）。
- 不能两个或两个以上的分隔符连在一起。
- 小数点的前后不能有分隔符。
- 科学计数法里面，表示指数的e或E前后不能有分隔符。

### Promise.any
```js
// 只要参数实例有一个变成fulfilled状态，包装实例就会变成fulfilled状态；如果所有参数实例都变成rejected状态，包装实例就会变成rejected状态。
const promise1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise1");
      //  reject("error promise1 ");
    }, 3000);
  });
};
const promise2 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise2");
      // reject("error promise2 ");
    }, 1000);
  });
};
const promise3 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("promise3");
      // reject("error promise3 ");
    }, 2000);
  });
};
Promise.any([promise1(), promise2(), promise3()])
  .then((first) => {
    // 只要有一个请求成功 就会返回第一个请求成功的
    console.log(first); // 会返回promise2
  })
  .catch((error) => {
    // 所有三个全部请求失败 才会来到这里
    console.log("error", error);
  });

```


## ES2022

### .at() 
索引值对应值的方法

```js
const array = [1,2,3,4,5,6]

// ✅ When used with positive index it is equal to [index]
array.at(0) // 1
array[0] // 1

// ✅ When used with negative index it mimicks the Python behaviour
array.at(-1) // 6
array.at(-2) // 5
array.at(-4) // 3
```






https://juejin.cn/post/7046217976176967711
https://juejin.cn/post/7119309621453389855


