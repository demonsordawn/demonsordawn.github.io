---
title: '前端知识'
date: 2025-10-28
---
# 闭包是什么?在实际项目中有哪些应用场景?

## 闭包就是让一个内部函数可以访问外部函数的作用域,
## 任何闭包的使用场景都离不开这两点:
#### 1.创建私有变量
#### 2.延长变量的生命周期
## 柯里化函数
### 柯里化的目的在于避免频繁调用具有相同参数函数的同时,又能轻松的重用

```javascript
// 假设我们有一个求长方形面积的函数
function getArea(width, height) {
    return width * height
}
// 如果我们碰到的长方形的宽老是10
const area1 = getArea(10, 20)
const area2 = getArea(10, 30)
const area3 = getArea(10, 40)

// 我们可以使用闭包柯里化这个计算面积的函数
function getArea(width) {
    return height => {
        return width * height
    }
}

const getTenWidthArea = getArea(10)
// 之后碰到宽度为10的长方形就可以这样计算面积
const area1 = getTenWidthArea(20)

// 而且如果遇到宽度偶尔变化也可以轻松复用
const getTwentyWidthArea = getArea(20)

