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
##### FlexBox 布局 不用写display
###### justifyContent
~~~~
垂直布局
~~~~
###### alignItems
~~~~
水平布局
~~~~
##### 定位
~~~~
position: "relative" //定位
index: 2,//层级关系
elevation: 2,//和zIndex一起做层级关系

1.对于android:
既没有zIndex属性，又没有elevation属性      由其摆放位置决定的，放在里面的组件会在上层
两个组件只有zIndex没有elevation属性时      zIndex大的在上层
两个组件有elevation属性                   elevation大的在上层
两个组件既有zIndex属性elevation属性        以elevation为准

2.对于ios
同层级的组件，z轴的层叠关系只与摆放顺序与zIndex有关，与elevation无关
~~~~
##### shadow 阴影
###### shadowColor
~~~~jsx
shadowColor: "#000"
~~~~
###### shadowOffset
~~~~jsx
shadowOffset: { width: 0, height: 2 }
~~~~
###### shadowOpacity
~~~~jsx
shadowOpactity: 0.3
~~~~

#### 页面的渲染
##### 定义数据
~~~~jsx
const [lxy, setLxy] = useState([]);
~~~~
##### 获取数据
~~~~jsx
useMemo(() => {
  fetch("http://192.168.31.91:3001/app/get_some_value").then(res => {
    res.json().then(data => {
        setLxy(data);
      }
    );
  });
}, []);
~~~~
##### 渲染数据
~~~~jsx
<View>
  {
    lxy.map((item, index) => {
      return(
        <Text key={index}>{item.name}</Text>
      )
    })
  }
</View>
~~~~

#### fetch请求
##### 定义get请求
~~~~jsx
import config from "../../config";

const { URL } = config;
//get请求
const get = (url, signal) => {
  return new Promise((resolve, reject) => {
    fetch(`${URL}${url}`, {
      method: "get",//get请求
      signal,//用于终止请求
      //还有参数：headers、body、cache、mode、redirect、referrer
    }).then(res => {
      res.json().then(resolve).catch(reject);
    }).catch(reject);
  });
};
const instance = {
  get,
};
export default instance;
~~~~
##### 定义每一个get接口
~~~~jsx
import instance from "../fetch";

const getValue = (url) => {
  const controller = new AbortController();
  return {
    getValueImplement: () => instance.get(url, controller.signal),//执行
    getValueAbort: () => controller.abort(),//终止
  };
};
export default getValue;
~~~~
##### 使用接口
~~~~jsx
import getValue from "../../../servers/getValue";

const { getValueImplement, getValueAbort } = getValue("/app/get_some_value");//先结构出来
useMemo(() => {
getValueImplement().then((data) => {
    setLxy(data);
  });
}, []);

~~~~
##### 关闭接口，中断请求
~~~~jsx
const { getValueImplement, getValueAbort } = getValue("/app/get_some_value");

useEffect(() => {
  return () => {
    getValueAbort();//卸载时调用
  };
}, []);
~~~~