# @ `Object`

构造函数创建一个对象包装器.

## 对象初始化/字面量语法

对象可以通过 `new Object()`, `Object.create()` 方法,或者使用字面 标记 (初始化 标记)初始化.
对象初始化,由花括号{}包含的一个由0个或者多个对象属性名和关联值组成的列表构成.

## 语法

```javascript
var obj = {};
var obj = {
    a: 'foo',
    b: 42,
    c: {},
};

var a = 'foo', b = 42, c = {};
var obj = {
    a: a,
    b: b,
    c: c,
};

var obj = {
    property: function () {},
    get property() {},
    set property(value) {},
};
```

## 描述

对象初始化是一个描述对象初始化过程的表达式.对象初始化是由一组描述对象的属性组成.属性的值可以是固有类型,也可以是其他对象.

## 创建对象

没有属性的空对象可以用以下方式创建：

```javascript
var object = {};
```

不过,字面 和初始化 标记的优势在于,可以用内含属性的花括号快速创建对象.简单地编写一个逗号分隔的键:值对的类别.

```javascript
var object = {
    foo: 'bar',
    age: 42,
    baz: {
        myProp: 12,
    },
};
```

## 属性访问

```javascript
object.foo;  // 'bar'
object['age']; // 42

object.foo = 'bar';
```

我们可以将对象看做是一个关联数组,或映射,字典,哈希表,查找表.这个数组中的键就是这个对象中属性的名称.
通常,当我们提及一个对象的属性时,会对属性与方法之间做个对比.然而,属性与方法之间的区别并不大.

访问对象属性有两种方式：点符号表示法和括号表示法.

```javascript
// 点符号表示法
get = object.property;
object.property = set;

// 以上代码,属性必须要是一个有效的`javascript`标识符,只能是一串字符串字符(包括下划线及美元符号),不能以数字开头!
```

```javascript
// 括号表示法
get = object[property_name];
object[property_name] = set;

// `property_name` 可以为任意字符串,例如`1foo` `!bar!` 甚至可以为空格;
```

## 属性名

属性名必须是字符串,这意味着非字符串对象不能用来作为一个对象的属性键.
任何非字符串对象,包括`Number`可通过`toString()`方法类型转换成字符串;

```javascript
var object = {};
object['1'] = 'value';
console.log(object[1]); // value
```

```javascript
var foo = {
    unique_prop: 1,
};
var bar = {
    unique_prop: 2,
};
var object = {};
object[foo] = 'value';
console.log(object[bar]);

// 最终输出为`value`,由于对象`foo`和`bar`赋值的时候都被转换成字符串`[object Object]`;
```

## 重复属性名

属性使用了同样的名称时,后面的属性会覆盖前面的属性.

```javascript
var a = {
    x: 1,
    x: 2,
};
console.log(a); // {x: 2}
```
