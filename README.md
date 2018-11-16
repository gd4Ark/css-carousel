# CSS轮播

顾名思义，就是使用纯HTML+CSS开发图片轮播功能。

**主要功能如下：**

- 底部栏切换
- 两侧按钮切换
- 无缝轮播

	*主要思路为：*

	定义一堆`<input type="radio">`，通过CSS的兄弟选择器`~`来控制图片容器的`margin-left`值进行切换。

	使用`label`标签代理`<input type="radio">`的点击。

如果对你有帮助，欢迎Star！