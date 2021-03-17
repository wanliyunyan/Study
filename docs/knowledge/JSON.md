# JSON

## stringify
```
let a= {
    b:function(){}
}

console.log(a) //这里可以打印出函数
console.log(JSON.stringify (a)) // {} 在转成字符串的时候，函数没了
```
