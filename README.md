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
    
### setting sync id    
    Key “4dbfecc12ff36361679cf1f44283fb8cc038ce96”
    Token: 90e4f9ae9e81bc2d93a6e18ca0ec1a2389121f49
    ID “d1c846a11b9b435bc34808ebb4473327”
    
### 为什么需要virtual DOM ？
    VD使得开发者可以通过声明的方式表达页面的呈现效果，而不用关心DOM操作的相关细节。DOM元素的增删改完全可以交给框架来高效的完成。更新页面的时候，借助VD，DOM 元素的改变可以在内存中进行比较，再结合框架的事务机制将多次比较的结果合并后一次性更新到页面，从而有效地减少页面渲染的次数，提高渲染效率。
    
### React 源码理解
    react组件 => 一个object
	生成react组件 是由一个createElement(type, props, children) 函数创建的

### es6 set用法
    去重（⚠️ NaN在set内部是相等的 {}在set内部是不相等的）
	set.add() 相当于 arr.push() (返回 Set 结构本身。)
	set.size 相当于 arr.length
   <a href="http://es6.ruanyifeng.com/#docs/set-map" target="_blank">详情请点击</a>
    ￼￼￼￼
￼￼
