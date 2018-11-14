# - 前端笔记

### 求出两个数组的交集和差集 
主要用法：（ES7 Array.prototype.includes ）

    let intersection = a.filter(v => b.includes(v))
    let difference = a.concat(b).filter(v => !a.includes(v) || !b.includes(v))
    
### setting sync id    
    Key “4dbfecc12ff36361679cf1f44283fb8cc038ce96”
    Token: 90e4f9ae9e81bc2d93a6e18ca0ec1a2389121f49
    ID “d1c846a11b9b435bc34808ebb4473327”
