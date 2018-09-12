# @`web workers`

`Web Workers` 使得一个 `Web` 应用程序可以在与主执行线程分离的后台线程中运行一个脚本操作. 这样做的好处是可以在一个单独的线程中执行费时的处理任务, 从而允许主(通常是UI)线程运行而不被阻塞/放慢.

# @使用

`setTimeout` 和 `Web Worker`随着 `Ajax` 应用的流行,浏览器所承担的职责也越来越多.
一些原来由服务器端执行的计算操作也被迁移到浏览器端来执行.
通过 `JavaScript` 工作线程,可以在不影响页面本身运行的情况下,在后台运行耗时的任务.

```javascript
/* 创建 */
var worker = new Worker('task.js');

/* 通信 */
// main.js
var worker = new Worker('doWork.js');

worker.addEventListener('message', function(e) {
    console.log('Worker said: ', e.data);
}, false);

worker.postMessage('Hello World'); // Send data to our worker.

// doWork.js
self.addEventListener('message', function(e) {
    self.postMessage(e.data);
}, false);

/* 停止 */
myWorker.terminate();

// worker内部
self.close()

/* 处理错误 */
worker.onerror = function() {
    console.log('There is an error with your worker!');
}
```

## `Example`

```html
<p><label for="limit">计算范围上界:</label><input type="text" id="limit" value="100000"></input><button onclick="calculate();">开始计算</button></p>
<p><button onclick="testUI();">界面响应测试</button></p>
```

```javascript
// main.js
var worker = new Worker("prime_worker.js");

worker.onmessage = function(event) {
    var result = event.data;
    alert("计算完成,质数个数为:" + result);
};

function calculate() {
    var limit = parseInt(document.getElementById("limit").value) || 100000;
    worker.postMessage(limit);
}

function testUI() {
    alert("界面响应.");
}
```

```javascript
// prime_worker.js
function isPrime(n) {
    if (n == 0 || n == 1) {
        return false;
    }
    var bound = Math.floor(Math.sqrt(n));
    for (var i = 2; i <= b ound; i++) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

function calculateNormal(limit) {
    var count = 0;
    for (var i = 2; i <= l imit; i++) {
        if (isPrime(i)) {
            count++;
        }
    }
    return count;
}
onmessage = f unction(event) {
    var limit = e vent.data;
    var count = c alculateNormal(limit);
    postMessage(count);
}
```

# @适用场景

由于 `Web Worker` 的多线程行为, 所以它们只能使用 `JavaScript` 功能的子集:

- `navigator` 对象
- `location` 对象（只读）
- `XMLHttpRequest`
- `setTimeout()/clearTimeout()` 和 `setInterval()/clearInterval()`
- `Application Cache`
- `importScripts()`
- 生成其他 `Web Worker`

## 无法使用的场景

- `DOM`(非线程安全)
- `window` 对象
- `document` 对象
- `parent` 对象

# @参考

IBM developerWorks JavaScript 工作线程实现方式 (https://www.ibm.com/developerworks/cn/web/1105_chengfu_jsworker/)

The Basics of Web Workers (https://www.html5rocks.com/zh/tutorials/workers/basics/)
