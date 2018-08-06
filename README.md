# Applet-of-WeChat
微信小程序入门学习-极客时间-9小时搞定微信小程序开发

第二讲: 什么是小程序

- 小程序是一种不需要下载安装即可使用的应用
- 用户扫一扫或者搜一下即可打开应用，体现了"用完即走"的理念
- 用户不用关心是否安装太多应用的问题

小程序与应用程序区别:

- 无需安装
- 不占内存
- 易传播

小程序开发准备工作:
(https://developers.weixin.qq.com/miniprogram/dev/)

1. 注册小程序账号(微信公众平台-小程序)
2. 激活邮箱
3. 信息登记
4. 登录小程序管理后台
5. 完善小程序信息
6. 绑定开发者

小程序代码结构与基本配置:

1. app.js: 注册微信小程序应用
2. app.json: 全局配置，网络请求超时时间，页面注册路径
3. app.wxss: 全局样式

小程序代码结构与基本配置:

app:

1. Pages: 注册所有页面
2. tabBar: 多tab
3. networkTimeout: 各个网络请求超时时间
4. debug: 打印需要的调试信息
5. navigationStyle

app&page:

1. navigationBarBackgroundColor
2. navigationBarTextStyle
3. navigationBarTitileText
4. backgroundColor
5. backgroundTextStyle
6. onReachBottomDistance
7. enablePullDownRefresh

disableScroll开启是否滚动

共有五个版本:

- 预览版本
- 开发版本 体验版本
- 审核版本
- 线上版本

一个微信小程序至少要有两个文件: app.js和app.json

app.js注册小程序应用
app.json: 全局配置

helloworld.wxml 页面元素
helloworld.js 注册页面
helloworld.json 配置
helloworld.wxss 页面样式

微信小程序开发框架--基本构成:

- WXML
- WXSS
- WXS
- Java Script

WXS: WeiXin Markup Language，是框架设计的一套标签语言，结合组件、WXS和事件系统，可以构建出页面的结构。

```
<标签名 属性名 = "属性名1" 属性名="属性名2" ...>
...
</标签名>
```

WXML:

- 数据绑定
- 列表渲染
- 条件渲染
- 模板引用

__数据绑定:__实现数据的更新

```
//绑定文本
<!--index.wxml-->
<view>
	<text>{{message}}</text>
</view>
//index.js
Page({
data:({
	message: "Hello, World"
})
}
)
```

```
//绑定属性
<!--index.wxml-->
<view>
	<text data-name="{{theName}}"></text>
</view>
//index.js
Page({
	data:{
		theName: "Jack"
}
})
```

```
//运算符绑定
<!--index.wxml-->
<view hidden="{{flag?true:false}}">
	Hidden
</view>
//index.js
Page({
	data: {
		flat: false
}
})
```

微信小程序开发框架--属性

属性名      类型      描述      注解

id String 组件的唯一标示  保持整个页面唯一

class String 组件的样式类 在对应的WXSS中定义的样式类

style String 组件的内联样式 可以动态设置的内联样式

hidden Boolean 组件是否显示 所有组件默认显示

data-* Any 自定义属性 组件上触发的事件时，会发送给事件处理函数

bind*/catch* EventHandler 组件的事件 详见事件


####微信小程序开发框架--列表渲染

```
<!--index.wxml-->
<view>
	<block wx: for="{{items}}" wx:for-item="item" wx:key="index">
		<view>{{index}}:{{item.name}}</view>
	</block>
</view>
//index.js
Page({
	data:{
		items:[
			{name:"商品A"},
			{name:"商品B"},
			{name:"商品C"},
			{name:"商品D"},
			{name:"商品A"},
		]
	}
})
```

####微信小程序开发框架--条件渲染

```
<!--index.wxml-->
<view>今天吃什么?</view>
<view wx:if="{{condition === 1}}">
	饺子
</view>
<view wx:elif="{{condition === 2}}">
	米饭
</view>
<view wx:else>
	面食
</view>
//index.js
Page({
	data:{
		condition: Math.floor(Math.random()*3+1)
	}
})
```

####微信小程序开发框架--模板引用

```
<!--index.wxml-->
<template name="template">
	<view>
		<view>收件人: {{name}}</view>
		<view>联系方式: {{phone}}</view>
		<view>地址: {{address}}</view>
	</view>
</template>
<template is="template" data="{{...item}}"></template>
//index.js
Page({
	data:{
		item: {
			name: "张三",
			phone: "18888888888",
			address: "中国"
		}
	}
})
```

文件引用: import、include

```
<!--index.wxml-->
<import src="a.wxml"></import>
<template is="a"></template>
<!--a.wxml-->
<view>Hello, world</view>
<template name="a">
	Hello, World!
</template>
```

import只能引用所定义的模板文件的模板内容块。

作用域的概念: 也就是说只能引用目标文件所定义的template模板，如果目标文件嵌套了其他文件的template模板，不会被引用

```
<!--index.wxml-->
<import src="a.wxml"></import>
<template is="a"></template>
<!--a.wxml-->
<import src="c.wxml" />
<template name="a">
	This is a.wxml
</template>
<template is="b"></template>
<!--b.wxml-->
<template name="b">
	This is b.wxml
</template>
```
避免了死循环的情况

include: 目标文件中除了模板代码块外的所有代码都引入，相当于拷贝到了include的位置。

```
<!--index.wxml-->
<include src="a.wxml" />
<template is="a">
</template>
<!--a.wxml-->
<template name="a">
	<view>
		This is a.wxml
	</view>
</template>
<view>Hello, world</view>
```

####微信小程序开发框架--WXSS

WXSS: WeiXin Style Sheets: 是一套样式语言， 用于描述WXML的组件样式。

CSS: Cascading Style Sheets: 是一套样式语言， 是一种样式表语言， 用来描述HTML或XML文档的呈现。

width height position color border

- 尺寸单位: rps 响应式的像素
- 样式导入
- 内联样式
- 选择器

- 设备像素device pixels
- CSS像素 CSS pixcls
- PPI/DPI pixel per inch
- DPR devicepixelRatio

屏幕分辨率:  X * Y

PPI = 开平方(X^2 + Y^2)/屏幕尺寸

以iPhone 6为例:

开平方(750^2 + 1334^2)/4.7 = 325.6

样式导入: @import

外联样式:

```
<!--index.wxml-->
<view class="container">
	Hello, world!
</view>

//index.wxss
@import './assets.wxss';
.container{
	color: red;
}

//assets.wxss
.container {
	border: 1px solid #000;
}

```

还支持内联样式:

```
<!--index.wxml-->
<view style="width: 500rpx;height:30px;background-coor:{{colorValue}}">
	Hello, world!
</view>
//index.js
Page({
	data: {
		colorValue: 'red'
	}
})

```

目前支持的选择器有: 

选择器        样例       样例描述

.class .intro  选择所有拥有class="intrl"的组件

\#id #firstname 选择拥有id="firstname"的组件

element view 选择所有view组件

element.element view, checkbox 选择所有文档的view组件和所有的checkbox组件

::after view::after 在view组件后边插入内容

::before view::before 在view组件前边插入内容

优先级:

- !important  无穷

- style 1000

- \#element 100

- .element 10

- element 1

####微信小程序开发框架--JavaScript

JavaScript是一种轻量的、解释型的、面向对象的头等函数语言，是一种动态的基于原型和多范式的脚本语言， 支持面向对象、命令式和函数式的编程风格。

两本书: 
JavaScript高级程序设计
JavaScript权威指南

小程序中的JavaScript: 

- ECMAScript
- 小程序框架
- 小程序API

浏览器中的JavaScript:

- ECMAScript
- DOM
- BOM

iOS -> JavaScriptCore

android -> X5内核

IDE -> nwjs

####微信小程序开发框架--WXS

模块、变量、注释、运算符、语句、数据类型、基础类库

模块:

```
<!--index.wxml-->
<wxs module="m1">
	module.exports = {
		message: 'Hello, world!'
	}
</wxs>

<view>{{m1.message}}</view>

<!--index.wxml-->
<wxs src = "./m2.wxs" module = "m2"></wxs>
<view>{{m2.message}}</view>
//m2.wxs
module.exprots = require('./m2.wxs')
//m1.wxs
module.exprots = {
	message: "hello world!"
}
```

注释: 

```
<!--index.wxml-->
<wxs module = "m3">
	var v = 1;
	module.exports.value = v;
	//单行注释
	/* 多行注释
	v += 1;
	*/
	console.log(v);
	/*
	var d = 3;
	console.log(d);
</wxs>
<view>{{m3.message}}</view>
```

//控制台只打印出1 d在注释后

运算符: 基本运算符、一元运算符、位运算符、比较运算符、等值运算符、赋值运算符、二元逻辑运算符


数据类型: number、string、boolean、object(对象类型)、array、function(函数类型)、date、regexp(正则类型)

date、regexp 使用get创建；

基础类库: Number、Date、Global、console、Math、JSON