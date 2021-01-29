# Object

## Object.create(null) 和{}的区别

- js创建对象的方式
```
var obj = Object.create(null);
var obj1 = {}
var obj2 = new Object()
```

- 创建的方法有如上的三种方法，那么他们之间有什么区别呢？
1. 通过 Object.create(null) 创建的对象是不继承Object原型链上的属性方法
2. 通过{}创建的对象和new Object()的方式是一样的，都会继承Object对象的所有属性


valueOf() 与 toString()

## 创建对象

1. 对象字面量
```
let obj = {
    name:"ha",
    sex:"male"
}
obj.name = "sdsad"

```

2. 构造函数

```
let obj = new Object(); // 实例化构造函数
obj.name = "sdsad"
obj.sex = "sdsad"
```

自定义构造函数
// 首字母大写
function Teacher(name,sex){
    this.name = name;    
    this.sex = sex;    
    this.smoke = function(){
        console.log(123)
    };    
    this.eat = = function(){
        console.log(123)
    };
}
let teacher1 = new Teacher();
let teacher2 = new Teacher();
用new实例化后，this才存在，this才能指向对象，单纯执行Teacher，this指向window
new的时候，在AO中保存this，this 被构造函数return给对象

```
function Car(color,brand){
    let me = {};
    me.color = color;
    return me
}
```


```
function Car(color,brand){
    this.color  = "red"
    
    // 引用值会影响new {} [] function ，原始值不影响
    return 引用值
}

let car = new Car();

```