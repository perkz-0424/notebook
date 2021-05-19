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
#### 启动ios项目
~~~~
react-native run-ios
react-native run-android
~~~~
#### command+D -> 打开控制台
#### 项目的基本步骤
##### 1.导入React和ReactNative
~~~~jsx
import React from "react";
import ReactNative from "react-native";
~~~~
##### 2.创建component函数（hooks）
~~~~jsx
const Home = () => {
  return (
    <View></View>
  );
};
~~~~
##### 3.将代码渲染在模拟器上
~~~~javascript
AppRegistry.registerComponent(appName, () => App);
~~~~
### React和ReactNative的比较
#### React
~~~~
React定义了Component是什么，以及它的工作模式
React定义并实现了让不同Component交互与协作机制
~~~~
#### ReactNative
~~~~
主要用于将Component的输出显示在具体的设备上
提供了平台无关的各种预定义组件，比如:View,Text,Image,ListView等
~~~~
