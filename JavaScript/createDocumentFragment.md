# @简介

创建一个新的空白的文档片段( `DocumentFragment`).

## 语法

```javascript
let docFragment = document.createDocumentFragment();
```

`DocumentFragments` 是`DOM`节点.它们不是主`DOM`树的一部分.通常的用例是创建文档片段,
将元素附加到文档片段,然后将文档片段附加到`DOM`树.在`DOM`树中，文档片段被其所有的孩子所代替.

因为文档片段存在于内存中,并不在DOM树中,所以将子元素插入到文档片段时不会引起页面回流(reflow)
(对元素位置和几何上的计算).因此,使用文档片段`document fragments` 通常会起到优化性能的作用(`better performance`).

## 测试

看文档解释觉得这个`API`很高大上,联想到`React&Vue`的虚拟`DOM`也是整片代码段映射到真是的`DOM`节点中;是不是这个原理呢;

```javascript
// createDocumentFragment
let s = (new Date).getTime();
let ul = document.querySelector('#ul'),
    docfrag = document.createDocumentFragment();

const browserList = [];

for (var i = 0; i < 100000; i++) {
    browserList.push(i);
}

browserList.forEach((e) => {
    let li = document.createElement('li');
    li.textContent = e;
    docfrag.appendChild(li);
})

ul.appendChild(docfrag);
document.body.innerHTML = "<p>DocumentFragment Append: " + ((new Date).getTime() - s) + "</p>" + document.body.innerHTML;

// 结果为: 215 234 276 236 244 223
```

```javascript
// Normal
let s = (new Date).getTime();
let ul = document.querySelector('#ul'),
    docfrag = document.createDocumentFragment();

const browserList = [];

for (var i = 0; i < 100000; i++) {
    browserList.push(i);
}

browserList.forEach((e) => {
    let li = document.createElement('li');
    li.textContent = e;

    ul.appendChild(li);
})
document.body.innerHTML = "<p>Normal Append: " + ((new Date).getTime() - s) + "</p>" + document.body.innerHTML;

// 结果为: 139 156 198 157 193 156
```

```
设备: i5 8g
浏览器: chrome
```

这个测试结果完全不是它说了那么理想化,这个区别到底在哪里呢,是现在的浏览器底层优化做的好?

[jsfiddle e.g. createDocumentFragment](https://jsfiddle.net/evan_g/1emeL3ru/)
[jsfiddle e.g. Normal](https://jsfiddle.net/evan_g/ngk6f4ek/)

# @参考

[MDN Document.createDocumentFragment()](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createDocumentFragment)

[stackoverflow](https://stackoverflow.com/questions/13239618/is-there-any-benefit-to-using-createdocumentfragment-as-opposed-to-an-out-of-dom)
