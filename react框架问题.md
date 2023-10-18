### 请简单描述一下react hooks 的api以及相应的功能
+ 避免疯狂式嵌套，可读性提高。
+ 函数式组件，比class语法更加已读和理解。
+ class组件钩子函数太多太复杂。
+ 解决HOC和render props的缺点。
+ UI和逻辑更方便解耦。
+ 解决组件之间的副作用
+ useState 函数组建中，可以用来管理组件的状态
+ useReducer  用于集中管理状态，可做全局或局部的状态管理  接收一个reducer函数(入参：更新前的state初始值，action )和一个初始值(initialState)，返回一个state和dispatch方法
+ useEffect 接收一个包含命令式，且可能包含副作用的函数
	支持在组件内完成挂载、状态更细和卸载的能力。
	第一个参数是一个callback，可以用来做一些副作用，比如异步请求，修改外部参数等行为
	useEffect的第二个参数source是一个触发条件，类型为数组，如果数组中观测的值发生变化才会触发useEffect的callback回调。
+ useLayoutEffect 与useEffect函数类似，但会在DOM修改后同步触发执行，并且比useEffect先执行，会阻塞浏览器的函数渲染。 
	useEffect执行顺序：组件更新挂载完成，DOM绘制完成，执行useEffect回调。 
	useLayoutEffect执行顺序：组件更新挂载完成，执行useLayoutEffect回调，DOM绘制完成
+ useMemo 提升性能，给子组件传递状态时绑定这个函数，可以避免组件更新时，子组件进行不必要的更新
+ useCallback 
+ useContext 组件之间的通信，组件深入传值时，props不如useContext方便。  creatContext.privoder useContext  配合```<MyContext.Provider data={{val:"test"}}>```进行传递，在子组件中使用。
+ 在子组件中import {MyContext} from "./MyContext"，在方法里调用 const obj = useContext(MyContext)；
### 请说出useState和useReducer的区别
从官方文档来看，useState 相当于类组件的 setState，存在的目的都是拿来做组件内的状态管理。

只不过一个类组件只有一个 setState，但是一个函数组件却可以有很多 useState，这让我们可以把独立的状态分开管理，逻辑上更清晰了，更方便维护了，这是 hooks 的天然优势。

虽说 useReducer 可以拿来做组件内状态管理，但是 useReducer 对于单组件来说太重了，绝大多数情况下是用用不到的。

useReducer 更适合拿来做简单场景下的数据流。useReducer 是阉割版的 redux，只缺了一个状态共享能力，用 hooks 的 useContext 刚刚好。
### 请解释一下diff算法
diff算法就是进行虚拟节点对比，并返回一个patch对象，用来存储两个节点不同的地方，最后用patch记录的消息去局部更新Dom。 简单来说Diff算法就是在虚拟DOM树从上至下进行同层比对，如果上层已经不同了，那么下面的DOM全部重新渲染。 这样的好处是算法简单，减少比对次数，加快算法完成速度
真实DOM和虚拟DOM  真实DOM比较重，上面挂载了很多原生的方法，虚拟DOM清，是一个对象。
DOM的更新的时候 重排和重绘
如果标签的首字母是小写，就会被认定为原生标签，反之就是React组件
实际上，React会将整个DOM保存为虚拟DOM，如果有更新，都会维护两个虚拟DOM，以此来比较之前的状态和当前的状态,并会确定哪些状态被修改，然后将这些变化更新到实际DOM上,一旦真正的DOM发生改变，也会更新UI
所以在虚拟DOM感受到变化的时候，只会更新局部，而非整体。同时，虚拟DOM会减少了非常多的DOM操作 ，所以性能会提升很多

它的优势是在于diff算法和批量处理策略,将所有的DOM操作搜集起来，一次性去改变真实的DOM,但在首次渲染上，虚拟DOM会多了一层计算，消耗一些性能，所以有可能会比html渲染的要慢
React基于虚拟DOM实现了一套自己的事件机制，并且模拟了事件冒泡和捕获的过程，采取事件代理、批量更新等方法，从而磨平了各个浏览器的事件兼容性问题

虚拟DOM转换为真实DOM：大体上可以分为四步： 处理参数、批量处理、生成html和渲染html

Diff算法 
Web UI 中 DOM 节点跨层级的移动操作特别少，可以忽略不计。
拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构。
对于同一层级的一组子节点，它们可以通过唯一 id 进行区分。

+ tree diff: 同级比较,既然DOM 节点跨层级的移动操作少到可以忽略不计，那么React通过updateDepth 对 Virtual DOM 树进行层级控制，也就是同一层，在对比的过程中，如果发现节点不在了，会完全删除不会对其他地方进行比较，这样只需要对树遍历一次就OK了


+ component diff：组件比较，React对于组件的策略有两种方式，一种是相同类型的组件和不同类型的组件
对同种类型组件对比，按照层级比较继续比较虚拟DOM树即可，但有种特殊的情况，当组件A如果变化为组件B的时候，有可能虚拟DOM并没有任何变化，所以用户可以通过shouldComponentUpdate() 来判断是否需要更新，判断是否计算
对于不同组件来说，React会直接判定该组件为dirty component（脏组件），无论结构是否相似，只要判断为脏组件就会直接替换整个组件的所有节点

+ element diff：节点比较，对于同一层级的一子自节点，通过唯一的key进行比较

### react性能优化可以从哪些方面去做
+ 组件按需挂载  懒加载
+ 防抖、节流
+ 减少重新 Render 的次数 使用React.memo来缓存组件
+ 使用useMemo来缓存大量计算
+ css display none 和visibile hidden
+ 使用Fragment来避免添加额外的DOM节点
+ 避免使用匿名函数  匿名函数在每次渲染的时候都会重新渲染
+ 跳过不必要的组件更新
+ 列表项使用 key 属性
+ 利用 useMemo 可以缓存计算结果的特点，如果 useMemo 返回的是组件的虚拟 DOM，则将在 useMemo 依赖不变时，跳过组件的 Render 阶段。该方式与 React.memo 类似，但与 React.memo 相比有以下优势：
更方便。React.memo 需要对组件进行一次包装，生成新的组件。而 useMemo 只需在存在性能瓶颈的地方使用，不用修改组件。
更灵活。useMemo 不用考虑组件的所有 Props，而只需考虑当前场景中用到的值，也可使用 useDeepCompareMemo 对用到的值进行深比较。

### 如何封装一个业务组件
+ 命名规范  命名语义化 
+ 注释规范
+ 不要传输组件是否展示的参数
+ 合理的参数
+ 业务逻辑和代码逻辑分开
+ 可维护、可拓展
+ 低耦合

### 前端工程化
+ 模块化 js模块化  css模块化 资源的模块化 
简单来说，模块化就是将一个大文件拆分成相互依赖的小文件，再进行统一的拼装和加载。
用webpack+babel将所有模块打包成一个文件同步加载，也可以搭乘多个chunk异步加载；
用system+babel主要是分模块异步加载；
用浏览器```<script type="module">```加载。

sass、less、stylus等预处理器实现了css的文件拆分
+ 组件化
从ui拆分下来的每个包含模板（html）+样式（css）+逻辑（js）功能完备的结构单元，我们称之为组件

组件化≠模块化。模块化只是在文件层面上，对代码或资源的拆分；而组件化是在设计层面上，对ui（用户界面）的拆分。除了封装组件本身，还要合理处理组件之间的关系，比如（逻辑）继承、（样式）扩展、（模板）嵌套和包含等，这些关系都可以归为依赖。

+ 规范化
1. 目录结构的制定
1. 编码规范
1. 前后端接口规范
1. 文档规范
1. 组件管理
1. git分支管理
1. commit描述规范
1. 视觉图表规范

+ 自动化
1. 图标合并
1. 持续继承
1. 自动化构建
1. 自动化部署
1. 自动化测试