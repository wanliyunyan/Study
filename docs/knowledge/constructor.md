# 构造函数

- 1.什么是构造函数  
在 JavaScript 中,用 new 关键字来调用的函数,称为构造函数。

- 2.构造函数的执行过程   
    - (1) 当以 new 关键字调用时,会创建一个新的内存空间,标记为**类**的实例。
    - (2) 函数体内部的 this 指向该内存。
    - (3) 执行函数体内的代码。
    - (4) 默认返回 this 。

- 3.构造函数的返回值
    - (1) 没有手动添加返回值,默认返回 this 。
    - (2) 手动添加一个基本数据类型的返回值,最终还是返回 this。
    - (3) 手动添加一个复杂数据类型(对象)的返回值,最终返回该对象。
    
- 4.手动实现new   
```
function realizeNew () {
    //创建一个新对象
    let obj  = {};
    //获得构造函数
    let constructor = [].shift.call(arguments);
    //链接到原型（给obj这个新生对象的原型指向它的构造函数的原型）
    obj.__proto__ = constructor.prototype;
    //绑定this
    let result = constructor.apply(obj,arguments);
    //确保new出来的是一个对象
    return typeof result === "object" ? result : obj
}
```


     

