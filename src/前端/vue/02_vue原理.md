## Vue原理

## vue 原理

### 组件化(如何理解 MVVM 模型)

- 传统组件，只是静态渲染，还要依赖操作 DOM
- 现在实现了数据驱动视图-MVVM
- model--》viewModel--》DOM
- vue 通过 Object.defineProperty 和发布订阅者模式实现了数据驱动视图，get 中通过 dep 收集依赖，然后在 set 中发布消息给 watcher，watcher 订阅了 dep，收到消息后，更新视图

### 响应式

- vue2 通过 Object.defineProperty 改写数据的 get 与 set 实现对 对象 变化的监听
  - 缺点：深度监听，需要一次性递归到底，计算量大
  - 新增删除属性监听不到，要使用 Vue.set,Vue.delete
  - 无法原生监听数组，需要特殊处理

```JavaScript
Object.defineProperty(data, 'name', {
  get: function () {
    return name;
  },
  set: function (newVal) {
    name = newwVal;
  }
});
```

### 虚拟 dom

- vdom：用 js 模拟 dom 结构，计算出最小变更，操作 dom，数据驱动视图的模式下，有效控制 dom 操作
- vdom 参考 snabdom

### diff 算法

- vdom 的核型
- diff 算法能在日常使用中体现出来(key)
- 原始的 diff 算法时间复杂度为 O(n^3),优化后为 O(n):只比较同一层级，不跨级比较；tag 不同，则直接删掉重建，不再深度比较；tag 和 key，两者相同，则认为相同节点，不再深度比较

#### diff 算法总结：

1. 判断是否 sameVnode（就是看 key 和 tag 是否相同）
2. 是的话，patchVnode，进一步比较；否，直接替换成新的，没有比较的价值
3. patchVnode: 1）只是文本不一样，修改文本 2）旧的有子节点，新的没有子节点，删除子节点 3）新的没有子节点，旧的有子节点，新增子节点 4）新的旧的都有子节点，且子节点不相同，updateChildren
4. updateChildren:
   1. 新旧两组子节点，首尾置指针
   2. 比较，若相同，往另一头移动
      1. newStart oldStart，相同，移动
      2. newStart oldEnd，相同，oldEnd 移动到 newStart 前，移动
      3. newEnd oldEnd，相同，移动
      4. newEnd oldStart，相同，oldStart 移动到 newEnd 后，移动
      5. 都不同，比较 newStart 和 old 数组的 key，匹配，移动到 oldStart 6）都没找到，新建 newStart，放前面
   3. 新旧两列其中之一 start > end ,停止，将另一个剩余的部分添加或移除

### 模板编译

#### with 语法

- 改变{}内自由变量的查找规则，当作 obj 的属性查找，如果找不到对应的属性，则报错

#### 编译模板

- 模板不是 html，有指令，插值，js 表达式，判断，循环
- html 是标签语言，只有 js 才能实现，判断，循环（图灵完备的）
- 因此，模板一定是转换为某种 js 代码，即模板编译
- 模板编译为 render 函数，执行 render 函数返回 vnode
- 基于 vnode 再执行 patch 和 diff
- 使用 webpack vue-loader 会在开发环境下编译模板

### 组建渲染更新的过程

#### 初次渲染

1. 解析模板为 render 函数(或者在开发环境已经完成，vue-loader)
2. 触发响应式，监听 data，属性 getter 和 setter
3. 执行 render 函数，生成 v-node，patch(elem, vnode)

#### 更新过程

1. 修改 data，触发 setter(此前在 getter 中已被监听)
2. 重新执行 render 函数，生成 newVnode
3. patch(vnode, newVnode)

### 异步渲染

- 汇总 data 修改，一次性修改视图
- 减少操作 dom 次数，提高性能

## 前端路由

### hash

1. hash 会触发网页跳转，即浏览器前进后退
2. hash 不会刷新页面，SPA 必须的特点
3. hash 永远不会提交到 server 端

### history

1. 用 url 规范的路由，但跳转时不刷新页面
2. history.pushState window.onpopState