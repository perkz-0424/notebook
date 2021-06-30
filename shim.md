### shim.js
~~~~
#先install一下
npm i --save react-native-crypto
npm i --save react-native-randombytes
react-native link react-native-randombytes
npm i --save-dev tradle/rn-nodeify
~~~~
~~~~json
#在package.json里添加如下:
"nodeify": "rn-nodeify --hack --install process,crypto,events,constant,console,stream,url,util",
"postinstall": "yarn nodeify"
~~~~
~~~~
#跑nodeify
yarn nodeify
~~~~
~~~~
这样就有一个shim.js文件
~~~~
~~~~jsx
import "./shim";
~~~~
~~~~
接下来就可以使用Buffer等node元素但是crypto这个node包与原生的包有所不同
~~~~