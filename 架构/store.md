### redux、mobx、useReducer
#### 一.redux（thunk）
##### 1.创建数据源
~~~~jsx
const movieNames = (state = {
  page: 1,
  top: 0,
  searchValue: "",
  readyMovieName: [],
}, action) => {
  switch (action.type) {
    case "MOVIE":
      return { ...state, ...action.payload };
    default:
      return state;
  }
};
export default movieNames;
~~~~
##### 2.将数据源打包
~~~~jsx
import { createStore, combineReducers, applyMiddleware } from "redux";
import movieNames from "./readyMovies/readyMovies";
import thunk from "redux-thunk";//异步存储axios的中间键
//数据仓库
const store = createStore(combineReducers({
  movieNames,
})), applyMiddleware(thunk);
export default store;
~~~~
##### 3.将打包好的数据源放入仓库
~~~~jsx
import React from "react";
import Routes from "./components/Routes";
import routers from "./routers/index";
import { Provider } from "react-redux";//数据仓库
import store from "./stores/index";//数据源包

const App = () =>
  <div className="theme">
    <Provider store={store}>
      <Routes routers={routers}/>
    </Provider>
  </div>
;
export default App;
~~~~
##### 4.更新数据
~~~~jsx
import { connect } from "react-redux";

//离开页面保存一些数据
saveDate = () => {
    const { searchResult, page, searchValue } = JSON.parse(JSON.stringify(this.state));
    this.props.dispatch(diapatch => {
        dispatch({
            type: "MOVIE",
            payload: {
                page,
                searchValue,
                top: util.getScrollTop(),
                readyMovieName: [...searchResult],
            }
        })
    });
};

//储存axios数据
getValue = () => {
    this.props.dispatch(dispatch => {
        getValue().then(res => {
            dispatch({
                type: "DATA",
                payload: {
                    data: res.data
                }
            })
        })
    })
}

export default connect(state => ({ state }))(Home);
~~~~

##### 5.使用数据
~~~~jsx
import { connect } from "react-redux";

//初始化页面
initHome = () => {
    const { page, searchValue, readyMovieName, top } = this.props.state.movieNames;//读数据
    this.setState({
        page, searchValue,
        displayName: searchValue,
        searchResult: readyMovieName,
    }）
};

export default connect(state => ({ state }))(Home);
~~~~
#### 一.redux（saga）

#### 二.useReducer
~~~~
React本身不提供状态管理功能，通常需要使用外部库，这方面最常用的库时Redux
Redux的核心概念是，组件发出action与状态管理收到action以后，使用Reducer函数算出新状态，Reducer函数的形式是（state，action）=> newState
~~~~
##### 1.创建数据源
~~~~jsx
const defaultState = {
    count: 0
};
const countRenducer = ( state = defaultState, action ) => {
    switch(action.type){
        case "dec":
            return { ...state, ...action.payload };
        default:
            return state;
    }
};
export { defaultState }
export default countRenducer;
~~~~
##### 2.创建仓库
~~~~jsx
import React from "react";
const ReactContext = React.createContext();
~~~~

##### 3.打包数据放入仓库
~~~~jsx
import React, { useReducer } from "react";
import countRenducer, { defaultState } from "./countRenducer";
import { ReactContext } from "./ReactContext";

const Provider = ReactContext.Provider;
const App = () => {
    const [state, dispatch] = useReducer(countRenducer, defaultState);
    return(
        <Provider value={{state, dispatch}}>
            <Home/>
        </Provider>
    )
}
~~~~
##### 4.更新和使用数据
~~~~jsx
import React, { useContext } from "react";
import { ReactContext } from "./ReactContext";
const Home = () => {
    const context = useContext(ReactContext);
    const updata = () => {//更新数据
        context.dispatch({
            type: "dec",
            payload: {
                count: ++context.state.count
            }
        })
    }
    return(
        <div>
           <p>{context.state.count}</p>
           <button onClick={updata}>增加</button>
        </div>
    )
}
~~~~
#### 三.mobx