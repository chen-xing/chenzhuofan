## 如何实现跨浏览器共享cookies

###  1、cookies说明

> cookies是浏览器缓存与服务之间数据的一种手段，是浏览器的默认行为；不通的浏览器的cookies在硬盘的存储位置是不同的
>
> cookies存在域名使用限制，有效期，是否前端js可以操作，读取等属性



### 2、场景说明

+ 用户在浏览器A上操作,调用第三方，跳转到第三方App
+ 在App上完整业务后根据回调地址就行跳转回原来的业务系统
+ app唤起的浏览器B,(非跳转前的浏览器A),因为app有自己唤起浏览器逻辑。当手机上存在多个浏览器存在此问题
+ 浏览器B无之前的会话状态，后续操作失败，直接跳转到登录页面



### 3、解决方案

![解决方案](D:\data\dataImages\跨浏览器cookies共享.png)



### 4、重点说明

> 核心的逻辑是跳转前吧会话缓存到服务端
>
> 跳转的时候携带会话缓存key
>
> 跳转后根据会话缓存key获取缓存内容，还原会话状态

### 5、后续

更多精彩，敬请关注， [ 程序员导航网](https://chenzhuofan.top)  [https://chenzhuofan.top](https://chenzhuofan.top)

![程序员导航网](D:\data\dataImages\卓帆网.png)