### Taro
#### Taro内部转化图
~~~~
           Nerv(类React代码)
             （抽象语法树）  
模板（taro转化器）      组件库   Api   运行时框架
   Taro转化器                Taro运行时
                  Trao 
        Web端、App端、小程序端、快应用端      
~~~~
#### 安装
~~~~
1.安装Taro开发工具 @tarojs/cli
npm install -g @tarojs/cli
~~~~
#### 创建
~~~~
taro init appName
~~~~
#### 开发命令
~~~~
1. web: npm run dev:h5
2. 微信小程序: npm run dev:weapp
3. 支付宝小程序: npm run dev:alipay
4. 百度小程序: npm run dev:swan
5. RN: npm run dev:rn
~~~~
#### 编译就是把上面的dev换成build