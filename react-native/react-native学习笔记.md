#React Native

# 学习资料与工具

[react-native github](https://github.com/facebook/react-native)

[React Native中文网](https://reactnative.cn/)

[react navigation教程](https://reactnavigation.org/)  

[react-native-debugger github](https://github.com/jhen0409/react-native-debugger)

[React-Native学习指南 各种资源的合集](https://github.com/reactnativecn/react-native-guide)  

[react-native-scrollable-tab-view](https://github.com/ptomasroos/react-native-scrollable-tab-view#readme)  

[平安科技移动开发二队技术周报（特别版のReact Native专题）](https://www.jianshu.com/p/96febc4fec45)  

[react-native兴趣交流群开源项目整理](https://www.jianshu.com/p/ced34ce5d7b1)

[awesome-react-native](https://github.com/jondot/awesome-react-native)  

[react-native-awesome](https://github.com/crazycodeboy/react-native-awesome)

[react-native-open-project](https://github.com/MarnoDev/react-native-open-project)


# 新建项目

使用react native命令行工具新建项目

`react-native init 项目名`

运行项目，首先要确保有可用的真机或模拟器

```
cd 项目名
react-native run-android
```

# 笔记

## 尺寸

> React Native 中的尺寸都是无单位的，表示的是与设备像素密度无关的逻辑像素点。

## TextInput

> `TextInput`在安卓上默认有一个底边框，同时会有一些padding。如果要想使其看起来和iOS上尽量一致，则需要设置`padding: 0`，同时设置`underlineColorAndroid="transparent"`来去掉底边框。
>
> 又，在安卓上如果设置`multiline = {true}`，文本默认会垂直居中，可设置`textAlignVertical: 'top'`样式来使其居顶显示。
>
> 又又，在安卓上长按选择文本会导致`windowSoftInputMode`设置变为`adjustResize`，这样可能导致绝对定位的元素被键盘给顶起来。要解决这一问题你需要在AndroidManifest.xml中明确指定合适的`windowSoftInputMode`( <https://developer.android.com/guide/topics/manifest/activity-element.html> )值，或是自己监听事件来处理布局变化。

## react navigation

### 页面跳转

```
<Button
  title="Go to Details... again"
  onPress={() => this.props.navigation.push('Details')}
/>
```

+ `this.props.navigation`：`navigation` prop 传递给每个在 stack navigator 中定义的(**屏幕组件**)。

+ - `navigate（'Details'）`：我们使用用户将要跳转的路由的名称来调用`navigate`方法。

#### 多次导航到同一路由

重复使用`navigate('Details')`并不会多次跳转这个路由，如果是想添加另一个`Details`路由，应该使用`push('Details')`

```javascript
<Button
  title="Go to Details... again"
  onPress={() => this.props.navigation.push('Details')}
/>
```

每次调用`push`都会向导航堆栈中添加新路由。当你调用 ` navigate ` 时, 它首先尝试查找具有该名称的现有路由, 并且只有在堆栈上没有一个新路由时才会推送该路由。

#### 返回

如果当前页面可以执行返回操作，则 stack navigator 会自动提供一个包含返回按钮的标题栏（如果导航堆栈中只有一个页面，则没有任何可返回的内容，因此也不存在返回键）。

有时候你希望能够以编程的方式触发此行为，可以使用` this.props.navigation.goBack() `。

> 在Android上，React Navigation 挂钩到硬件的返回按钮，并在用户按下返回按钮时触发` goBack()`方法，因此它的行为与用户期望的相同。
>
> 另一个常见需求是能够跨越*多个*页面返回 - 例如，如果你处在堆栈深处，上面有多个页面，此时你想要将上面所有的页面都销毁，并返回第一个页面。 在这种情况下，我们知道我们要回到` Home `，所以我们可以使用` navigate('Home') `（而不是` push `！ 尝试一下，看看有什么不同）。 另一个选择是` navigation.popToTop() `，它可以返回到堆栈中的第一个页面。

#### 摘要

* ` this.props.navigation.navigate('RouteName') `将新路由推送到堆栈导航器，如果它尚未在堆栈中，则跳转到该页面。
* 我们可以多次调用` this.props.navigation.push('RouteName') `，并且它会继续推送路由。
* 标题栏会自动显示返回按钮，但你可以通过调用` this.props.navigation.goBack() `以编程方式返回。 在Android上，硬件返回按钮会按预期工作。
* 您可以使用` this.props.navigation.navigate('RouteName') `返回堆栈中的现有页面，你可以使用` this.props.navigation.popToTop() `返回堆栈中的第一个页面。
* ` navigation ` prop适用于所有屏幕组件（组件定义为路由配置中的屏幕，并且被 React Navigation 渲染为路由）。

### 传递参数给路由

传递参数

```
this.props.navigation.navigate('RouteName', { /* params go here */ })
```

接收参数

```
this.props.navigation.getParam(paramName, defaultValue)
```

#### 摘要

- `navigate`接受可选的第二个参数，以便将参数传递给要导航到的路由。 例如：`this.props.navigation.navigate('RouteName', {paramName: 'value'})`。
- 我们可以使用`this.props.navigation.getParam`读取参数
- 作为`getParam`的替代方法，可以使用`this.props.navigation.state.params`。 如果未指定参数，则为`null`。

### 设置标题栏

```javascript
class HomeScreen extends React.Component {
  static navigationOptions = {
    title: 'Home',
  };

  /* render function, etc */
}
```

> `createStackNavigator`默认情况下按照平台惯例设置，所以在iOS上标题居中，在Android上左对齐。

#### 在标题中使用参数

```javascript
class DetailsScreen extends React.Component {
  static navigationOptions = ({ navigation }) => {
    return {
      title: navigation.getParam('otherParam', 'A Nested Details Screen'),
    };
  };

  /* render function, etc */
}
```

传递给`navigationOptions`函数的参数是具有以下属性的对象：

- `navigation` - 页面的[ 导航属性 ](https://reactnavigation.org/docs/zh-Hans/navigation-prop.html)，在页面中的路由为`navigation.state`。
- `screenProps` - 从导航器组件上层传递的 props
- `navigationOptions` - 如果未提供新值，将使用的默认或上一个选项

## 图片

```javascript
// 正确
<Image source={require("./my-icon.png")} />;

// 错误
var icon = this.props.active ? "my-icon-active" : "my-icon-inactive";
<Image source={require("./" + icon + ".png")} />;

// 正确
var icon = this.props.active
  ? require("./my-icon-active.png")
  : require("./my-icon-inactive.png");
<Image source={icon} />;
```

### 网络图片

`你需要手动指定图片的尺寸`

```javascript
// 正确
<Image source={{uri: 'https://facebook.github.io/react/logo-og.png'}}
       style={{width: 400, height: 400}} />

// 错误
<Image source={{uri: 'https://facebook.github.io/react/logo-og.png'}} />
```

### 网络图片的请求参数

```javascript
// 示例
<Image
  source={{
    uri: "https://facebook.github.io/react/logo-og.png",
    method: "POST",
    headers: {
      Pragma: "no-cache"
    },
    body: "Your Body goes here"
  }}
  style={{ width: 400, height: 400 }}
/>
```

## 定时器

**务必在卸载组件前清除定时器！**

在某个组件被卸载（unmount）之后，计时器却仍然在运行。要解决这个问题，只需铭记`在unmount组件时清除（clearTimeout/clearInterval）所有用到的定时器`即可

```javascript
import React, { Component } from "react";

export default class Hello extends Component {
  componentDidMount() {
    this.timer = setTimeout(() => {
      console.log("把一个定时器的引用挂在this上");
    }, 500);
  }
  componentWillUnmount() {
    // 请注意Un"m"ount的m是小写

    // 如果存在this.timer，则使用clearTimeout清空。
    // 如果你使用多个timer，那么用多个变量，或者用个数组来保存引用，然后逐个clear
    this.timer && clearTimeout(this.timer);
  }
}
```

## AsyncStorage

> AsyncStorage是一个简单的、异步的、持久化的Key-Value存储系统，它对于App来说是全局性的。它用来代替LocalStorage。

[AsyncStorage](https://reactnative.cn/docs/asyncstorage/)

## 项目调试技巧

[在React Native中调试项目技巧](https://www.imooc.com/video/14298)
我主要记录window下Android模拟器怎么调试

+ 使用到哪些工具？

  开发者菜单，Chrome开发者工具，真机

+ 怎么打开这些功能工具？

  `ctrl+m`打开开发者菜单，点击`Debug JS Remotely`打开Chrome浏览器，`F12`就打开了Chrome开发者工具（作为一个前端开发就不多介绍怎么使用了）

  > 注意：有时打开Chrome浏览器的URL是：http://10.0.2.2:8081/debugger-ui，可能存在无法访问的问题，将URL修改为：http://localhost:8081/debugger-ui/就能范问了

+ 这些工具主要有哪些特性？

  开发者菜单：

  **reload**: 重新加载，跟按两下`R`键是一样的效果。

  **Debug JS Remotely**:见上文。

  **Enable Live Reload**: 开启动态重载，将js文件的变化实时加载出来。

  **Enable Hot Reloading**:开启热重载，应用程序运行过程中替换、添加或删除模块，而无需重新加载整个页面。

  ...

## console.log语句

在运行打好了离线包的应用时，控制台打印语句可能会极大地拖累JavaScript线程。注意有些第三方调试库也可能包含控制台打印语句，比如redux-logger，所以在发布应用前请务必仔细检查，确保全部移除。  
>  这里有个小技巧可以在发布时屏蔽掉所有的console.*调用。React Native中有一个全局变量__DEV__用于指示当前运行环境是否是开发环境。我们可以据此在正式环境中替换掉系统原先的console实现。

```
if (!__DEV__) {
  global.console = {
    info: () => {},
    log: () => {},
    warn: () => {},
    error: () => {},
  };
}
```


  ​
