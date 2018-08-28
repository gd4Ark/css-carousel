# CSS轮播

顾名思义，就是使用纯HTML+CSS开发图片轮播功能。

**主要功能如下：**

- 底部栏切换
- 两侧按钮切换
- 无缝轮播

	*主要思路为：**	

	定义一堆`<input type="radio">`，通过CSS的兄弟选择器`~`来控制图片容器的`margin-left`值进行切换。

	使用`label`标签代理`<input type="radio">`的点击。

**部分代码：**

**HTML结构：**

```html
    <div class="container">
        <!-- 底部控制板按钮 隐藏-->
        <input type="radio" name="input-btn" id="count-item-1" checked>
        <input type="radio" name="input-btn" id="count-item-2">
        <input type="radio" name="input-btn" id="count-item-3">
        <!-- 两侧按钮 隐藏 -->
        <!-- 前一张 -->
        <input type="radio" name="input-btn" id="prev-btn-1">
        <input type="radio" name="input-btn" id="prev-btn-2">
        <input type="radio" name="input-btn" id="prev-btn-3">
        <!-- 后一张 -->
        <input type="radio" name="input-btn" id="next-btn-1">
        <input type="radio" name="input-btn" id="next-btn-2">
        <input type="radio" name="input-btn" id="next-btn-3">
        <!-- 两侧按钮 显示 -->
        <div class="prev-btn side-btn">
            <label for="prev-btn-1"></label>
            <label for="prev-btn-2"></label>
            <label for="prev-btn-3"></label>
        </div>
        <div class="next-btn side-btn">
            <label for="next-btn-1"></label>
            <label for="next-btn-2"></label>
            <label for="next-btn-3"></label>
        </div>
        <!-- 底部控制板 显示 -->
        <ul class="count-list">
           <li class="count-item count-item-1">
               <label for="count-item-1"></label>
           </li>
           <li class="count-item count-item-2" >
               <label for="count-item-2"></label>
           </li>
           <li class="count-item count-item-3">
               <label for="count-item-3"></label>
           </li>
        </ul>
        <!-- 图片容器 -->
        <div class="pic-list">
            <div class="pic-item pic-item-1">ONE</div>
            <div class="pic-item pic-item-2">TWO</div>
            <div class="pic-item pic-item-3">THREE</div>
        </div>
        <!-- 无缝轮播 -->
        <div class="pic-after">
            <div class="pic-item">THREE</div>
            <div class="pic-item">ONE</div>
        </div>
    </div>
```

注意：

 - 因为要用兄弟选择器来进行控制，所以`input`标签要与其他容器标签为同级标签，且要放在前面

**部分CSS代码：**

```css
label{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    cursor: pointer;
}

.container{
    position: relative;
    overflow: hidden;
}
/* 图片容器 */
.container .pic-list{
    position: absolute;
    top: 0;
    left: 0;
    width: 300%; /* 300% 对应 3张图片 */
    height: 100%;
    margin-left: 0;
    transition: margin 0.5s ease;
}
.pic-item{
    float: left;
    width : calc(100% / 3); /* 计算每个子元素的宽度 */
    height: 100%;
}
/* 无缝轮播 */
.container .pic-after{
    position: absolute;
    top: 0;
    left: 0;
    width: 200%;
    height: 100%;
    z-index: -1;
}
.container .pic-after div{
    width: 50%;
}
```

**控制部分代码：**

```css
/* 所有的按钮选中后都会执行 */
input[name="input-btn"]:checked ~ .count-list .count-item{
    background:rgba(255, 255, 255, 0.5);
}
input[name="input-btn"]:checked ~ .side-btn label{
    display: none;
}
/* 考虑哪些按钮选中后会显示第一张 */
/* 显示第一张图片 */
/* 图片容器偏移 */
#count-item-1:checked ~ .pic-list,
#prev-btn-2:checked ~ .pic-list,
#next-btn-3:checked ~ .pic-list{
    margin-left: 0;
}
/* 设置当前图片对应的底部点的样式 */
#count-item-1:checked ~ .count-list .count-item-1,
#prev-btn-2:checked ~ .count-list .count-item-1,
#next-btn-3:checked ~ .count-list .count-item-1{
    background:rgba(255,255,255,1);
}
/* 显示对应的两侧按钮 */
#count-item-1:checked ~ .side-btn label:nth-child(1),
#prev-btn-2:checked  ~ .side-btn label:nth-child(1),
#next-btn-3:checked ~ .side-btn label:nth-child(1){
    display: block;
}
/* 以此类推 */

/* 无缝轮播 */
#prev-btn-1:checked ~ .pic-after,
#next-btn-3:checked ~ .pic-after{
    z-index: 1;
}
#prev-btn-1:checked ~ .pic-after{
    animation: moveRight 0.5s;
}
#next-btn-3:checked ~ .pic-after{
    margin-left: -100%;
    animation: moveLeft 0.5s;
}
@keyframes moveLeft{
    0%{
        margin-left: 0;
    }
    100%{
        margin-left: -100%;
    }
}
@keyframes moveRight{
    0%{
        margin-left: -100%;
    }
    100%{
        margin-left: 0;
    }
}
```

如果对你有帮助，欢迎Star！