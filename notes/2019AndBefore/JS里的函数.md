## 如何调用函数

```
f.call(asThis, input1,input2)
其中 asThis 会被当做 this，[input1,input2] 会被当做 arguments
禁止使用 f(input1, input2)
```