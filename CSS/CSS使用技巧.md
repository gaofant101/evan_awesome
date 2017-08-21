## `chrome`输入框黄色背景

1. 通过修改样式来改变背景颜色   
```
// e.g. 1
input:-webkit-autofill {
    -webkit-box-shadow: 0 0 0 1000px white inset !important;  // 这种粗暴的方式对渲染性能有要求
}
```
```
// e.g. 2
input:-webkit-autofill {
    -webkit-transition-delay: 9999s;
    -webkit-transition: color 9999s ease-out, background-color 9999s ease-out;
}
```

2. 通过设置表单禁止浏览器自动填充
```
<input type="text" autocomplete="off" name="sometext" />
```

## 参考

[stackoverflow](https://stackoverflow.com/questions/2920306/google-chrome-form-autofill-and-its-yellow-background)

[stackoverflow](https://stackoverflow.com/questions/2781549/removing-input-background-colour-for-chrome-autocomplete)

[MDN input](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input)
