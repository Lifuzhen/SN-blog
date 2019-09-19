转载自[ERIC](https://segmentfault.com/a/1190000019670168)

this.setState( )方法是React.js中最常见的一种方法，利用它可以控制各种状态变化，达到页面各种交互效果，但是，我们在React开发中偶尔会发现，明明已经通过this.setState( )方法处理过某个state的值，但是在后续的方法里，log打印出来仍然是之前的值，或者，第一次获取到原来的值，第二次才能获取到设置之后的新值，让人误以为是因为电脑或浏览器性能问题造成的"延迟"问题。

# 执行过程
---

为了理解这个问题，我们首先来看一下setState这个过程中发生了什么：

1、将setState传入的partialState参数存储在当前组件实例的state暂存队列中。
2、判断当前React是否处于批量更新状态，如果是，将当前组件加入待更新的组件队列中。
3、如果未处于批量更新状态，将批量更新状态标识设置为true，用事务再次调用前一步方法，保证当前组件加入到了待更新组件队列中。
4、调用事务的waper方法，遍历待更新组件队列依次执行更新。
5、执行生命周期componentWillReceiveProps。
6、将组件的state暂存队列中的state进行合并，获得最终要更新的state对象，并将队列置为空。
7、执行生命周期componentShouldUpdate，根据返回值判断是否要继续更新。
8、执行生命周期componentWillUpdate。
9、执行真正的更新，render重新渲染。
10、执行生命周期componentDidUpdate。

# 官方解释
---

首先思考为什么会出现这种情况，在facebook给出的官方文档中我们可以看到这么一段话：

```
setState(updater[, callback])
```
_Think of setState( ) as a request rather than an immediate command to update the component. For better perceived performance, React may delay it, and then update several components in a single pass. React does not guarantee that the state changes are applied immediately._

_setState( ) does not always immediately update the component. It may batch or defer the update until later. This makes reading this.state right after calling setState( ) a potential pitfall. Instead, use componentDidUpdate or a setState callback (setState(updater, callback)), either of which are guaranteed to fire after the update has been applied. If you need to set the state based on the previous state, read about the updater argument below._

总结一下，就是以下几点：

- setState( ) 更类似于是一种请求而不是立即更新组件的命令
- 为了更好的性能，React会延迟调用它，不会保证state的变更会立即生效，而是会批量推迟更新
- 官方承认会存在隐患
- 建议在componentDidUpdate中执行或利用回调函数（setState(updater, callback)）

举个简单例子：

```
constructor(props) {
  super(props);
  this.state = {
    num: 1
  };
}

componentDidMount = () => {
  this.setState({ num: this.state.num + 1 });
  console.log(this.state.num);   // 1
}
```
这是因为this.setState( )本身是异步的，程序异步运行，可以提高程序运行的效率，不必等一个程序跑完，再跑下一个程序，特别当这两个程序是无关的时候。React会去合并所有的state变化，在前一个方法未执行完时，就先开始运行后一个方法。但是实际操作中，为了能实时获取后一个状态值，需要一些解决的办法。

# 利用全局属性
---

尝试一下换个写法，利用全局属性的办法而不是用state的方式去获取数据：

```
constructor(props) {
  super(props);
  this.num = 1;
}

componentDidMount = () => {
  this.num = this.num + 1;
  console.log(this.num);   // 2
}
```
这其实是一种取巧的方式，写法方便，原理简单，但是并不十分推荐，因为它并不符合React中关于有状态组件的设计理念，存在有可能无法触发刷新的风险(虽然在我的开发过程从没有发生这样的事)，所以还是希望大家优先使用下面的方法。

# 利用回调函数
---

回调函数众所周知，就是某个函数执行完毕后执行的函数，利用它可以确保在this.setState( )整个函数执行完成之后去获取this.state.xxx的值：
```
constructor(props) {
  super(props);
  this.state = {
    num: 1
  };
}

componentDidMount = () => {
  this.setState({ num: this.state.num + 1 }, () => {
    console.log(this.state.num);   // 2
  });
  console.log(this.state.num);   // 1
}
```
控制台按顺序先后打印出两个结果：
```
1
2
```
# 利用setTimeout( )
---

首先简单回顾一下，利用setTimeout( )模拟一下前文提到的Javascript中的异步：
```
foo = () => {
  console.log('11111111');
  setTimeout(function(){
    console.log('22222222');
  },1000);
};
bar = () => {
  console.log('33333333');  
}
foo();
bar();
// 11111111
// 33333333
// 22222222
```
所以，在上述代码块中，在前一方法（foo）执行时，后一方法（bar）也可以执行。符合异步的基本概念，程序并不按顺序执行。在foo函数中执行到setTimeout的时候，函数会跳出，并先执行bar( )方法，这样就模拟了一个异步的效果。这里顺便再提一下前面说的，setState方法通过一个队列机制实现state更新，当执行setState的时候，会将需要更新的state合并之后放入状态队列，而不会立即更新，通过下面的例子可见。
```
constructor(props) {
  super(props);
  this.state = {
    num: 1,
  };
}
componentWillMount = () => {
  this.setState({
    num: this.state.num + 1,
  });
  console.log(this.state.num);
  this.setState({
    num: this.state.num + 1,
  });
  console.log(this.state.num);
}

render() {
  console.log(this.state.num);
  return (<div />);
}
```
代码输出结果为： ==1，1，2==

利用setTimeout方法可以解决state的异步问题，因为setState只在合成事件和钩子函数中是“异步”的，在原生事件和setTimeout 中都是同步的：
```
componentWillMount = () => {
  setTimeout(() => {
    this.setState({
      num: this.state.num + 1,
    });
    console.log(this.state.num);  // 1
    this.setState({
      num: this.state.num + 1,
    });
    console.log(this.state.num);  // 2
  }, 0);
} 
```
# 利用componentDidUpdate( )
---

根据前面文档所说，在componentDidUpdate( )方法中去获取新的state值，根据React的生命周期，此时this.state已经更新。
```
constructor(props) {
    super(props);
    this.state = {
      num: 1
    };
}

componentWillMount = () => {
    this.setState({ num: this.state.num + 1 });
}

componentDidUpdate = () => {
    console.log(this.state.num);   // 2
}
```
# 警告
---

⚠️注意，很多新人在遇到这种问题时无所适从，可能会用一些投机取巧的方式，上面的全局对象是一种方式，还有一种就是绕过setState直接赋值：
```
this.state.num = 2   // 2
```
理论上讲，这种方法当然也能达到赋值目的，但将state设计成更新延缓到最后批量合并再去渲染，对于应用的性能优化是有极大好处的，如果每次的状态改变都去重新渲染真实dom，那么它将带来巨大的性能消耗，所以不建议上面写法。

⚠️如果在shouldComponentUpdate或者componentWillUpdate方法中调用setState，此时this._pending-StateQueue != null，就会造成循环调用，使得浏览器内存占满后崩溃。