判断元素是否在可视区域中

在前端开发中，有些时候我们需要等到目标元素出现在视口中(被用户看到)才进行某些操作，最常见的就是数据懒加载，比如图片的懒加载，这样做的意义是：

- 快速地呈现第一屏数据给用户(假设一个页面很多图片，如果一下子全部加载，接口返回较慢，会阻塞页面的渲染，用户可能需要好几秒甚至更久的时间才能看到内容，这是不能忍受的)
- 缓解服务器的压力(一个页面有很多图片，用户可能只看了第一屏或者前几屏的图片，后面就不往下看了，这时候后面的图片就失去了加载的意义，耗费了服务器资源却得不到相应的收益)


```
<script setup>
  import {onMounted, onBeforeUnmount, ref} from 'vue'

  const observer = ref(null)

  onMounted(() => {
    const observerCallback = (entries) => {
      entries.forEach(entry => {
        if (entry.intersectionRatio > 0) { // 被观察者进入视口
          console.log(entry.target.id)
        }
      });
    }
    // 初始化观察者实例
    observer.value = new IntersectionObserver(observerCallback)

    // 开始观察目标元素
    observer.value.observe(document.getElementById('content1'))
    observer.value.observe(document.getElementById('content2'))
    observer.value.observe(document.getElementById('content3'))
    observer.value.observe(document.getElementById('content4'))
    observer.value.observe(document.getElementById('content5'))
    observer.value.observe(document.getElementById('content6'))
  })

  onBeforeUnmount(() => {
     // 停止观察目标元素
    observer.value.unobserve(document.getElementById('content1'))
    observer.value.unobserve(document.getElementById('content2'))
    observer.value.unobserve(document.getElementById('content3'))
    observer.value.unobserve(document.getElementById('content4'))
    observer.value.unobserve(document.getElementById('content5'))
    observer.value.unobserve(document.getElementById('content6'))
  })
</script>

```


<b>intersectionRatio</b> 属性(目标元素与视口的交叉比例) 的取值区间为 [0-1]，为0则目标元素完全不可见，为1则目标元素完全可见，其具体取值可根据实际需要来调整，比如如果希望目标元素的一半以上出现在视口中再进行业务逻辑操作，则 <code>entry.intersectionRatio > 0.5</code>


现在假设每个目标元素可见时，就加载其对应的数据填充到页面上，我们补充一下代码，为了保证个目标元素的数据只加载一次，我们给每个目标元素一个控制变量，标志其是否已经进入过视口，当目标元素进入视口时，如果其数据已经加载过，则不再加载

```

const hasLoadedData = ref({
    'content1':false,
    'content2':false,
    'content3':false,
    'content4':false,
    'content5':false,
    'content5':false,
  })

const loadData = (target) => {
   console.log(target)
   // 具体的请求逻辑
   // ...
 }

const oberverCallback = (entries) => {
      entries.forEach(entry => {
        if (entry.intersectionRatio > 0) { // 被观察者进入视口
          switch (entry.target.id) {
            case 'content1':
              {
                if (!hasLoadedData.value['content1']) { // 第一次加载
                  loadData('content1') // 加载数据
                  hasLoadedData.value['content1'] = true  // 加载完数据后，把其标记为已加载
                }
              }
            break
            case 'content2':
              {
                if (!hasLoadedData.value['content2']) { 
                  loadData('content2')
                  hasLoadedData.value['content2'] = true
                }
              }
            break
            case 'content3':
              {
                if (!hasLoadedData.value['content3']) { 
                  loadData('content3')
                  hasLoadedData.value['content3'] = true
                }
              }
            break
            case 'content4':
              {
                if (!hasLoadedData.value['content4']) {
                  loadData('content4')
                  hasLoadedData.value['content4'] = true
                }
              }
            break
            case 'content5':
              {
                if (!hasLoadedData.value['content5']) { 
                  loadData('content5')
                  hasLoadedData.value['content5'] = true
                }
              }
            break
            case 'content6':
              {
                if (!hasLoadedData.value['content6']) { 
                  loadData('content6')
                  hasLoadedData.value['content6'] = true
                }
              }
            break
            default:
              break
          }
          
        }
      });
    }
```

https://blog.csdn.net/weixin_42650595/article/details/128551249