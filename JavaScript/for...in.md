# @ `for...in`

`for...in` 语句以任意顺序遍历一个对象的可枚举属性.对于每个不同的属性,语句都会被执行.

## 语法

```javascript
for (variable in object) {...}
```

## 参数

`variable`在每次迭代时,将不同的属性名分配给变量.
`object `被迭代其枚举属性的对象.

## 描述

`for...in` 循环只遍历可枚举属性.像 `Array` 和 `Object` 使用内置构造函数所创建的对象都会继承自 `Object.prototype` 和 `String.prototype` 的不可枚举属性,例如 `String` 的 `indexOf()`  方法或者 `Object` 的 `toString` 方法.循环将迭代对象的所有可枚举属性和从它的构造函数的 `prototype` 继承而来的（包括被覆盖的内建属性）.


## `Array` 迭代和 `for...in`

数组索引仅是可枚举的整数名,其他方面和别的普通对象属性没有什么区别.`for...in` 并不能够保证返回的是按一定顺序的索引,但是它会返回所有可枚举属性,包括非整数名称的和继承的.

因为迭代的顺序是依赖于执行环境的,所以数组遍历不一定按次序访问元素. 因此当迭代那些访问次序重要的 `arrays` 时用整数索引去进行 `for` 循环 (或者使用 `Array.prototype.forEach()` 或 `for...of` 循环) .

## 仅迭代自身的属性

如果你只要考虑对象本身的属性,而不是它的原型,那么使用 `getOwnPropertyNames()` 或执行  `hasOwnProperty()` 来确定某属性是否是对象本身的属性 (也能使用`propertyIsEnumerable`).另外,如果你知道外部不存在任何的干扰代码,你可以扩展内置原型与检查方法.

```javascript
var obj = {
    a:1,
    b:2,
    c:3
};

for (var prop in obj) {
  console.log("obj." + prop + " = " + obj[prop]);
}

// Output:
// "obj.a = 1"
// "obj.b = 2"
// "obj.c = 3"
```

下面的函数阐述了 `hasOwnProperty()` 的用法: 隐藏的继承属性将不会被显示.

```javascript
var triangle = {
    a:1,
    b:2,
    c:3
};

function ColoredTriangle() {
    this.color = "red";
}

ColoredTriangle.prototype = triangle;

var obj = new ColoredTriangle();

for (var prop in obj) {
    if( obj.hasOwnProperty( prop ) ) {
        console.log("o." + prop + " = " + obj[prop]);
    }
}

// Output:
// "o.color = red"
```
