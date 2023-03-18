# requestAnimationFrame 

## 实现动画的方式
- JavaScript：setTimeout 和 setInterval
- Css3：transition 和 animation
- Html：canvas 和 SVG
- requestAnimationFrame API

## 是什么
请求动画帧，也称 帧循环

## 怎么玩
告诉浏览器你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。
```

(() => {
  let n = 0
  function test() {
    n++
    console.log(`🚀🚀hello ~ requestAnimationFrame ${n}`);
    requestAnimationFrame(test)
  }
  // 注意：若你想在浏览器下次重绘之前继续更新下一帧动画，那么回调函数自身必须再次调用
  requestAnimationFrame(test)
})()

```

## 执行频率
根据浏览器屏幕刷新次数自动调整了，也就是说浏览器屏幕刷新多少次，它就执行多少次。
屏幕刷新频率（次数）： 屏幕每秒出现图像的次数。普通笔记本为60Hz。

## 回调参数
回调函数会被传入`DOMHighResTimeStamp`参数，指示当前被 `requestAnimationFrame()` 排序的回调函数被触发的时间。
```
(() => {
  function test(timestamp) {
    console.log(`🚀🚀hello ~ requestAnimationFrame ${timestamp}`);
    requestAnimationFrame(test)
  }
  requestAnimationFrame(test)
})()
```
## 浏览器的自我拯救
为了提高性能和电池寿命，因此在大多数浏览器里，当`requestAnimationFrame()` 运行在后台标签页或者隐藏的`<iframe>`里时，`requestAnimationFrame()`会被暂停调用以提升性能和电池寿命。

## 返回值
一个 long 整数，请求 ID ，是回调列表中唯一的标识。是个非零值，没别的意义。

## 终止执行

只需要把`requestAnimationFrame`的返回值作为参数传递给`cancelAnimationFrame`就可以了。

链接：https://juejin.cn/post/6991297852462858277