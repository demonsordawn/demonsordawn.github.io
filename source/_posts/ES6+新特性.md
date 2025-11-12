---
title: ES6+新特性
tags: [ES6+]
---
### 1. let/const
  - 特性:块级作用域,取代var的函数作用域和变量提升问题,const用于声明常量
  - 应用:在项目中，我使用const声明不会重新赋值的变量，let用于块级作用域内的变量，避免了var变量提升和全局污染的问题。
  - 代码:
```javascript
// 组件状态管理
const [user, setUser] = useState(null);
let loading = false;

// 循环中的块级作用域
for (let i = 0; i < items.length; i++) {
  // 每个 i 都有独立的块级作用域
  setTimeout(() => console.log(i), 1000);
}
```
### 2. 箭头函数
  - 特性:(params)=>{....}简洁语法;没有自己的this,继承自父级作用域的this;不绑定arguments对象;不支持new操作符;不支持yield关键字
  - 应用:在想要保持this的指向上下文的场景中,比如在react类组件中定义回调函数,或者在数组方法(如map,filter)中使用
  - 代码:
```javascript
// React 组件方法
const handleClick = () => {
  setCount(prev => prev + 1);
};

// 数组方法
const activeUsers = users.filter(user => user.isActive);
const userNames = users.map(user => user.name);  
```
### 3. 模板字符串
 - 特性:使用反引号(`)和${}插入变量,支持多行字符串
 - 应用: 拼接字符串,特别是在组件动态HTML片段或者生成复杂字符串时,使代码更清晰
 - 代码: 
```javascript
// 动态 CSS 类名
const buttonClass = `btn ${isPrimary ? 'btn-primary' : 'btn-secondary'} ${size}`;

// 生成动态 URL
const apiUrl = `/api/users/${userId}/posts?page=${currentPage}&limit=${pageSize}`;

// 多行文本
const emailTemplate = `
  尊敬的 ${userName}：
  
  您的订单 ${orderId} 已发货。
  预计送达时间：${deliveryDate}
`;
```
### 4. 解构赋值
 - 特性: 从数组或对象中提取值,并赋值给变量
 - 应用: 从函数返回对象中快速获取属性,函数参数的定义,以及API返回的数据中提取所需的字段
 - 代码:
 ```javascript
// React props 解构
const UserCard = ({ name, age, email, onEdit }) => {
  return <div>{name} - {age}</div>;
};

// API 响应解构
const { data: userList, pagination } = await api.getUsers();
const { current, pageSize, total } = pagination;

// 函数参数解构
const updateUser = ({ id, name, role }) => {
  // 直接使用参数
};
```

### 5. 默认参数
 - 特性: 函数参数可以设置默认值
 - 应用: 在函数定义时,为参数提供默认值,避免函数内部进行undefined判断和默认值赋值
 - 代码:
 ```javascript
const add =(a=1,b=2)=>a+b;
 ```

 ### 6.剩余参数和展开运算符
 - 特性: 剩余参数(..)将多个参数合并为数组,展开运算符将数组或对象展开
 - 应用:剩余参数用于函数参数处理,代替arguments,展开运算符用于数组拼接,对象合并,以及React中传递props\
 - 代码:
 ```javascript
 const sum = (...nums)=>{
  return nums.reduce((acc,cur)=>acc+cur,0);
 }
 const arr1 = [1,2,3];
 const arr2 = [4,5,6];
 const arr3 = [...arr1,...arr2]; // [1,2,3,4,5,6]
 ```

 ### 7.Class类
 - 特性: 更接近传统面向对象语言的类写法,包括继承,静态方法等
 - 应用: 在React中定义类组件,以及在其他面向对象编程的场景使用

 ### 8.模块化
 - 特性: 使用import和export进行模板的导入和导出
 - 应用: 早项目中拆分代码为多个模块,按需导入,提高代码可维护性

 ### 9.Promise
 - 特性:异步编程的解决方案,避免回调地狱
 - 应用:处理异步操作,如API请求,使用then和catch处理成功和失败情况

 ### 10.async/await
 - 特性: 基于Promise的异步编程语法糖,使异步代码看起来像同步代码
 - 应用:在异步函数中,使用await等待Promise结果,使代码更易读和调试
 - 代码:
 ```javascript
 async function fetchData(){
  try{
    await fetch('https://jsonplaceholder.typicode.com/todos/1');
  } ctach(error){
    console.log(error);
  }
 }
 ```

### 11.Symbol
 - 特性:唯一的,不可变的数据类型,常用于对象属性的键
 - 应用:定义对象的私有属性,或者放在属性名冲突
 - 代码:
 
 ### 12.Set和Map
 - 特性:Set是值不重复的集合,Map是键值对集合,键可以是任意类型
 - 应用:Set用数组去重,Map用于需要非字符串键的场景
 - 代码:
 ```javascript
 // 权限管理
const userPermissions = new Set(['read', 'write']);
const hasPermission = userPermissions.has(permission);

// 数据缓存
const cache = new Map();
const getCachedData = (key) => {
  if (cache.has(key)) {
    return cache.get(key);
  }
  const data = fetchData(key);
  cache.set(key, data);
  return data;
};

// 去重
const uniqueIds = [...new Set(duplicateIds)];
 ```

 ### 14.迭代器和生成器
 - 特性:迭代器是一种接口,生成器是一种返回迭代器的函数
 - 应用: 自定义数据结构的遍历,或者在需要惰性求值的场景中使用生成器

### 15.Procy和Reflect
- 特性: Procxy用于修改某些操作的默认行为,Reflect是操作对象的方法的集合
- 应用: 实现数据绑定和观察者模式,例如在vue3中用于响应式系统

### 16.可选链操作符(?)
- 特性: 在访问深层嵌套的属性时,如果中间属性不存在,则返回undefined,而不是报错
- 应用: 安全地访问对象属性,避免undefined或null而导致的错误
- 代码:
```javascript
// 安全访问嵌套属性
const userName = user?.profile?.personalInfo?.name ?? '匿名用户';
const firstPost = user?.posts?.[0]?.title;

// 函数调用保护
const result = apiService?.getData?.() ?? defaultValue;

// 配置处理
const timeout = config?.timeout ?? 5000;
const headers = config?.headers ?? {};
```

### 17.空值合并运算符(??)
- 特性:当左侧操作数为null后undefined时,返回右侧操作数,否则返回左侧操作数
- 应用: 提供默认值,与||不同,不会因为左侧操作数为0或false而返回右侧操作数
-代码:
```javascript
const name = user?.name ?? '匿名用户';
const age = user?.age ?? 0;
```

### 总结:
 - 代码简洁性:箭头函数,解构,模板字符串
 - 可维护性:模块化,类,const/let
 - 可靠性: Promise,async/await
 - 开发效率: 可选链,空值合并的安全访问
 - 性能优化:Map/Set的数据结构选择