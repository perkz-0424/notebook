### React-Native
#### 一.创建react-native项目
~~~~
react-native init 项目名称 react-native版本
react-native init ablums --version react-native@0.42
~~~~
#### 二.react-native-cli手脚架创建react-native项目
~~~~
sudo npm install -g react-native-cli
~~~~
#### 三.启动项目
~~~~
react-native run-ios
react-native run-android
~~~~
#### 四.command+D -> 打开控制台
#### 五.项目的基本步骤
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
#### 六.React和ReactNative的比较
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
#### 七.View 
~~~~
是reactNative相当于HTML里的div
~~~~
#### 八.ReactNative的样式
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

#### 九.页面的渲染
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
#### 十.react-native-antd的引入
##### 1.install antd
~~~~
npm install @ant-design/react-native --save
npm install react-native-vector-icons --save
react-native link @ant-design/react-native
react-native link @ant-design/icons-react-native
~~~~
##### 2.install babel
~~~~
npm install babel-plugin-import --save
~~~~
##### 根目录新建.babelrc
~~~~js
{
  "plugins": [
    ["import", { libraryName: "@ant-design/react-native" }] // 与Web平台的区别是不需要设置 style
  ]
}
~~~~
#### 十一.主题颜色
###### 1.准备两个主题的文件(一个暗色、一个亮色)
~~~~
dark.js和light.js
~~~~
###### 2.将颜色文件、改变颜色函数、颜色主题的名字放在Context里
~~~~jsx
import React, { useState } from "react";
import lightAntdStyle from "../../assets/style/theme/light";
import darkAntdStyle from "../../assets/style/theme/dark";

const ThemeContext = React.createContext();
const Provider = ThemeContext.Provider;
const themes = { "light": lightAntdStyle, "dark": darkAntdStyle, };
const Theme = ({ children }) => {
  const [theme, changeTheme] = useState("light");
  return (<Provider value={{ theme: themes[theme], themeName: theme, changeTheme }}>{children}</Provider>);
};

export { ThemeContext };
export default Theme;
~~~~
###### 3.Theme包裹整个App
~~~~jsx
const Root = () => {
  return (
    <Theme><App/></Theme>
  )
};
~~~~
###### 4.添加antd-mobile主题
~~~~jsx
import { Provider } from "@ant-design/react-native";
import { ThemeContext } from "./src/components/Theme/Theme";

const App = () => {
  const { theme } = useContext(ThemeContext);//主题
  return (
      <Provider theme={theme}><Home/></Provider>
  );
};
~~~~
###### 5.添加自定义颜色
~~~~jsx
import React, { useState, useContext } from "react";
import { ThemeContext } from "../../../components/Theme/Theme";

const { theme, themeName } = useContext(ThemeContext);//主题

//使用：backgroundColor: theme.background_color,

//如果是antd-mobile组件要加上key（因为antd-mobile组件渲染）
<View style={style.header} key={themeName}>
    <SearchBar
      style={style.searchBar}
      placeholder="搜索你想看的"
      value={searchValue}
      onChange={searchChange}
      onSubmit={searchSubmit}
      onCancel={searchCancel}
    />
</View>
~~~~
###### 6.改变主题
~~~~jsx
const { changeTheme, theme, themeName } = useContext(ThemeContext);
changeTheme("dark");
changeTheme("light");
~~~~
#### 十二.Image
~~~~jsx
//Image必须是有宽高，可以根据高度用flex去自适应宽度
<Image
   source={{ uri: "图片的引用地址" }}
   style={{ height: 200, flex: 1 }}
/>
~~~~

#### 十三.ScrollView
~~~~
如果使用了ScrollView，那最顶端view必须是以flex形式存在
~~~~
~~~~jsx
<ScrollView style={style.bodyStyle}>
  {
    props.searchResult.map((item, index) => {
      return (
        <View key={index} style={style.card}>
          <Text style={{ color: theme.font_color }}>{item.title}</Text>
        </View>
      );
    })
  }
</ScrollView>
~~~~
~~~~jsx
//最外层的View
<View style={{ flex: 1 }}></View>
~~~~
#### 十四.按钮Button
~~~~
react-native官方有Button，也可以自己写Button
~~~~
~~~~jsx
import React, { useContext } from "react";
import { Text, TouchableOpacity } from "react-native";
import { ThemeContext } from "../../store/Theme/Theme";

const Button = props => {
  const { theme } = useContext(ThemeContext);
  const styles = {
    buttonStyle: {
      borderWidth: 1,
      borderRadius: 1,
      padding: 8,
      borderColor: theme.button_border_color,
      width: props.width
    },
    text: {
      textAlign: "center",
      fontSize: 14,
      color: theme.button_border_color
    }
  };
  return (
    <TouchableOpacity style={styles.buttonStyle} onPress={props.onPress}>
      <Text style={styles.text}>
        {props.children}
      </Text>
    </TouchableOpacity>
  );
};
export default Button;
~~~~
~~~~jsx
<Button onPress={LinkingToBaidu}>Baidu</Button>
~~~~
#### 十五.Linking跳转（可以跳转别的app）
~~~~jsx
import { Linking } from "react-native";

Linking.openURL("https://www.baidu.com").then(()=>{});
~~~~

#### 十六.Redux（js库）
~~~~
                                     掌管应用程序数据的对象
                           _________________Store__________________
                          |                                        |                 
                          |                                        |
                          |                                        |
         Action -----—————|———--->Reducer-----—————--->State       |                    
一个JS对象，用于告知Reducer  |     返回数据的函数     应用程序中的具体数据  |
       如何改变数据         |                                        |                   
                          |________________________________________|
~~~~
