# iphone

##业界的毒瘤Safari


###图片引用

安卓的浏览器这样写 可以看到图片，但是 Safari就是不行

```
import a from "/assets/images/lbtfour.png";  

<img src={a as any } alt=""  />
```
只能这样写
```
<img src={"/assets/images/lbtfour.png"} alt=""  />
```

