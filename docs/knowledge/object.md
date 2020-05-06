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
