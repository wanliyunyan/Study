# 杂七杂八

## fn.apply(this,arguments))  
这种写法只是因为参数不固定，如果this没有在fn用到，传null也可以

## [].shift.call(arguments)与 [].slice.call(arguments)

slice 方法原理就是根据传入的参数（值）对原数组（或者类数组）进行遍历获取，赋给新数组然后返回。如果没有参数便复制整个原数组（或者类数组），后赋给新数组然后返回。
因为slice内部实现是使用的this代表调用对象。那么当[].slice.call() 传入 arguments对象的时候，通过 call函数改变原来 slice方法的this指向, 使其指向arguments，并对arguments进行复制操作，而后返回一个新数组。至此便是完成了arguments类数组转为数组的目的！

     

