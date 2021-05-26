### 路由
#### 一.react-router-dom
~~~~
本身是基于react-router，加入了在浏览器运行环境的一些功能
HashRouter：有#
BrowserRouter：没有#
Route：设置路由与组件关联
Switch：只要匹配到一个地址就不会在往下匹配
Link：跳转页面
exact：完全匹配路由
Redirect：路由重定向
~~~~
##### 1.创建Routes
~~~~jsx
import React, { Suspense } from "react";
import { BrowserRouter, Route, Redirect, Switch } from "react-router-dom";

const Routes = ({ routers, fallback }) => {
  const createAllRoutes = [];
  (function createRoute (routers) {
    /**这个可以做权限的判断，如token或者是分级用户权限**/
    const _routers = { ...routers }
    if(_routers.level === "0" && localStorage.getItem("user_level") !== "full_member"){//模块等级为会员级，且不是会员跳转至开通会员页面开通会员
      Object.assign(_routers, {
        redirect: "/membership",
      })
    }
    if(!getCookieToken()){//没有登录先登录
      Object.assign(_routers, {
        redirect: "/login",
      })
    }
    createAllRoutes.push({ ..._routers });
    _routers.children && _routers.children.forEach(item => {
      createRoute(item);
    });
  })(routers);
  return (
    <BrowserRouter>
      <Suspense fallback={fallback ? fallback : <React.Fragment/>}>
        <Switch>
          {createAllRoutes.map(item => {
            return item.redirect ?
              <Route path={item.path} key={item.name} exact={item.exact ? item.exact : true}><Redirect to={item.redirect}/></Route> :
              <Route path={item.path} key={item.name} component={item.component} exact={item.exact ? item.exact : true}/>;
          })}
        </Switch>
      </Suspense>
    </BrowserRouter>
  );
};

export default Routes;
~~~~
##### 2.创建每个模块的router（包含了name、path、component）
~~~~jsx
import { lazy } from "react";

const Home = lazy(() => import("../../modules/home"));
const homeRouter = {
  name: "home",
  path: "/home",
  component: Home,
};
export default homeRouter;
~~~~
##### 3.集合router
~~~~jsx
import movieRouter from "./movie/movieRouter";
import homeRouter from "./home/homeRouter";

const routers = {
  name: "root",
  path: "/",
  redirect: "/home",
  children: [
    homeRouter,
    movieRouter,
  ]
};
export default routers;
~~~~
##### 4.将routers放入Routes里
~~~~jsx
import React from "react";
import Routes from "./components/Routes";
import routers from "./routers/index";

const App = () =>
  <div className="theme">
    <Routes routers={routers}/>
  </div>
;
export default App;
~~~~

#### 二.react-router
##### 1.创建路由
~~~~jsx
const HomePage = lazy(() => import("./components/Home"));
const HomeStatic = lazy(() => import("./components/HomeStatic"));

export default {
  path: "home",
  component: Home,
  route_name: "首页",
  indexRoute: {
    onEnter: (nextState, replace) => replace("/home/index"),
  },
  childRoutes: [
    {
      path: "index",
      component: HomePage,
      route_name: '首页',
    },
    {
      path: "staticHome",
      component: HomeStatic,
      route_name: "静态首页",
    }
  ],
};
~~~~
##### 2.创建集合
~~~~jsx
import App from "./App";
import Home from "./Home";

const NavRoutes = [ Home ];
const Routes = {
  path: "/",
  component: App,
  onEnter: (nextState, replace) => {
    if (!getCookieToken()) { //根据是否存在token
      replace({
        pathname: "/auth/login",//跳转到登录页面
        query: {
          ...nextState.location.query,
          from: nextState.location.pathname,//是从哪个页面跳到登录页面
        },
      });
    }
  },
  childRoutes: NavRoutes,
};
~~~~
##### 3.放入到react-router里
~~~~jsx
import { browserHistory, Router } from "react-router";
import Routes from "./routes";

<Router history={browserHistory} routes={Routes}/>
~~~~