## setState

```
setState(updater, [callback])
```

`setState()`对组件状态进行队列更改,并告知`React`,该组件及其子组件需要以更新状态重新呈现.这是用于更新用户界面以响应事件处理程序和服务器响应的主要方法.

将其`setState()`视为请求而不是即时命令来更新组件.为了更好的感知性能,`React`可能会延迟它,然后在单次通过中更新多个组件.`React`不能保证立即应用状态更改.

`setState()`并不总是立即更新组件.它可能会批量或延迟更新直到后来.`this.state`调用`setState()`潜在的陷阱之后,这就使阅读权.相反,使用`componentDidUpdate`或`setState`回调（`setState(updater, callback)`）,其中任何一个都保证在应用更新后触发.如果您需要根据先前的状态设置状态,请阅读`updater`下面的参数.

`setState()`将永远导致重新渲染,除非`shouldComponentUpdate()`返回`false`.如果使用可变对象并且无法实现条件呈现逻辑`shouldComponentUpdate()`,则`setState()`只有当新状态与先前状态不同时才调用,才能避免不必要的重渲染.

## `setState` 使用动态`key`值该怎么写

```
example = (key, value) => {
    this.setState({
        key: value,
    })
}
```

这段示例代码`key`是一个动态的值.   
想通过传进来的`key`去响应`state`的状态,但是实际运行是找不到`state`里对应的`key`值的.   
因为代码执行的执行的时候是找`key`这个关键字,并不是动态传进来的值.   

这应该和`JSX`语法也有关系, `state`是一个对象,那么就去查找`Object`是怎么操作对象属性的.   

从`ECMAScript 2015`开始,对象初始化语法开始支持计算的属性名.其允许在`[]`中放入表达式,计算结果可以当做属性名.这种用法和用方括号访问属性非常类似,也许你已经用来读取和设置属性了.现在同样的语法也可以用于对象字面值了:

```
// Computed property names (ES6)
var i = 0;
var a = {
    ["foo" + ++i]: i,
    ["foo" + ++i]: i,
    ["foo" + ++i]: i
};

console.log(a.foo1); // 1
console.log(a.foo2); // 2
console.log(a.foo3); // 3

var param = 'size';
var config = {
    [param]: 12,
    ["mobile" + param.charAt(0).toUpperCase() + param.slice(1)]: 4
};

console.log(config); // { size: 12, mobileSize: 4 }
```

从上面示例可以看出`[key]`这种写法是可以用于对象的字面值了   
回到上最初的示例代码:
```diff
example = (key, value) => {
    this.setState({
-        key: value,
+        [key]: value,
    })
}
```

## 参考资料

[React setState](https://facebook.github.io/react/docs/react-component.html#setstate)

[Object 计算的属性名](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Object_initializer)

[Reactjs setState() with a dynamic key name?](https://stackoverflow.com/questions/29280445/reactjs-setstate-with-a-dynamic-key-name)

[Reactjs handling-multiple-inputs](https://facebook.github.io/react/docs/forms.html#handling-multiple-inputs)
