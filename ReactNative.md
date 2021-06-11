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
                           _______________Store_______________
                          /                                   \                
                          |                                   |
                          |                                   |
         Action -----—————|—--->Reducer-----—--->State        |                    
一个JS对象，用于告知Reducer  |  返回数据的函数  应用程序中的具体Data  |
       如何改变数据         |                                   |                   
                          \___________________________________/
~~~~

#### 十七.官方组件
##### 1.ActivityIndicator(loading动态图)
~~~~jsx
<ActivityIndicator 
  size="small" //尺寸 可以是large、small也可以是number
  color="#0000ff" //颜色 android没有默认色、ios默认色是#999
  //animating 是否动画 默认是true
  // hidesWhenStopped 在animating为 false 的时候，是否要隐藏指示器（默认为 true）。如果animating和hidesWhenStopped都为 false，则显示一个静止的指示器。（ios）
/>
~~~~
##### 2.Button
~~~~jsx
<Button
  onPress={() => {}} //按下事件 fn
  title="按钮" //按钮里的文字 str
  disabled={false} //是否禁用 bool true为禁用
  color="#f40" //文本的颜色(iOS)，或是按钮的背景色(Android)
  //accessibilityLabel 用于给残障人士显示的文本（比如读屏应用可能会读取这一内容）str
/>
~~~~
##### 3.FlatList 高效渲染数据列表，继承了ScrollView
~~~~jsx
<FlatList
  data={value} //数据源
  renderItem={({ item, index }) =><TouchableOpacity key={index} onPress={() => {}}><Image uri={item["imageSrc"]}/></TouchableOpacity>} //数据渲染
  keyExtractor={item => item.name} //key
/>
~~~~
##### 4.SectionList，支持分组的头部组件，继承了VirtualizedList
~~~~jsx
//和FlatList用法差不多
<SectionList
  sections={value}
  keyExtractor={(item, index) => item + index}
  renderItem={({ item }) => <Item title={item} />}
  renderSectionHeader={({ section: { title } }) => (<Text style={styles.header}>{title}</Text>)}
/>
~~~~
##### 5.ScrollView
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
##### 6.VirtualizedList SectionList和FlatList的底层实现,渲染固定区域的组件，离开区域则不渲染

##### 7.ImageBackground 背景图片
~~~~jsx
<View style={{ flex: 1, flexDirection: "column" }}>
  <ImageBackground
    style={{ flex: 1, resizeMode: "cover", justifyContent: "center" }}
    source={{ uri: "https://zh-hans.reactjs.org/logo-og.png" }}
   >
    <Text>
      React Native
    </Text>
  </ImageBackground>
</View>
~~~~
##### 8.KeyboardAvoidingView 根据弹出的键盘调整height或者底部padding以免被挡住
~~~~jsx
<KeyboardAvoidingView
  behavior={Platform.OS === "ios" ? "padding" : "height"} //三种值height、position、padding
  style={{ flex: 1 }}
  //contentContainerStyle 如果设定 behavior 值为'position'，则会生成一个 View 作为内容容器。此属性用于指定此内容容器的样式。
  //enabled 是否启用 KeyboardAvoidingView bool
  //keyboardVerticalOffset 有时候应用离屏幕顶部还有一些距离（比如状态栏等等），利用此属性来补偿修正这段距离。
>
  <Header searchSubmit={() => {}}/>
</KeyboardAvoidingView>
~~~~
##### 9.Modal
~~~~jsx
<Modal
  animationType="slide"
  transparent={true}
  visible={false}
>
  <Text>Hello World!</Text>
</Modal>
~~~~
##### 10.Pressable 长按
~~~~jsx
<Pressable
  onPress={() => {}}
  //android_disableSound bool是否有按压的声音
  //android_ripple RippleConfig 使用并配置 Android 波纹效果。
  //children 接收按压状态布尔值的子节点
  //delayLongPress 从 onPressIn 触发到 onLongPress 被调用的时间间隔（毫秒）
  //disabled 是否禁用按压行为
  //hitSlop 设置元素能够检测到按压动作的额外距离
  //onLongPress 在 onPressIn 持续超过 500 毫秒后调用
  //onPressIn 在 onPressOut 和 onPress 之前， 按压后立即调用
  //onPressOut 松开手后调用
  //pressRetentionOffset 在 onPressOut 被触发前，view 额外的有效触控距离
>
...
</Pressable>
~~~~
~~~~
android_ripple 属性的波纹效果配置
 1.color color 定义波纹的颜色
 2.borderless bool 定义波纹效果是否包含边框
 3.radius num 定义波纹的半径
~~~~
##### 11.RefreshControl 用在ScrollView、FlatList里用于下拉刷新
~~~~jsx
<FlatList
  refreshControl={<RefreshControl refreshing={false} onRefresh={() => {}}/>}
/>
~~~~
~~~~jsx
<RefreshControl 
  refreshing={true}//视图是否应该在刷新时显示指示器
  onRefresh={() => {}}//下拉回调
  //colors android array of color 指定至少一种颜色用来绘制刷新指示器
  //enabled bool android 指定是否要启用刷新指示器
  //progressBackgroundColor color android 指定刷新指示器的背景色
  //progressViewOffset num android 指定刷新指示器的垂直起始位置(top offset)。
  //size enum(RefreshLayoutConsts.SIZE.DEFAULT, RefreshLayoutConsts.SIZE.LARGE) android 指定刷新指示器的大小
  //tintColor color 指定刷新指示器的颜色 ios
  //title str ios 指定刷新指示器下显示的文字
  //titleColor color 指定刷新指示器下显示的文字的颜色 ios 
/>
~~~~
##### 12.TouchableHighlight
~~~~
触摸颜色可变化
~~~~
##### 13.TouchableOpacity
~~~~
触摸透明度变化
~~~~

#### 十八.官方API
##### 1.Platform.OS
~~~~jsx
//判断是不是ios
Platform.OS === "ios"
~~~~
##### 2.AccessibilityInfo
~~~~jsx
//判断用户是否在读屏
~~~~
###### （1）AccessibilityInfo.fetch() 查询屏幕阅读器当前是否启用
~~~~jsx
AccessibilityInfo.fetch().done((bool) => {
  //bool为true则正在读屏，反之则不再读屏
})
~~~~
###### (2) AccessibilityInfo.addEventListener(eventName, handler) 监听是否读屏
~~~~jsx
AccessibilityInfo.addEventListener("change", handler); //change也可以是announcementFinished用于ios
const handler = (e) => {console.log(e)} //返回读屏是否启用的布尔值
~~~~
###### (3) AccessibilityInfo.setAccessibilityFocus() 将可访问性焦点设置为反应组件 ios
###### (4) AccessibilityInfo.removeEventListener(eventName, handler) 删除事件处理程序

##### 3.Alert 弹框
~~~~jsx
Alert.alert(title, message?, buttons?, options?, type?)
~~~~
~~~~
title: 弹出的字
message:对话框标题下会显示一条可选消息
buttons:按钮
~~~~
##### 4.Animated 流畅动画 View、Text、Image、ScrollView、FlatList和SectionList可以使用
