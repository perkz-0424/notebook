### Hooks
~~~~js
useState(initialState)
useReducer(reducer, initialArg, init)
useRef(initialValue)
useEffect(create, deps)
useLayoutEffect(create, deps)
useCallback(callback, deps)
useMemo(create, deps)
useImperativeHandle(ref, create, deps)
useDebugValue(value, formatterFn)
useContext(Context, unstable_observedBits)
memo(type, compare)
~~~~
#### useState
~~~~
相当于constructor
const [lxy, setLxy] = useState([]);
~~~~

#### useEffect
~~~~
相当于componentDidMount、componentDidUpdate、componentWillUnmount
~~~~
#### useLayoutEffect
~~~~
~~~~
#### useMemo
~~~~
相当于shouldComponentUpdate，在第一次渲染执行
useMemo(() => {
  fetch("http://192.168.31.91:3001/app/get_some_value").then(res => {
    res.json().then(data => {
        setLxy(data);
      }
    );
  });
}, []);
第二个参数为一个空数组表示页面加载时渲染一遍，第二个参数空数组里的值监听，里面的值发生变化则调用一次useMemo
~~~~
#### useCallback
~~~~
用于得到一个固定引用值的函数，通常用它进行性能优化，useCallback跟useMemo比较类似，但它返回的是缓存的函数
~~~~
#### useReducer
~~~~
跨组件传值（不限于父子组件），共享通讯
~~~~
#### useRef
~~~~
~~~~
#### useImperativeHandle
~~~~
~~~~
#### useDebugValue
~~~~
~~~~
#### useContext
~~~~
~~~~
#### memo
~~~~
~~~~
#### other
~~~~
~~~~