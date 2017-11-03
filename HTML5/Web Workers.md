# @ `web workers`

JavaScript 工作线程实现方式

## @ 使用

`setTimeout` 和 `Web Worker` 随着 `Ajax` 应用的流行,浏览器所承担的职责也越来越多.   
一些原来由服务器端执行的计算操作也被迁移到浏览器端来执行.   
通过 `JavaScript` 工作线程,可以在不影响页面本身运行的情况下,在后台运行耗时的任务.

## `Example`

```html
<p><label for="limit">计算范围上界:</label><input type="text" id="limit" value="100000"></input><button onclick="calculate();">开始计算</button></p>
<p><button onclick="testUI();">界面响应测试</button></p>
```

```javascript
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

## @参考

[IBM developerWorks JavaScript 工作线程实现方式](https://www.ibm.com/developerworks/cn/web/1105_chengfu_jsworker/)
