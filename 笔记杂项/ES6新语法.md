#### ES6新语法

**1.Object.is()**

​		`Object.is`就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

​		ES5实现:

```javascript
Object.defineProperty(Object,'is',{
    value:funciton(){
    	if(x === y){
    		return x !== 0 || 1 / x === 1 / y 
    		return x !== x && y !== y;
		}
	configurable:true,
    enumerable:false,
    writable:true
	}
})
```

**2.Object.assign()**

​		`Object.assign()`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

​	**浅拷贝**

