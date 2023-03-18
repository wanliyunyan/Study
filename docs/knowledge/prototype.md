# prototype
## __proto__、constructor 、prototype

**`Object.prototype.__proto__`  该特性已经从 Web 标准中删除，虽然一些浏览器目前仍然支持它，但也许会在未来的某个时间停止支持，请尽量不要使用该特性。**

`__proto__`和constructor属性是对象所独有的  
prototype属性是函数所独有的,但是由于JS中函数也是一种对象,所以函数也拥有`__proto__`和constructor属性。  

先来看下面这段代码：
```
function foo(){}
let f = new foo();
```

foo()是函数,它的constructor属性指向Function(),它的prototype属性指向foo.prototype,它的`__proto__`属性指向Function.prototype。   

f是foo实例化的对象,它的constructor属性指向foo(),`__proto__`属性指向foo.prototype。  

## prototype   
prototype属性的作用就是让该函数所实例化的对象们都可以找到公用的属性和方法。  
函数的prototype属性指向了一个对象，这个对象正是调用该构造函数而创建的实例的原型
原型对象prototype有一个默认的constructor属性，用于记录实例是由哪个构造函数创建；

## `__proto__`
这是每一个JavaScript对象(除了 null,undefined )都具有的一个属性，叫`__proto__`，这个属性会指向该对象的原型。  
`__proto__`属性的作用就是当访问一个对象的属性时,如果该对象内部不存在这个属性,
那么就会去它的`__proto__`属性所指向的那个对象（父对象）里找,一直找,直到`__proto__`属性的终点null,然后返回undefined,通过`__proto__`属性将对象连接起来的这条链路即我们所谓的原型链。
属性`__proto__`是一个对象，它有两个属性，constructor和`__proto__`；

```
{}.__proto__  // Uncaught SyntaxError: Unexpected token '.'
1.__proto__  // Uncaught SyntaxError: Invalid or unexpected token
```

使用`__proto__`是有争议的，也不鼓励使用它。因为它从来没有被包括在 EcmaScript 语言规范中，但是现代浏览器都实现了它。`__proto__` 属性已在 ECMAScript 6 语言规范中标准化，用于确保 Web 浏览器的兼容性，因此它未来将被支持。它已被不推荐使用，现在更推荐使用Object.getPrototypeOf/Reflect.getPrototypeOf 和Object.setPrototypeOf/Reflect.setPrototypeOf（尽管如此，设置对象的 [[Prototype]] 是一个缓慢的操作，如果性能是一个问题，应该避免）

## Object.getPrototypeOf()
```js
const prototype1 = {};
const object1 = Object.create(prototype1);

console.log(Object.getPrototypeOf(object1) === prototype1);
```

## constructor
constructor属性的含义就是指向该对象的构造函数,所有函数（此时看成对象了）最终的构造函数都指向Function。
```
函数创建的对象.__proto__ === 该函数.prototype 最终指向 object.prototype
函数.__proto__ === Function.prototype  
函数.prototype.constructor=== 函数本身  
Object.__proto__=== Function.prototype  

Function.__proto__=== Function.prototype  
Function.prototype.__proto__=== Object.prototype  
Function.constructor === Function  
```

原型的prototype其实是function对象的一个属性
这个prototype是定义构造函数构造出每个对象的公共祖先
所有该构造函数构造出的对象都可以继承原型上的属性和方法

```
function Phone(color,brand){
    this.color = color;
    this.brand = brand;
    // this.screen = "18:9" 一般不写这 为了显示下面的18:9
}

Phone.prototype.screen = 16:9;

let p1 = new("red","小米")；
console.log(p1.screen)  // 18:9  自己有的属性不会去原型上找
```

开发插件的时候,当需要传的值写到构造函数上面,方法和其它的属性都直接挂在prototype上

不能通过修改实例化对象,更改prototype

构造函数是可以更改的
function Telephone(color,brand){ }

Phone.prototype{
    constructor:Telephone  // 这里就可以改变构造函数
}

```
function Car(){
    let this = {
        __proto__:Car.prototype // 
    }
}
Car.prototype.name = "Benz";
let car = new Car();
console.log(car)

__proto__就是对象的一个属性,是可以被修改的
car.__proto__  = {
    name:"mazda"
}
```

```
Car.prototype.name = "Mazda";
console.log(Car.prototype) 
let car1= new Car();

Car.prototype= {name : "Benz"}
console.log(Car.prototype)
let car2= new Car();

console.log(car1.name) // Mazda
console.log(car2.name) // Benz
```

```
function Car(){
    this.brand = "Benz"
}
Car.prototype = {
    brand:"Mazda",
    intro:function(){
        console.log(this.brand)
    }
}

let var = new Car();
car.intro(); //Benz
Car.prototype.intro();  Mazda

```
