## 键盘事件

`KeyboardEvent` 对象描述了键盘的交互方式. 每个事件都描述了一个按键`(Each event describes a key)`;
事件类型`keydown`, `keypress` 与 `keyup` 可以确定是哪种事件在活动.

> `KeyboardEvent` 表示刚刚发生在按键上的事情.当你需要处理文本输入的时候，使用 `HTML5 input` 事件代替.
例如,用户使用手持系统如平板电脑输入时,按键事件可能不会触发.

通常Gecko这样派出事件:
- 当按键被按下时, 发送 `keydown` 事件
- 如果该按键不是修饰键, 发送 `keypress` 事件
- 当按键被释放时, 发送 `keyup` 事件

特殊情况:   

一些按键能切换指示灯的状态,如 `Caps Lock` 键, `Num Lock` 键和 `Scroll Lock` 键.
在 `Windows` 和 `Linux` 上, 这些按键仅发送 `keydown` 事件和 `keyup` 事件.


## 参考

[KeyboardEvent](https://developer.mozilla.org/zh-CN/docs/Web/API/KeyboardEvent)
