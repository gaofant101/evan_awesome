## @ `Function`

## @ 箭头函数

箭头函数有几个使用注意点.

- 函数体内的this对象,就是定义时所在的对象,而不是使用时所在的对象.
- 不可以当作构造函数,也就是说,不可以使用new命令,否则会抛出一个错误.
- 不可以使用arguments对象,该对象在函数体内不存在.如果要用,可以用Rest参数代替.
- 不可以使用 `yield` 命令,因此箭头函数不能用作 `Generator` 函数.

## @ 尾递归

函数调用自身,称为递归.如果尾调用自身,就称为尾递归.

递归非常耗费内存,因为需要同时保存成千上百个调用帧,很容易发生栈溢出错误.但对于尾递归来说,由于只存在一个调用帧,所以永远不会发生栈溢出错误.

```javascript
function factorial(n) {
    if (n === 1) return 1;
    return n * factorial(n - 1);
}

factorial(5) // 120
```

上面代码是一个阶乘函数,计算n的阶乘,最多需要保存n个调用记录,复杂度 O(n) .

如果改写成尾递归,只保留一个调用记录,复杂度 O(1) .

```javascript
function factorial(n, total) {
    if (n === 1) return total;
    return factorial(n - 1, n * total);
}

factorial(5, 1) // 120
```

还有一个比较著名的例子,就是计算`fibonacci` 数列,也能充分说明尾递归优化的重要性

如果是非尾递归的`fibonacci` 递归方法

```javascript
function Fibonacci (n) {
    if ( n <= 1 ) {return 1};

    return Fibonacci(n - 1) + Fibonacci(n - 2);
}

Fibonacci(10); // 89
// Fibonacci(100)
// Fibonacci(500)
// 堆栈溢出了
```

如果我们使用尾递归优化过的`fibonacci` 递归算法

```javascript
function Fibonacci2 (n , ac1 = 1 , ac2 = 1) {
    if( n <= 1 ) {return ac2};

    return Fibonacci2 (n - 1, ac2, ac1 + ac2);
}

Fibonacci2(100) // 573147844013817200000
Fibonacci2(1000) // 7.0330367711422765e+208
Fibonacci2(10000) // Infinity
```
