### let 和 const

ES6新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。

### 不存在变量提升

let命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

	// var 的情况
	console.log(foo); // 输出undefined
	var foo = 2;
	
	// let 的情况
	console.log(bar); // 报错ReferenceError
	let bar = 2;

### 暂时性死去

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

	var tmp = 123;
	
	if (true) {
	  tmp = 'abc'; // ReferenceError
	  let tmp;
	}


### 不允许重复声明

let不允许在相同作用域内，重复声明同一个变量。

	// 报错
	function () {
	  let a = 10;
	  var a = 1;
	}
	
	// 报错
	function () {
	  let a = 10;
	  let a = 1;
	}
	
### 块级作用域

	var tmp = new Date();
	
	function f() {
	  console.log(tmp);
	  if (false) {
	    var tmp = 'hello world';
	  }
	}
	
	f(); // undefined


### const基本语法

const声明一个只读的常量。一旦声明，常量的值就不能改变。

const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指针，const只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。

	const foo = {};
	
	// 为 foo 添加一个属性，可以成功
	foo.prop = 123;
	foo.prop // 123
	
	// 将 foo 指向另一个对象，就会报错
	foo = {}; // TypeError: "foo" is read-only
	
