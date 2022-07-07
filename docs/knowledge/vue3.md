# vue3

## ref 与 reactive 区别

```typescript
class RefImpl{
    get value(){
        
    }
    set value(newVal){
        
    }
}
```
因为string类型又不被proxy支持 ,ref是利用class提供的get和set来做的操作拦截：get时收集依赖，set时派发更新。  
reactive 则用是proxy

```typescript
const proxy = new Proxy(target,{
    get():()=>{
        
    },
    set:()=>{
        
    }
})
```

 

