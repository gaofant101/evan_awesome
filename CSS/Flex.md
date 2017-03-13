#### FLEXCSS 弹性盒子布局是 CSS 的模块之一，定义了一种针对用户界面设计而优化的 CSS 盒子模型。在弹性布局模型中，弹性容器的子元素可以在任何方向上排布，也可以“弹性伸缩”其尺寸，既可以增加尺寸以填满未使用的空间，也可以收缩尺寸以避免父元素溢出。子元素的水平对齐和垂直对齐都能很方便的进行操控。通过嵌套这些框（水平框在垂直框内，或垂直框在水平框内）可以在两个维度上构建布局。
[深入理解 CSS3 弹性盒布局模型](https://www.ibm.com/developerworks/cn/web/1409_chengfu_css3flexbox/#_清单 1.简单的图片缩略图预览页面的 HTML 代码)[使用 CSS 弹性盒子](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout)[使用CSS3 Flexbox布局](https://www.w3cplus.com/css3/css3-flexbox-layout.html)

[ISUX -> 移动端全兼容的flexbox速成班](https://isux.tencent.com/flexbox.html)

## exampel

	<div class="flex-box">
		<div class="flex-item">1</div>
		<div class="flex-item">2</div>
		<div class="flex-item">3</div>
		<div class="flex-item">1.1</div>
		<div class="flex-item">2.1</div>
		<div class="flex-item">3.1</div>
		<div class="flex-item">1.2</div>
		<div class="flex-item">2.2</div>
		<div class="flex-item">3.2</div>
	</div>
	<style>
		.flex-box{
			display: flex;
			width: 500px;
			height: 300px;
			/*flex-direction 指定元素以何种方式排列 row row-reverse column column-reverse*/
			/*row -> 列 column -> 行*/
			/*flex-direction: row;*/
			/*换行 和元素flex值关联 wrap-reverse -> 也是换行，表现形式不一样*/
			flex-wrap: wrap;
			/*定义父容器内元素水平方向的空间*/
			justify-content: flex-end;
			/*定义父容器内元素垂直方向的空间*/
			/*align-content: space-between;*/
			/*定义父容器内元素垂直方向的对齐方式*/
			/*align-items: center;*/
		}
		.flex-box > div{
			flex: auto;
			background: #ccc;
		}
		.flex-item:first-child{
			width: 500px;
			background: #956;
			/*定义item拉伸值 不能为负值*/
			/*flex-grow: 10;*/
			/*定义item收缩值 不能为负值*/
			/*flex-shrink: 2;*/
			/*定义排序优先值*/
			order: 2;
		}
		.flex-item:nth-child(2n){
			background: #965;
			/*定义item拉伸值 不能为负值*/
			flex-grow: 2;
			/*定义排序优先值*/
			order: 1;
		}
		.flex-item:nth-child(3n){
			background: #556;
			/*定义item拉伸值 不能为负值*/
			flex-grow: 3;
			/*定义排序优先值*/
			order: 3;
		}
	</style>