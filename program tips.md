1 在js中使用单引号'',不要使用双引号""

2 类名不要使用驼峰式命名,而是使用下划线 _ 或是 -

3 netstat -ano|findstr "4000" 查看某个端口的pid

4 React中,组件的私有方法都用 _ 开头，所有事件监听的方法都用 handle 开头。把事件监听方法传给组件的时候，属性名用 on 开头。

5 react 中  组件的编写顺序
    1 static 开头的类属性，如 defaultProps、propTypes
    2 构造函数，constructor
    3 getter/setter
    4 组件生命周期
    5 _ 开头的私有方法
    6 事件监听方法，handle*
    7 render*开头的方法，有时候 render() 方法里面的内容会分开到不同函数里面进行，这些函数都以 render* 开头
    8 render() 方法
6 redux步骤

    // 定一个 reducer
    function reducer (state, action) {
      /* 初始化 state 和 switch case */
    }

    // 生成 store
    const store = createStore(reducer)

    // 监听数据变化重新渲染页面
    store.subscribe(() => renderApp(store.getState()))

    // 首次渲染页面
    renderApp(store.getState()) 

    // 后面可以随意 dispatch 了，页面自动更新
    store.dispatch(...)
    
7 个人写 reducer 文件的习惯，仅供参考：

    定义 action types
    编写 reducer
    跟这个 reducer 相关的 action creators
