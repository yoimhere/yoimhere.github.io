---
layout: post
title: ReactNative之iOS Image无法显示http图片问题
description: 准备入门ReactNative, 写了个Image显示网络图片的
tags: ReactNative

---
准备入门ReactNative, 写了个Image显示网络图片的

```
import React from 'react';
import {Image,View,AppRegistry} from 'react-native';

export default class App extends React.Component{
  render(){
      let picUrl = {
          uri: "http://xxxx.jpg"
      }
      return (
        <View style={{backgroundColor: 'red'}}>
            <Image source={picUrl} style={{width: 193, height: 210}}/>
        </View>
      );
  };
}
AppRegistry.registerComponent('HelloWorld', () => App);
```

运行在`iOS模拟器`上,无法显示图片

在Info.list 加个Allow Arbitrary Loads -> Yes
依然无法显示图片

给uri整个https的网络图片路径，搞定

