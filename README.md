# - 前端笔记

### 求出两个数组的交集和差集 
主要用法：（ES7 Array.prototype.includes ）

    let intersection = a.filter(v => b.includes(v))
    let difference = a.concat(b).filter(v => !a.includes(v) || !b.includes(v))
    
主要用法2: （ES6 set）

	let a = new Set([1, 2, 3]);
	let b = new Set([4, 3, 2]);

	// 并集
	let union = new Set([...a, ...b]);
	// Set {1, 2, 3, 4}

	// 交集
	let intersect = new Set([...a].filter(x => b.has(x)));
	// set {2, 3}

	// 差集
	let difference = new Set([...a].filter(x => !b.has(x)));
	// Set {1}
    
### 为什么需要virtual DOM ？

   VD使得开发者可以通过声明的方式表达页面的呈现效果，而不用关心DOM操作的相关细节。DOM元素的增删改完全可以交给框架来高效的完成。更新页面的时候，借助VD，DOM 元素的改变可以在内存中进行比较，再结合框架的事务机制将多次比较的结果合并后一次性更新到页面，从而有效地减少页面渲染的次数，提高渲染效率。
    
### React 源码理解
   react组件 => 一个object
生成react组件 是由一个createElement(type, props, children) 函数创建的

### es6     <a href="http://es6.ruanyifeng.com/#docs/set-map" target="_blank">详情请点击</a>
## set用法
   定义：一个不重复的集合
	
   去重（⚠️ NaN在set内部是相等的 {}在set内部是不相等的）
   
   set.add(v) 相当于 arr.push() (返回 Set 结构本身。)
   
   set.delete(v) 删
	
   set.has(v) 集合中某元素是否存在
	
   set.clear() 清除
	
   set.size 相当于 arr.length

## weakSet
	定义: 一个不重复集合 但是是浅引用 
￼￼￼￼
### ['1', '2', '3'].map(parseInt) 问题思考
	['1', '2', '3'].map(parseInt) 相当于 ['1', '2', '3'].map((item, index) => return parseInt(item, index))
	arr.map()有三个参数 参数一: item 参数二: 索引 参数三: arr本身
	parseInt()有两个参数 参数一: 要转换的数字或者字符串 参数二: 基数
 <a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map" target="_blank">map用法</a>
  <a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt" target="_blank">parseInt用法</a>

### 防抖和节流
	
  防抖是指一段时间内 事件只能被触发一次 当事件一直在被反复执行时是不触发的 只有在事件执行完毕之后才会被触发
  ```
  let timeout = false
  timeout = setTimeout(() => {
    timeout = null
    func()
  }, time)
  ```
  节流是指在规定的时间内 事件只执行一次
  ```
  let canrun = true
  if (!canrun) return 
  
  canrun = false
  setTimeout(() => {
    func()
    canrun = true
  }, wait)
  ```
### 事件循环机制
宏任务（macro task）和微任务（micro task）的区别

宏任务是指 在执行完任务之后 再执行下一个任务 通常是执行完任务之后 页面进行渲染 然后再执行下一个任务 所以执行流程如下：
	macro task => render => macro task => render => …
宏任务有哪些呢
	如 setTimeout, setInterval, I/o, postMessage, setImmediate等

微任务是指 执行当前任务之后立即执行下一个任务，也就是说，在当前task任务后，下一个task之前，在渲染之前。
因为无需渲染 所以执行速度比宏任务要快

microtask主要包含：Promise.then、async  await 、MutaionObserver、process.nextTick(Node.js 环境)

## node和浏览器事件循环差别
在node11版本之前 先执行所有的宏任务 再执行微任务，
在node11之后 跟浏览器执行机制一致

例：
```
function test () {
   console.log('start')
    setTimeout(() => {
        console.log('children2')
        Promise.resolve().then(() => {console.log('children2-1')})
    }, 0)
    setTimeout(() => {
        console.log('children3')
        Promise.resolve().then(() => {console.log('children3-1')})
    }, 0)
    Promise.resolve().then(() => {console.log('children1')})
    console.log('end') 
}

test()

// 以上代码在node11以下版本的执行结果(先执行所有的宏任务，再执行微任务)
// start
// end
// children1
// children2
// children3
// children2-1
// children3-1

// 以上代码在node11及浏览器的执行结果(顺序执行宏任务和微任务)
// start
// end
// children1
// children2
// children2-1
// children3
// children3-1
```
