# Vue生命周期

# 前言

 Vue 的生命周期是一个日常高频接触的东西，但一直停留在使用阶段，没有深入了解，参考官方文档和他人的资料，在此总结记录下。

# 生命周期图示

先上官方文档的图，对生命周期有个大概的了解。

![生命周期图示-vuejs](https://cn.vuejs.org/images/lifecycle.png)

**tips：** 你已经是个成熟的程序员了，要学会自己翻译！（英语太烂，就不误人子弟了—_—!）

# 生命周期钩子

以下这些在[官方文档](https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90)里都有。

### beforeCreate

+ **类型**：`Function`

+ **详细**：

  在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

+ **参考**：[生命周期图示](#生命周期图示)

### created

- **类型**：`Function`

- **详细**：

  在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，`$el` 属性目前不可见。

- **参考**：[生命周期图示](#生命周期图示)

### beforeMount

- **类型**：`Function`

- **详细**：

  在挂载开始之前被调用：相关的 `render` 函数首次被调用。

  **该钩子在服务器端渲染期间不被调用。**



**参考**：[生命周期图示](#生命周期图示)

### mounted

- **类型**：`Function`

- **详细**：

  `el` 被新创建的 `vm.$el` 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 `mounted` 被调用时 `vm.$el` 也在文档内。

  注意 `mounted` **不会**承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 [vm.$nextTick](https://cn.vuejs.org/v2/api/#vm-nextTick) 替换掉 `mounted`：

  ```
  mounted: function () {
    this.$nextTick(function () {
      // Code that will run only after the
      // entire view has been rendered
    })
  }
  ```

  **该钩子在服务器端渲染期间不被调用。**

- **参考**：[生命周期图示](#生命周期图示)

### beforeUpdate

- **类型**：`Function`

- **详细**：

  数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。

  **该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行。**

- **参考**：[生命周期图示](#生命周期图示)

### updated

- **类型**：`Function`

- **详细**：

  由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

  当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用[计算属性](https://cn.vuejs.org/v2/api/#computed)或 [watcher](https://cn.vuejs.org/v2/api/#watch) 取而代之。

  注意 `updated` **不会**承诺所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以用 [vm.$nextTick](https://cn.vuejs.org/v2/api/#vm-nextTick) 替换掉 `updated`：

  ```
  updated: function () {
    this.$nextTick(function () {
      // Code that will run only after the
      // entire view has been re-rendered
    })
  }
  ```

  **该钩子在服务器端渲染期间不被调用。**

- **参考**：[生命周期图示](#生命周期图示)

### beforeDestroy

- **类型**：`Function`

- **详细**：

  实例销毁之前调用。在这一步，实例仍然完全可用。

  **该钩子在服务器端渲染期间不被调用。**

- **参考**：[生命周期图示](#生命周期图示)

### destroyed

- **类型**：`Function`

- **详细**：

  Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

  **该钩子在服务器端渲染期间不被调用。**

- **参考**：[生命周期图示](#生命周期图示)
