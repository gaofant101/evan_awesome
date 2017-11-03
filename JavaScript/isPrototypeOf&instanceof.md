## @ `isPrototypeOf`

`isPrototypeOf` 方法用于检测一个对象是否存在于另一个对象的原型链上.   

### 语法

```javascript
prototypeObj.isPrototypeOf(object)
```

### 参数

`object`在该对象上的原型链上搜索

### 返回值

`Boolean`

### e.g.

```javascript
function Fee() {
  // . . .
}

function Fi() {
  // . . .
}
Fi.prototype = new Fee();

function Fo() {
  // . . .
}
Fo.prototype = new Fi();

function Fum() {
  // . . .
}
Fum.prototype = new Fo();

var fum = new Fum();

// 下面创建一个 Fum 实例，检测 Fi.prototype 是否存在于该实例的原型链上.
if (Fi.prototype.isPrototypeOf(fum)) {
  // do something safe
}
```

## @ `instanceof`

`instanceof` 运算符用来测试一个对象在其原型链中存在一个构造函数的`prototype`属性.

### 语法

```javascript
object instanceof constructor
```

### 参数

`object`要检测的对象

`constructor`某个构造函数

### e.g.

```
// 定义构造函数
function C(){}
function D(){}

var o = new C();

o instanceof C;  // true,因为 Object.getPrototypeOf(o) === C.prototype

o instanceof D;  // false,因为 D.prototype不在o的原型链上

o instanceof Object; // true,因为Object.prototype.isPrototypeOf(o)返回true

C.prototype instanceof Object // true,同上

C.prototype = {};
var o2 = new C();

o2 instanceof C; // true

o instanceof C; // false,C.prototype指向了一个空对象,这个空对象不在o的原型链上.

D.prototype = new C(); // 继承
var o3 = new D();
o3 instanceof D; // true
o3 instanceof C; // true
```

> 需要注意的是,如果表达式 `obj instanceof Foo` 返回`true`,则并不意味着该表达式会永远返回true,
因为`Foo.prototype`属性的值有可能会改变,改变之后的值很有可能不存在于`obj`的原型链上,这时原表达式
的值就会成为`false`.另外一种情况下,原表达式的值也会改变,就是改变对象`obj`的原型链的情况,虽然在
目前的`ES`规范中,我们只能读取对象的原型而不能改变它,但借助于非标准的`__proto__`魔法属性,是可以
实现的.比如执行`obj.__proto__` = {}之后,`obj instanceof Foo`就会返回`false`了.

### e.g. 2

下面的代码使用了`instanceof`来证明:` String`和`Date`对象同时也属于`Object`类型.

```javascript
var simpleStr = "This is a simple string";
var myString  = new String();
var newStr    = new String("String created with constructor");
var myDate    = new Date();
var myObj     = {};

simpleStr instanceof String; // returns false   检查原型链会找到 undefined
myString  instanceof String; // returns true
newStr    instanceof String; // returns true
myString  instanceof Object; // returns true

myObj instanceof Object;    // returns true    despite an undefined prototype
({})  instanceof Object;    // returns true    同上

myString instanceof Date;   // returns false

myDate instanceof Date;     // returns true
myDate instanceof Object;   // returns true
myDate instanceof String;   // returns false
```

下面的代码创建了一个类型`Car`,以及该类型的对象实例`mycar`. `instanceof`运算符表明了这个`mycar`对象既属于`Car`类型,又属于`Object`类型.

```javascript
function Car(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
}
var mycar = new Car("Honda", "Accord", 1998);
var a = mycar instanceof Car;    // 返回 true
var b = mycar instanceof Object; // 返回 true
```
