### Object.prototype.hasOwnProperty()


`hasOwnProperty()` 方法会返回一个布尔值，其用来判断某个对象是否含有指定的属性。

所有继承了 Object 的对象都会继承到 hasOwnProperty 方法。这个方法可以用来检测一个对象是否含有特定的自身属性；和 in 运算符不同，该方法会忽略掉那些从原型链上继承到的属性。

### 语法
	
	obj.hasOwnProperty(prop)
	
### 参数

`prop`要检测的属性  字符串 名称或者 Symbol

### 返回值

用来判断某个对象是否含有指定的属性的 Boolean 

	o = new Object();
	o.prop = 'exists';
	
	function changeO() {
	  o.newprop = o.prop;
	  delete o.prop;
	}
	
	o.hasOwnProperty('prop');   // 返回 true
	changeO();
	o.hasOwnProperty('prop');   // 返回 false

&nbsp;

	o = new Object();
	o.prop = 'exists';
	o.hasOwnProperty('prop');             // 返回 true
	o.hasOwnProperty('toString');         // 返回 false
	o.hasOwnProperty('hasOwnProperty');   // 返回 false
	
### 使用 hasOwnProperty 作为属性名

JavaScript 并没有保护 hasOwnProperty 属性名，因此某个对象是有可能存在使用这个属性名的属性，使用外部的 hasOwnProperty 获得正确的结果是需要的：

	var foo = {
	    hasOwnProperty: function() {
	        return false;
	    },
	    bar: 'Here be dragons'
	};
	
	foo.hasOwnProperty('bar'); // 始终返回 false
	
	// 如果担心这种情况，可以直接使用原型链上真正的 hasOwnProperty 方法
	({}).hasOwnProperty.call(foo, 'bar'); // true
	
	// 也可以使用 Object 原型上的 hasOwnProperty 属性
	Object.prototype.hasOwnProperty.call(foo, 'bar'); // true