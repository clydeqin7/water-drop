# 实现一个JQuery的API

## 目标

```
补全???处代码，实现效果
window.jQuery = ???
window.$ = jQuery

var $div = $('div')
$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi
```

## 封装addClass

封装一个函数，实现能给div添加class。[代码链接](http://js.jirengu.com/mepejixiqi/6/edit)

```
//因为是按着课堂教学来的，so
//先封装了一个getSiblings函数
function getSiblings(node){
  var nodes = node.parentNode.children;
  var array = { length:0 };
  for(let i=0; i<nodes.length; i++){
    if(nodes[i] !== node){
      array[i] = nodes[i];
      array.length += 1;
    } 
  }
  
  return array;
}

//封装一个addClass函数
//var classes = ['a', 'b', 'c']; 
var classes = {'a':true, 'b':true, 'c':false}
function addClass(node, classes){
//classes.forEach( (value) => node.classList.add(value)); //forEach
  for(let key in classes){ //for...in
    if(classes[key]){
      node.classList.add(key)
    }
  }
}
```

## 封装setText

封装一个函数，实现能给div设置内容。[代码链接](http://js.jirengu.com/cufojerodo/13/edit)

```
// node为element的id, text为内容
function setText(node, text){
  node.textContent = text;
}

setText(item3, 'hello');
```

## 整合

现在我们封装了getSiblings, addClass, setText三个函数，接下来就是整合到一起。[代码链接](http://js.jirengu.com/nitusevudi/23/edit)

```
function jQuey(nodeOrSelector){
  let nodes = {}
  if(typeof nodeOrSelector === 'string'){
    let temp = document.querySelectorAll(nodeOrSelector)
    for(let i=0; i<temp.length; i++){
      nodes[i] = temp[i]
    }
    nodes.length = temp.length
  }else if(nodeOrSelector instanceof Node){
    nodes = {
      0: nodeOrSelector,
      length: 1
    }
  }
  
  nodes.addClass = function(classes){ 
    if(Array.isArray(classes) === true){
      classes.forEach( (value) => {//forEach局限了只能是Array
        for(let i=0; i<nodes.length; i++){
          nodes[i].classList.add(value)       
        }
      })      
    }else if(typeof classes === 'string'){
        for(let i=0; i<nodes.length; i++){
          nodes[i].classList.add(classes)       
        }
    }
 
  }
  nodes.setText = function(text){
    for(let i=0; i<nodes.length; i++){
      nodes[i].textContent = text
    }
  }
  nodes.getText = function(){
    let texts = []
    for(let i=0; i<nodes.length; i++){
      texts.push(nodes[i].textContent)
    }
    return texts
  }
  
  return nodes  
}
```

其中setText和getText可以合并

```
nodes.text = function(text){
  if(text === undefined){
    let texts = []
      for(let i=0; i<nodes.length; i++){
        texts.push(nodes[i].textContent)
      }
      return texts    
  }else{
     for(let i=0; i<nodes.length; i++){
      nodes[i].textContent = text
    }   
  }
}
```





