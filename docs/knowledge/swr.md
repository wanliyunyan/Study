# swr

SWR is a React Hooks library for remote data fetching.
The name “SWR” is derived from stale-while-revalidate, a cache invalidation strategy popularized by HTTP RFC 5861.
SWR first returns the data from cache (stale), then sends the fetch request (revalidate), and finally comes with the up-to-date data again.

这个一个非常伟大的lib，配合react hook真的很爽，非常推荐大家使用，现在的中文资料不是很多。

用了这个lib以后最大的好处就是很多请求只有GET的组件，可以彻底从项目中解耦，一定要注意，这个lib只适合GET的请求，可别POST。
另外配合?.这种写法，真的是天衣无缝，避免了大量空值的判断。
乐观更新彻底颠覆了传统的悲观更新的做法
总的来说，这个lib非常适合大数据时代

##这里面有一个坑
我还没有想明白，就是useSWR中的回跳函数从redux中取值，取不到值，暂时还没有想明白为什么。

##心得1
如果在编辑页面使用了swr，切记在保存之后使用 `revalidate` 更新一下缓存中的数据，不然下一次进入页面的时候读取的是上一次的数据，会让人觉得很奇怪