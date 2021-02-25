# typeof

typeof运算符用于判断对象的类型,但是对于一些创建的对象,它们都会返回'object'

一个额外的小技巧是可以使用 typeof 来获取一个变量是否存在,如 
```
if(typeof a!="undefined"){
    alert("ok")
}
```
而不要去使用 
```
if(a){ // undefind
    alert("ok")
}
```
因为如果 a 不存在（未声明）则会出错

务必记住typeof是一个运算符,当然也可以像函数一样使用

```
if(typeof(a)!="undefined"){
    alert("ok")
}
```

     

