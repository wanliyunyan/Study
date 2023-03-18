# 对象 clone

Object.prototype.num = 1;
let person1 = {
    name:"张三",
    name:{
        first:"J"
    }
}

// let person2 = {};


for(let key in person1){
    person2[key] = person1[key]
}
person2.name = "李四";

person2.son.two = "B"; // person1 也会变

console.log(person1,person2)
// 浅拷贝
function clone(origin,target){
    let tar = target||{};
    for(let key in origin){
        if(origin.hasOwnProperty(key)){
            tar[key] = origin[key]
        }
    }
    return tar;
}
```
// TODO 需要再看看
function deepClone(origin,target){
    let tar = target||{};
    let toStr = Object.prototype.toString;
    let arrType = '[object Array]';

    for(let key in origin){
        if(origin.hasOwnProperty(key)){
            if(typeof(origin[key])==="object"&&origin[key]!==null){
                if(toStr.call(origin[key])===arrType){
                    tar[key] = []
                }else{
                    tar[key] = {}
                }
                deepClone(origin[key],tar[key])
            }else{
                tar[key] = origin[key]
            }
            
        }
    }
}
```

**千万不要用JSON.stringify()去实现深拷贝**

- 当对象中有时间类型的元素时候 -----时间类型会被变成字符串类型数据
- 当对象中有undefined类型或function类型的数据时 --- undefined和function会直接丢失
- 当对象中有NaN、Infinity和-Infinity这三种值的时候 --- 会变成null
- 当对象循环引用的时候 --会报错