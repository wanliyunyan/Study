# callee与caller

### callee caller

```
function test(a,b,c){
    console.log(arguments.callee.length) // 3
    console.log(test.length) // 3 形参数量
    console.log(arguments.length) // 2 实参数量
}

test(1,2) 

callee 正在执行的函数


function test1(){
    console.log(arguments.callee)
    function test2(){
        console.log(arguments.callee)
    }
    test2()
}
test1() // 各自打印自己的



let sum  = (function(n){
    if(n<1){
        return 1;
    }
    return n + arguments.callee(n-1) //匿名函数没有函数名
})(10)

caller 更没有用
谁调用的当前函数，则返回谁调用的这个函数的函数

function test1(){
    test2()    
}
function test2(){
    consolelog(test2.caller)  //打印test1
}
test1() 

