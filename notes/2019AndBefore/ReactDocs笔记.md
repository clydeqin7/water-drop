# ReactDocs笔记

[React 官方文档](https://reactjs.org/docs/hello-world.html)的学习笔记

## MAIN CONCEPTS

### Components and Props

`<Welcome/>` 大写字母起头
> Note: Always start component names with a capital letter.

### State and Lifecycle

`componentDidMount`
> We want to [set up a timer](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/setInterval) whenever the `Clock` is rendered to the DOM for the first time. This is called “mounting” in React.

`componentWillUnmount`

> We also want to [clear that timer](https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers/clearInterval) whenever the DOM produced by the `Clock` is removed. This is called “unmounting” in React.

```
  this.setState({ xx: 123 })
  this.setState((state, props) => {
    counter: state.couter + props.increment
  })
  this.setState(function(state, props) {
    return {
      counter: state.counter + props.increment
    }
  })
```
### Handing Events

React Events  vs  DOM Events
1.  React events are camelCase, DOM is lowercase
2.  React JSX, DOM string
    ```
    <button onClick={clickHandler}>click me</button> // React
    <button onclick="clickHandler()">click me</button> // HTML
    ```  
3.  you cannot return false to prevent default behavior in React. You must call preventDefault explicitly
    ```
      <a href="#" onclick="console.log('The link was clicked.'); return       
     false">
        Click me
      </a> 
    ```
    ```
      function ActionLink() {
          function handleClick(e) {
              e.preventDefault();
              console.log('The link was clicked.');
          }

          return (
            <a href="#" onClick={handleClick}>
              Click me
            </a>
        );
      }
    ```

**this 关键字绑定**
```
onClick={e => this.deleteRow(id, e)}
onClick={this.deleteRow.bind(this, id)}
```
