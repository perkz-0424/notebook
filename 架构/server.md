### fetch和axios
#### 一.fetch请求（app和web都可以使用）
~~~~
不需要引入
~~~~
##### 1.定义请求
~~~~jsx
import config from "../../config";

const { URL } = config;
//请求封装
const request = (method ,url, signal, body) => {
  return new Promise((resolve, reject) => {
    fetch(`${URL}${url}`, {
      headers: {//规定了参数是json
        "Accept": "application/json",
        "Content-Type": "application/json",
        //还可以把token带过去
      }
      method,//请求类型
      signal,//用于终止请求
      body,//请求体
      //还有参数：cache、mode、redirect、referrer
    }).then(res => {
      res.json().then(resolve).catch(reject);
    }).catch(reject);
  });
};
export default request;
~~~~
##### 2.定义一个post接口
~~~~jsx
import request from "../fetch";//从1里引入request

const getValue = (body) => {
  const controller = new AbortController();
  return {
    getValueImplement: () => request("post", "/app/get_some_value", controller.signal, JSON.stringify(body)),//执行(注：body转json)
    getValueAbort: () => controller.abort(),//终止
  };
};
export default getValue;
~~~~
##### 3.使用接口
~~~~jsx
import getValue from "../../../servers/getValue";//从2里引入

const { getValueImplement, getValueAbort } = getValue({ search_value: value, page: 1});//先结构出来
useMemo(() => {
   getValueImplement().then((data) => {
      setLxy(data);
   });
}, []);

~~~~
##### 4.关闭接口，中断请求
~~~~jsx
import getValue from "../../../servers/getValue";//从3里引入

const { getValueImplement, getValueAbort } = getValue("/app/get_some_value");/先结构出来
useEffect(() => {
  return () => {
    getValueAbort();//卸载时调用
  };
}, []);
~~~~

#### 二.axios请求（web端使用）
~~~~
需要引入
~~~~
##### 1.定义axios
~~~~js
import axios, { CancelToken } from "axios";
import webConfig from "../config";

/****>终止axios<****/
const CancelAxios = CancelToken.source();
const cancelAlwaysAxios = CancelAxios.cancel;//终止添加cancelAlwaysToken的请求(包括后续所有请求)
const cancelAlwaysToken = { cancelToken: CancelAxios.token };
/****>终止axios<****/

/****>配置axios<****/
const instance = axios.create({
  baseURL: webConfig.LocalHostURL,//localhost
  timeout: 30000,//请求超时时间
  headers: {
    "Content-Type": "application/x-www-form-urlencoded",
    //"Authorization": (读取cookie里的token),//这里可以取存在cookie里token返回给后端
  },
});
instance.interceptors.response.use(
  response => response,
  error => Promise.reject(error),
);
/*****>配置axios<*****/

export {
  instance,//重新定义的axios请求
  CancelToken,//axios自带的拦截token
  cancelAlwaysAxios,//终止添加cancelAlwaysToken的请求(包括后续所有请求，即对该请求的永久拦截)
  cancelAlwaysToken,//用于添加在请求上配合cancelAlwaysAxios去做永久拦截
} ;
export default axios;
~~~~
##### 2.axios拦截定义
~~~~jsx
/**取消axios请求**/
import { cancelAlwaysAxios } from "./axios";

const cancels = {
  cancelInputSearchValue: () => {},//单次拦截(需要自己在定义接口是定义这个函数)
  cancelAlwaysAxios,//永久拦截
};

export default cancels;
~~~~
##### 3.定义每一次的axios请求（永久拦截）
~~~~jsx
import axios, { CancelToken, instance, cancelAlwaysToken, } from "../axios";
import cancels from "../cancel";//axios永久拦截定义
import util from "../../assets/js/util";

//搜索框的搜索(永久拦截)
const getSearchValue = (body) => {
  return axios.get(
    `/index.php/ajax/suggest${util.objToQueryString({ ...body })}`,
    cancelAlwaysToken,//永久拦截
  );
};
~~~~
##### 4.定义每一次的axios请求（单次拦截）
~~~~jsx
import axios, { CancelToken, instance, cancelAlwaysToken, } from "../axios";
import cancels from "../cancel";//axios永久拦截定义
import util from "../../assets/js/util";

//搜索框搜索返回的结果(阻止了单次请求)
const getInputSearchValue = ({ search_value, page }) => {
  return instance.post(
    "/query/home_search_query",
    `search_value=${search_value}&page=${page}`,
    {
      cancelToken: new CancelToken(cancel => {
        cancels.cancelInputSearchValue = cancel;//cancels.cancelInputSearchValue定义在拦截定义的单次拦截
      })
    },
  );
};
~~~~
##### 5.axios的集合
~~~~jsx
import { getSearchValue, getInputSearchValue } from "./search/index";

const servers = {
  getSearchValue,
  getInputSearchValue,
};

export default servers;
~~~~
##### 6.使用请求
~~~~jsx
import servers from "../../servers";

servers.getInputSearchValue({
  page,
  search_value: encodeURI(searchValue)
}).then(() => {}).catch(() => {})
~~~~

##### 7.使用拦截
~~~~jsx
import cancels from "../../servers/cancel";

componentWillUnmount () {
  cancels.cancelInputSearchValue("单次拦截");//单次拦截
  cancels.cancelAlwaysAxios("永久拦截");//永久拦截
}
~~~~