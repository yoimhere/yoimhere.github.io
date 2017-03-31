---
layout: post
title: ReactNative之布局学习笔记
description: 弹性（Flex）宽高、Flex Direction、 Align Items、Justify Content
categories: ReactNative，RN，跨平台开发
tags: ReactNative

---
### 弹性（Flex）宽高

简单的说就是width或height值等(该View的Flex/同层的Views的Flex的总和)

>组件能够撑满剩余空间的前提是其父容器的尺寸不为零。如果父容器既没有固定的width和height，也没有设定flex，则父容器的尺寸为零,其子组件如果使用了flex，也是无法显示的。

### Flex Direction

**决定布局的方向**,默认值是垂直方向(column)，水平方向排列为row

### Align Items

**决定其子元素与Flex Direction不同的方向的排列方式**,这些可选项有：flex-start、center、flex-end以及stretch。

>注意：要使stretch选项生效的话，子元素在与Flex Direction不>同的方向上不能有固定的尺寸

### Justify Content

**决定其子元素沿着Flex Direction方向的排列方式**,可选项有：flex-start、center、flex-end、space-around以及space-between。

```
 <View style={{flex: 1,flexDirection: 'column',  justifyContent: 'X'}}>
           <View style={{backgroundColor:'red', width:30 , height:50}}/>
           <View style={{backgroundColor: 'blue', width:30 , height:50}}/>
           <View style={{backgroundColor: 'green', width:30 , height:50}}/>
 </View> );
```
当X = 'space-between'
![space-between.png](http://upload-images.jianshu.io/upload_images/157410-c4a3d81fd0b1cf17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/310)

当X = 'center'

![center.png](http://upload-images.jianshu.io/upload_images/157410-b3d523f4f22620f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/310)

当X = 'flex-end'
![flex-end.png](http://upload-images.jianshu.io/upload_images/157410-9b07c2662ef08072.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/310)

当X = 'space-around'

![space-around.png](http://upload-images.jianshu.io/upload_images/157410-22d913ada8a070c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/310)

当X = 'flex-start'

![flex-start.png](http://upload-images.jianshu.io/upload_images/157410-45aab586559567af.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/310)

### 参考链接：
[RN中文社区](http://reactnative.cn/docs/0.42/layout-with-flexbox.html#content)

