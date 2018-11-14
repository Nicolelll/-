# - 前端笔记

### 求出两个数组的交集和差集 
主要用法：（ES7 Array.prototype.includes ）

    let intersection = a.filter(v => b.includes(v))
    let difference = a.concat(b).filter(v => !a.includes(v) || !b.includes(v))
    
### setting sync id
    4dbfecc12ff36361679cf1f44283fb8cc038ce96
