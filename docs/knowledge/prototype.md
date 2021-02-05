# __proto__、constructor 、prototype

__proto__和constructor属性是对象所独有的  
prototype属性是函数所独有的 
但是由于JS中函数也是一种对象，所以函数也拥有__proto__和constructor属性。  

先来看下面这段代码：
```
function foo(){}
let f = new foo();
```

foo()是函数，它的constructor属性指向Function()，它的prototype属性指向foo.prototype，它的__proto__属性指向Function.prototype。   

f是foo实例化的对象，它的constructor属性指向foo()，__proto__属性指向foo.prototype。  

__proto__属性的作用就是当访问一个对象的属性时，如果该对象内部不存在这个属性，那么就会去它的__proto__属性所指向的那个对象（父对象）里找，一直找，直到__proto__属性的终点null，然后返回undefined，通过__proto__属性将对象连接起来的这条链路即我们所谓的原型链。
   
prototype属性的作用就是让该函数所实例化的对象们都可以找到公用的属性和方法。
    
constructor属性的含义就是指向该对象的构造函数，所有函数（此时看成对象了）最终的构造函数都指向Function。
   
```
函数创建的对象.__proto__ === 该函数.prototype 最终指向 object.prototype
函数.__proto__ === Function.prototype  
函数.prototype.constructor=== 函数本身  
Object.__proto__=== Function. prototype  

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

开发插件的时候，当需要传的值写到构造函数上面，方法和其它的属性都直接挂在prototype上

不能通过修改实例化对象，更改prototype

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

__proto__就是对象的一个属性，是可以被修改的
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

let obj = {}
let obj = new Object();
完全一样

### Object.create(对象、null) 创建对象

function Obj(){}
Obj.prototype.num = 1;
let obj = Object.create(Obj.prototype)
let obj = new Obj();
完全一样

new 1调用构造函数初始化属性和方法
    2 指定实例化对象的原型
let test = {num:2};
let obj = Object.create(test) 

// 创建没有原型的空对象
let obj1 = Object.create(null)
obj1.num = 1
// obj1作为obj2的原型
let obj2 = Object.create(obj1)

let obj3 = {count:2}
obj1.__proto__ = obj3
console.log(obj1.count) undefined
// 因为 __proto__ 不能人为指定，但是可以修改

undefined null 没有包装类，没有原型，所以没有对应的属性

let num = 1
let obj = {}
let obj2 = Object.create(null)
document.write(num)
document.write(obj)
document.write(obj2) // 报错 没有原型 没有toString

obj2.toString = function(){
    return ""
}
document.write(obj2.toString()) 

Number.prototype.toString.call(1) // "1"  
Object.prototype.toString.call(1) // "1"  

这两个toString方法不一样