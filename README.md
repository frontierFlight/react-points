## useMemo
一般用在父子组件传值处理性能优化，比如一个数据量比较多的对象传给自组件，需要包一层，否则都是会返回一个新的对象的。
还有就是可以把一些昂贵的计算逻辑放到 useMemo 中，只有当依赖值发生改变的时候才去更新。
在开发中当我们有部分变量改变时会影响到多个地方的更新那我们就可以返回一个对象或者数组，通过解构赋值的方式来实现同时对多个数据的缓存。
使用中 useMemo 的场景远比 useCallback 要广泛的很多，我们可以将 useMemo 的返回值定义为返回一个函数这样就可以变通的实现了 useCallback。


## React.memo
用于包裹组件，对props进行浅比较，如果props没有发生变化就不会重新渲染这个组件（因为是浅比较，所以传同一个函数也会重新渲染）


## useCallback
返回一个函数，只有在传入的依赖项变化才会更新。如父组件传递一个点击事件给自组件，如果没有用useCallback包裹这个事件，那么父组件更新都会引起子组件
的更新。如果没有传入依赖项，由于 JS 的静态作用域的原因，值就只会改变一次，之后就没有变化。但不是所有的方法都要用useCallback包一层，因为组件渲染
的时候，会多了useCallback里面的操作（函数的保存还有依赖项的比较）。一般都是要配合子组件的React.memo一起使用，不然就是反向优化。


## useEffect
用来取代componentDidMount 和 componentDidUpdate 进行一些副作用的操作、数据请求和访问dom


## createContext


## 受控组件和非受控组件
[ahooks 的 useControllableValue](https://ahooks.js.org/hooks/use-controllable-value)

[ahooks 的 useControllableValue源码](https://github.com/alibaba/hooks/blob/master/packages/hooks/src/useControllableValue/index.ts)

[如何实现受控组件和非受控组件双模式](https://zhuanlan.zhihu.com/p/536322574)

受控组件：组件内部的状态由父组件传入实现控制。

非受控组件：组件内部的状态由组件自己维护。在业务性组件中会明确是受控组件或者非受控组件。但是对于组件库来说会有很多组件需要两种模式都支持，比如输入类、切换、展开收起的组件。

组件支持双模式的实现思路是让组件内部维护一个状态，当处于受控模式时，手动同步组件内部状态和父组件的状态。useControllableValue内部实现主要是通过useRef+强制更新（数据存储+setState({})强制刷新）

![受控组件和非受控组件](./public//受控组件和非受控组件.jpg)


## react 的 keep-alive 实现
方案一：Portal将节点存储在内存中（createElement）