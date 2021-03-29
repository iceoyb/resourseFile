this指向理解：

this是指函数运行时所在的环境

this有以下四种调用情况

* 纯粹的函数调用--指向调用环境
* 作用对象属性调用--指向调用对象
* 作为构造函数调用--指向实例
* 通过apply调用--指向函数的第一个参数

**注：箭头函数无this，内部this为继承自外部作用域顶端

使用案例：

```javascript
var a = 'wina'
var b = 'winb'
var obj = {
  a: 'obja',
  b: 'objb',
  printA: function () { console.log(this.a) },
  printB: () => { console.log(this.b) },
  funcPrintB:  function(){
    return this.hc = {
      a:'hca',
      b:'hcb',
      printA:function(){console.log(this.a)}
    }
  }
}
obj.funcPrintB().printA.apply({a:'newObjA'})

```

