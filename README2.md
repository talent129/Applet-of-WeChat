小程序的开发框架称为MINA框架:

- View视图层(page: WXML、WXSS)
- App Service逻辑层<Manager、 API>
- Native系统层(JSBridge；微信能力、离线存储、网络请求...)

####运行机制--启动

启动: 冷启动(用户首次打开，或小程序被微信销毁(5分钟或连续两次收到系统警告5s内)再次打开)、热启动

####运行机制--加载

####生命周期

程序生命周期: 

- onLaunch
- onShow
- onHide
- onError


页面生命周期: 

- onLoad
- onShow
- onReady
- onHide
- onUnload

####路由

路由方式         		页面栈表现

初始化				新页面入栈

打开新页面			新页面入栈

页面重定向			当前页面出栈，新页面入栈

页面返回			页面不断出栈，直到目标返回页，新页面入栈

Tab切换				页面全部出栈，只留下新的Tab页面

重加载				页面全部出栈，只留下新的页面

---

####微信小程序开发框架--事件

事件是视图层到逻辑层的通讯方式。
事件可以将用户的行为反馈到逻辑层进行处理。
事件可以绑定在组件上，触发事件后，就会执行逻辑层中对应的事件处理函数。
事件对象可以携带额外信息。


- 事件捕获阶段
- 事件处理阶段
- 事件冒泡阶段

可捕获事件:

touchstart、touchmove、touchcancel、touchend、tap、longpress、longtap

可冒泡事件:

touchstart、touchmove、touchcancel、touchend、tap、longpress、longtap、transitionend、animationstart、animationiteratin、animationend、touchforcechange

####组件

- 组件是视图层的基本组成单元；
- 组件自带一些功能与微信风格的样式
- 一个组件通常包括: 开始标签和结束标签；属性用来修饰这个组件，内容在两个标签之内。

组件: 媒体组件、地图、开放能力、画布、视图容器、基础内容、表单组件、导航

视图容器: view、scroll-view、swiper、movable-view、cover-view

hover-stop-propagation: 阻止父view 的点击效果

```
<!--index.wxml-->
<view class='section'>
  <view>view组件</view>
  <view class='view-parent-container' hover-class='hover-parent-container'>
    <view class='view-container' hover-stop-propagation='true' hover-class='hover-container' hover-start-time='500' hover-stay-time='300'>
    </view>
  </view>
</view>
```

```
/**index.wxss**/
.view-parent-container {
  width: 300rpx;
  height: 300rpx;
  background: yellowgreen;
}

.hover-parent-container {
  background: #fff;
}

.view-container {
  width: 200rpx;
  height: 200rpx;
  background: chocolate
}

.hover-container {
  background: rgba(0, 0, 0, 0.7)
}
```








