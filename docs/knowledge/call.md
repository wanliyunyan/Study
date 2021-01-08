# call

## Array.prototype.slice.call()
Array.prototype.slice.call(arguments)能将具有length属性的对象转成数组，除了IE下的节点集合（因为ie下的dom对象是以com对象的形式实现的，js对象与com对象不能进行转换）

```
let a={length:2,0:'first',1:'second'};//类数组,有length属性，长度为2，第0个是first，第1个是second  
Array.prototype.slice.call(a,0)// ["first", "second"],调用数组的slice(0)
```

### arguments特性
尽管传入的是 **1,2,3** ,但是js的arguments会把它转换成伪数组
```
function list() {
    return Array.prototype.slice.call(arguments);
}
var list1 = list(1, 2, 3); // [1, 2, 3]
```

### prototype特性
Array方法具有prototype对象,[]继承于Array,直接可以使用slice
```
var args = Array.prototype.slice.call(arguments)  
var args = [].slice.call(arguments)
```