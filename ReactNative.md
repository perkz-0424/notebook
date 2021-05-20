### React-Native
#### 创建react-native项目
~~~~
react-native init 项目名称 react-native版本
react-native init ablums --version react-native@0.42
~~~~
#### react-native-cli手脚架创建react-native项目
~~~~
sudo npm install -g react-native-cli
~~~~
#### 启动项目
~~~~
react-native run-ios
react-native run-android
~~~~
#### command+D -> 打开控制台
#### 项目的基本步骤
##### 1.导入React和ReactNative
~~~~jsx
import React from "react";
import ReactNative, { View } from "react-native";
~~~~
##### 2.创建component函数（hooks）
~~~~jsx
const App = () => {
  return (
    <View></View>
  );
};
~~~~
##### 3.将代码渲染在模拟器上
~~~~javascript
AppRegistry.registerComponent(appName, () => App);
~~~~
#### React和ReactNative的比较
##### React
~~~~
React定义了Component是什么，以及它的工作模式
React定义并实现了让不同Component交互与协作机制
~~~~
##### ReactNative
~~~~
主要用于将Component的输出显示在具体的设备上
提供了平台无关的各种预定义组件，比如:View,Text,Image,ListView等
~~~~
#### View 
~~~~
是reactNative相当于HTML里的div
~~~~
#### ReactNative的样式
##### FlexBox
###### justifyContent
~~~~
垂直布局
~~~~
###### alignItems
~~~~
水平布局
~~~~
##### shadow 阴影
###### shadowColor
~~~~
shadowColor: "#000"
~~~~
###### shadowOffset
~~~~
shadowOffset: { width: 0, height: 2 }
~~~~
###### shadowOpacity
~~~~
shadowOpactity: 0.3
~~~~
~~~~
position: "relative" //定位
index: 2,//层级关系
elevation: 2,//和zIndex一起做层级关系

1.对于android:
既没有ZIndex属性，又没有elevation属性----->由其摆放位置决定的，放在下面的组件会在上层
两个组件只有zIndex没有elevation属性时----->zIndex大的在上层
两个组件有elevation属性----->elevation大的在上层
两个组件既有zIndex属性elevation属性----->以elevation为准

2.对于ios
同层级的组件，z轴的层叠关系只与摆放顺序与zIndex有关，与elevation无关
~~~~

##### 