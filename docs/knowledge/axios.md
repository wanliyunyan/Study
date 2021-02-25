# axios

##好坑的一个事

项目中 `axios.defaults.baseURL= /api/v1`   
调用接口 调用的 /a/b

但是项目路径是 `www.***.com/***/ `

接口接口都404了
调用的地址 `www.***.com/api/v1/***/a/b`

我的天,至今不理解为什么,也不知道怎么改,被迫把接口都改成`/api/v1/a/b`

