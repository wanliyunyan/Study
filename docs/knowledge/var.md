# var let const
通常网上介绍**var**与**let**的文章都是介绍它的一个最重要的区别,
即**var**存在变量提升,而**let**是块级作用域不存在变量提升。
但这说不够全面或者说的不够深入。

我们先看一段代码

```
a = 1
var a =2    
console.log(a) // 2
```


有些面试题会问你**a**等于多少,我们在全局作用域下声明**a = 1**,这相当于**window.a = 1**,可是**var a = 2**之后**a**为什么就变成2了呢？

这就是本文想说的重点,js编程环境的顶级作用域是window对象下的范围,称为全局作用域,全局作用域中的变量称为全局变量。在浏览器环境中**window**是顶层变量,es5中顶层变量的属性等价于全局变量,在全局作用域下**var a = 2**,此时**a**既是顶级变量也是全局变量,会覆盖**window**中的**a**。

再看一段代码

```
var a = 1
console.log(window.a) // 1
```

当我们声明**var a = 1**的时候,就已经把**a**声明到**window**对象中了。

但是**let**没有这种效果

```
a = 1
let a =2  
console.log(window.a) // 1
console.log(a) // 2
```

或者

```
let a = 1
console.log(window.a)  // undefined
```

**Function**定义的函数会覆盖**var**定义的变量,但是不会覆盖**let**定义的变量,会报错

```
let a = 1
function a(){}  // Uncaught SyntaxError: Identifier 'a' has already been declared
```

es5中顶层变量的属性等价于全局变量,es5的var function 声明的全局变量,依旧是顶级对象的属性。到了es6中有所改变, 而es6声明的全局变量不属于顶级对象的属性了

而这个区别或者说特性,网上的文章很少提到,请大家格外注意。

## 暂时性死区

```
var tmp = 123;

if (true) {
    // TDZ开始
    tmp = 'abc'; // ReferenceError
    console.log(tmp); // ReferenceError

    let tmp; // TDZ结束
    console.log(tmp); // undefined

    tmp = 123;
    console.log(tmp); // 123
}
```

上面代码中,存在全局变量tmp,但是块级作用域内let又声明了一个局部变量tmp,导致后者绑定这个块级作用域,所以在let声明变量前,对tmp赋值会报错。  
ES6明确规定,如果区块中存在let和const命令,这个区块对这些命令声明的变量,从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量,就会报错。  
总之,在代码块内,使用let命令声明变量之前,该变量都是不可用的。这在语法上,称为“暂时性死区”（temporal dead zone,简称TDZ）。


```
typeof x; // ReferenceError
let x;
```

上面代码中,变量x使用let命令声明,所以在声明之前,都属于x的“死区”,只要用到该变量就会报错。因此,typeof运行时就会抛出一个ReferenceError。  
作为比较,如果一个变量根本没有被声明,使用typeof反而不会报错。

```
function bar(x = y, y = 2) {
    return [x, y];
}

bar(); // 报错
```
上面代码中,调用bar函数之所以报错,是因为参数x默认值等于另一个参数y,而此时y还没有声明,属于”死区“。如果y的默认值是x,就不会报错,因为此时x已经声明了。
