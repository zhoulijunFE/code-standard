# Vue编码规范

[1 前言](#1-%E5%89%8D%E8%A8%80)

[2 组件文件](#2-组件文件)

　　[2.1 组件文件命名](#21-组件文件命名)

　　　　[2.1.1 模板中的组件名大小写](#211-模板中的组件名大小写)

　　　　[2.1.2 JS/JSX 中的组件名大小写](#212-JS/JSX%20%E4%B8%AD%E7%9A%84%E7%BB%84%E4%BB%B6%E5%90%8D%E5%A4%A7%E5%B0%8F%E5%86%99) 

　　　　[2.1.3 自闭和组件](#213-自闭和组件)  ```ESLINT```
　　　　

[3 prop](#3-prop)

　　[3.1 prop定义](#31-prop定义)   ```ESLINT```

　　[3.2 prop的大小写](#32-prop的大小写)

　　[3.3 prop对象属性](#33-prop对象属性)  ```CR```

[4 指令规范](#4-指令规范)

　　[4.1 为v-for设置键值](#41-为v-for设置键值)　```ESLINT```

　　[4.2 避免 v-if 和 v-for 用在一起](#42-%E9%81%BF%E5%85%8D%20v-if%20%E5%92%8C%20v-for%20%E7%94%A8%E5%9C%A8%E4%B8%80%E8%B5%B7)   <font color="red">ESLINT</font>

　　[4.3 指令缩写](#43-指令缩写)  ```ESLINT```
　　　　

[5 组件/实例顺序](#5-组件/实例顺序)

　　[5.1 组件/实例选项的顺序](#51-组件/实例选项的顺序) ```ESLINT```

　　[5.2 元素特性的顺序](#52-元素特性的顺序)```ESLINT```

[6 组件样式](#6-组件样式)

　　[6.1 组件样式设置作用域](#61-组件样式设置作用域)  ```CR```
　　

## 1 前言
本文档的目标是使Vue、Vuex代码风格保持一致，容易被理解和被维护。

## 2 组件文件
### 2.1 组件文件命名

#### 2.1.1 模板中的组件名大小写

##### [建议] 统一kebab-case

示例：

```javascript
// good
<my-component></my-component>
```

#### 2.1.2 JS/JSX 中的组件名大小写

##### [强制] 单文件组件、JSX、模板 里使用 PascalCase。 通过 Vue.component 定义推荐 kebab-case
示例：

```javascript
// good
Vue.component('my-component', {
  // ...
})

export default {
  name: 'MyComponent',
  // ...
}

import MyComponent from './my-component.vue'

```
#### 2.1.3 自闭和组件

##### [强制] 在单文件组件、字符串模板和 JSX 中没有内容的组件应该是自闭合的

示例：

```javascript
// good
<my-component/>

```
##### [强制] 多个特性的元素应该分多行撰写，每个特性一行。

示例：

```javascript
<my-component
  foo="a"
  bar="b"
  baz="c"
/>
```

## 3 prop
#### 3.1 prop定义

##### [强制] Prop 定义应该尽量详细。至少需要指定其类型、默认值

示例：

```javascript
// good
props: {
  status: {
    type: String,
    default: ''
  } 
}
```
#### 3.2 prop的大小写
##### [强制] 在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板和 JSX 中应该始终使用 kebab-case。

示例：

```javascript
// good
props: {
  greetingText: String
}
<WelcomeMessage greeting-text="hi"/>
```

#### 3.3 prop对象属性
##### [强制] prop 是object、Array类型初始值函数

示例：

```javascript
// good Array
props: {
  arr: {
    type: Array,
    default: function () {
      return []
    }
  }
}

or es6

props: {
  arr: {
    type: Array,
    default: () => []
  }
}
// good Object
props: {
  obj: {
    type: Object,
    default: function () {
      return {}
    }
  }
}

or es6

props: {
  obj: {
    type: Object,
    default: () => {}
  }
}
```

## 4 指令规范
#### 4.1 为v-for设置键值

##### [强制] 总是用 key 配合 v-for

示例：

```javascript
// good
<ul>
  <li
    v-for="todo in todos"
    :key="todo.id"
  >
    {{ todo.text }}
  </li>
</ul>
```
#### 4.2 避免 v-if 和 v-for 用在一起
##### [强制] 永远不要把 v-if 和 v-for 同时用在同一个元素上。

示例：

```javascript
// good
<ul v-if="shouldShowUsers">
  <li
    v-for="user in users"
    :key="user.id"
  >
    {{ user.name }}
  </li>
</ul>
```

#### 4.3 指令缩写
##### [强制] 指令缩写 (用 : 表示 v-bind: 、用 @ 表示 v-on: 和用 # 表示 v-slot:) 应该要么都用要么都不用

示例：

```javascript
// good
<input
  :value="newTodoText"
  :placeholder="newTodoInstructions"
>

<input
  v-bind:value="newTodoText"
  v-bind:placeholder="newTodoInstructions"
>

<input
  @input="onInput"
  @focus="onFocus"
>

<input
  v-on:input="onInput"
  v-on:focus="onFocus"
>

<template v-slot:header>
  <h1>Here might be a page title</h1> 
</template>
<template v-slot:footer>
  <p>Here's some contact info</p>
</template>

<template #header>
  <h1>Here might be a page title</h1> 
</template>

<template #footer>
  <p>Here's some contact info</p>
</template>
```

## 5 组件/实例顺序
#### 5.1 组件/实例选项的顺序

##### [强制] 组件/实例的选项应该有统一的顺序

示例：

```javascript
副作用 (触发组件外的影响)

el
全局感知 (要求组件以外的知识)

name
parent
组件类型 (更改组件的类型)

functional
模板修改器 (改变模板的编译方式)

delimiters
comments
模板依赖 (模板内使用的资源)

components
directives
filters
组合 (向选项里合并属性)

extends
mixins
接口 (组件的接口)

inheritAttrs
model
props/propsData
本地状态 (本地的响应式属性)

data
computed
事件 (通过响应式事件触发的回调)

watch
生命周期钩子 (按照它们被调用的顺序)
beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
activated
deactivated
beforeDestroy
destroyed
非响应式的属性 (不依赖响应系统的实例属性)

methods
渲染 (组件输出的声明式描述)

template/render
renderError
```
#### 5.2 元素特性的顺序

##### [强制] 组件/实例的选项应该有统一的顺序
示例：

```javascript
定义 (提供组件的选项)

is
列表渲染 (创建多个变化的相同元素)

v-for
条件渲染 (元素是否渲染/显示)

v-if
v-else-if
v-else
v-show
v-cloak
渲染方式 (改变元素的渲染方式)

v-pre
v-once
全局感知 (需要超越组件的知识)

id
唯一的特性 (需要唯一值的特性)

ref
key
slot
双向绑定 (把绑定和事件结合起来)

v-model
其它特性 (所有普通的绑定或未绑定的特性)

事件 (组件事件监听器)

v-on
内容 (覆写元素的内容)

v-html
v-text
```

## 6 组件样式
#### 6.1 组件样式设置作用域

##### [强制] style设置scope特性
解释：https://vue-loader-v14.vuejs.org/zh-cn/features/scoped-css.html

示例：

```javascript
// good
<style scoped>
    .example {
      color: red;
    }
</style>

// 深度作用选择器: 影响子组件，可以使用 >>> 操作符 or  /deep/ 
<style scoped>
 .a >>> .b { 
     /* ... */ 
  }
</style>

or 

<style scoped>
 .a /deep/ .b { 
     /* ... */ 
  }
</style>
```
