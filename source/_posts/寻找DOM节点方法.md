---
title: '寻找DOM节点方法'
tags: ['dom']
---

### 1. getElementById()
#### 这是最常用的方法之一，因为id在HTML文档中应该是唯一的。它返回一个元素对象，如果找不到则返回null。
```javascript
var element = document.getElementById('myId');
```
### 2. getElementsByClassName()
#### 该方法接受一个字符串参数,包含一个或多个类名(用空格分隔),返回一个实时更新的HTMLCollection.
#### 注意他返回的是集合,即使只有一个元素
#### HTMLCollection是动态集合,可以随时添加或删除元素,但不能使用索引访问元素
```javascript
var elements = document.getElementsByClassName('myClass');
```
### 3.getElementByTagName()
#### 该方法通过标签名（如'div', 'p'等）来查找元素，返回一个实时更新的HTMLCollection。
```javascript
var elements = document.getElementsByTagName('div');
```

### 4. querySelector()
#### 该方法使用CSS选择器作为参数,返回第一个匹配的元素,如果找不到则返回null
#### 注意:该方法只支持CSS选择器,不支持XPath
```javascript
var element = document.querySelector('.myClass'); // 第一个具有myClass类的元素
var element = document.querySelector('#myId'); // id为myId的元素
var element = document.querySelector('div'); // 第一个div元素
```
### 5. querySelectorAll()
#### 该方法使用CSS选择器作为参数,返回一个实时更新的NodeList,包含所有匹配的元素。
```javascript
var elements = document.querySelectorAll('div.myClass'); // 所有具有myClass类的div元素
```

### 6.getElementByName()
#### 该方法通过name属性查找元素,返回一个NodeList,常用于表单元素,单选按钮,复选框等
```javascript
var elements = document.getElementsByName('gender');
```