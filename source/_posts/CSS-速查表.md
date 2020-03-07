---
title: CSS 速查表
date: 2019-11-29 00:32:06
categories: [Dev, CSS]
tags:
    - CSS
toc: true
---
<!-- more -->
## 插入样式表

### 外部样式表

```html
<link rel="stylesheet" href="style.css">
```

### 内部样式表

```html
<style>
  div {
    color: red;
  }
</style>
```

### 内联样式表

```html
<div style="color=red"></div>
```



## Selector（选择器）

### 四种基本选择器

```css
// 元素选择器
div {
  margin: 0 auto;
}

// 属性选择器
[type="text"] {
  width: 150px;
}

// Id 选择器
#info {
  margin: 0 auto;
}

// Class 选择器
.container {
  margin: 0 auto;
}
```

### 三种关系选择器

```css
// 后代选择器
h1 strong {
	color: red;
}

// 子元素选择器
h1 > strong {
  color: red;
}

// 兄弟选择器
h1 + p {
  margin: 0 auto;
}
```

### 伪类选择器和伪元素选择器

```css
// 伪类选择器
// 未访问的连接
a:link {
  color: red;
}
// 已访问的连接
a:visited {
  color: purple;
}
// 鼠标移动到链接上
a:hover {
  color: grey;
}
// 选定的链接
a:active {
  color: blue;
}
```

```css
// 伪元素选择器
h1:before {
  content: url(logo.png);
}
.container:after {
	float: clear;
}

p:first-letter {
  font-size: xx-large;
}
p:first-line {
  color: blue;
}
```

## Background（背景）

### background-color (背景颜色)

| 值                 | 描述                               |
| ------------------ | ---------------------------------- |
| white              | 规定颜色值为颜色名称的背景颜色     |
| #ffffff            | 规定颜色值为十六进制值的背景颜色   |
| rgb(255, 255, 255) | 规定颜色值为 rgb 代码的背景颜色    |
| transparent        | 默认；背景颜色为透明               |
| inherit            | 从父元素继承 background-color 的值 |

### background-image (背景图片)

| 值       | 描述                               |
| -------- | ---------------------------------- |
| url(URL) | 指向图像的路径                     |
| none     | 默认值；不显示背景图像             |
| inherit  | 从父元素继承 background-image 的值 |

### background-repeat (是否重复)

| 值        | 描述                                     |
| --------- | ---------------------------------------- |
| repeat    | 默认；背景图像在垂直方向和水平方向上重复 |
| repeat-x  | 背景图像在水平方向上重复                 |
| repeat-y  | 背景图像在垂直方向上重复                 |
| no-repeat | 背景图像不重复，仅显示一次               |
| inherit   | 从父元素继承 background-repeat 的值      |

### background-position (背景位置)

- 关键字
  - center
  - top
  - bottom
  - right
  - left
  - 可组合，如：top right
- 百分比
  - 0% 0%    位于左上角
  - 50% 50%    位于中心
  - 100% 100%    位于右下角
- 长度值
  - 0px 0px 位于左上角
  - 50px 50px 位于内边距偏移50像素

### background-attachment (背景依附)

| 值      | 描述                                           |
| ------- | ---------------------------------------------- |
| scroll  | 默认值；背景图片会随着页面其余部分到滚动而移动 |
| fixed   | 当页面到其余部分滚动时，背景图片不会移动       |
| inherit | 从父元素继承 background-attachment 的值        |

### background (简写形式)

```css
background: #00ff00 url(image.png) no-repeat fixed top;
```



## Text（文本）

### color (文本颜色)

| 值    | 描述                           |
| ----- | ------------------------------ |
| white              | 规定颜色值为颜色名称的背景颜色     |
| #ffffff            | 规定颜色值为十六进制值的背景颜色   |
| rgb(255, 255, 255) | 规定颜色值为 rgb 代码的背景颜色    |
| inherit | 从父元素继承 color 的值 |

### text-align (文本对齐方式)

| 值      | 描述                         |
| ------- | ---------------------------- |
| left    | 文本左对齐                   |
| right   | 文本右对齐                   |
| center  | 文本居中对齐                 |
| justify | 文本两端对齐                 |
| inherit | 从父元素继承 text-align 的值 |

### text-decoration (文本修饰)

| 值           | 描述                              |
| ------------ | --------------------------------- |
| none         | 默认；定义标准的文本              |
| underline    | 定义文本下的一条线                |
| overline     | 定义文本上的一条线                |
| line-through | 定义穿过文本下的一条线            |
| blink        | 定义闪烁的文本                    |
| inherit      | 从父元素继承 text-decoration 的值 |

### text-transform (文本转换)

| 值         | 描述                                       |
| ---------- | ------------------------------------------ |
| none       | 默认；定义带有小写字母和大写字母的标准文本 |
| capitalize | 文本中的每个单词都以大写字母开头           |
| uppercase  | 全部转换为大写字母                         |
| lowercase  | 全部转换为小写字母                         |
| inherit    | 从父元素继承 text-transform 的值           |

### text-indent (文本缩进)

| 值                  | 描述                                          |
| ------------------- | --------------------------------------------- |
| *length* (例：50px) | 使用单位定义缩进长度                          |
| 20%                 | 使用基于父元素宽度百分比定义缩进长度(例：5px) |
| inherit             | 从父元素继承 text-indent 的值                 |

### word-spacing (单词/字间隔)

| 值      | 描述                           |
| ------- | ------------------------------ |
| normal  | 默认；定义单词间的标准空间     |
| 50px    | 定义单词间的固定单位间距       |
| inherit | 从父元素继承 word-spacing 的值 |

### letter-spacing (设置字符间距)

| 值                 | 描述                                 |
| ------------------ | ------------------------------------ |
| normal             | 默认；规定字符间没有额外的空间       |
| *length* (例：2px) | 定义字符间的固定空间（允许使用负值） |
| inherit            | 从父元素继承 letter-spacing 的值     |

### line-height (设置行高)

| 值                 | 描述                                               |
| ------------------ | -------------------------------------------------- |
| normal             | 默认；自动设置合理的行间距                         |
| *number*           | 设置数字，该数字会与当前的字体尺寸相乘来设置行间距 |
| *length* (例：5px) | 设置固定的行间距                                   |
| %                  | 基于当前字体尺寸的百分比行间距                     |
| inherit            | 从父元素继承 line-height 的值                      |



## Fonts（字体）

### font-style (字体样式)

| 值      | 描述                                 |
| ------- | ------------------------------------ |
| normal  | 默认值；浏览器显示一个标准的字体样式 |
| italic  | 浏览器会显示一个斜体的字体样式       |
| oblique | 浏览器会显示一个倾斜的字体样式       |
| inherit | 从父元素继承字体样式                 |

### font-size (字体大小)

| 值                 | 描述                           |
| ------------------ | ------------------------------ |
| xx-small           | 特小号字                       |
| x-small            | 较小号字                       |
| small              | 小号字                         |
| medium             | 中号字                         |
| large              | 大号字                         |
| x-large            | 较大号字                       |
| xx-large           | 特大号字                       |
| smaller            | 设置为比父元素更小的尺寸       |
| larger             | 设置为比父元素更大的尺寸       |
| *length* (例：5px) | 设置为一个固定的值             |
| %                  | 设置为基于父元素的一个百分比值 |
| inherit            | 从父元素继承字体尺寸           |

### font-family (字体)

| 值      | 描述             |
| ------- | ---------------- |
| 字体名  | 字体名           |
| inherit | 从父元素继承字体 |

### font-variant (是否以小型大写字母的字体显示文本)

| 值         | 描述                               |
| ---------- | ---------------------------------- |
| normal     | 默认值；浏览器会显示一个标准的字体 |
| small-caps | 浏览器会显示小型大写字母字体       |
| inherit    | 从父元素继承 font-variant 的值     |

### font-weight (字体粗细)

| 值      | 描述                   |
| ------- | ---------------------- |
| normal  | 默认；标准的字符       |
| bold    | 粗体                   |
| bolder  | 更粗字体               |
| lighter | 更细字体               |
| 100~900 | 由细到粗的字符         |
| inherit | 从父元素继承字体的粗细 |



## List（列表）

### list-style-image (图片标记)

| 值      | 描述                               |
| ------- | ---------------------------------- |
| URL     | 图像的路径                         |
| none    | 默认值；无图像被显示               |
| inherit | 从父元素继承 list-style-image 的值 |

### list-style-position (标记位置)

| 值      | 描述                                                         |
| ------- | ------------------------------------------------------------ |
| inside  | 列表项目标记放置在文本以内，且环绕文本根据标记对齐           |
| outside | 默认值；保持标记位于文本的左侧；列表项目标记放置在文本以外，且环绕文本不根据标记对齐 |
| inherit | 从父元素继承 list-style-position 的值                        |

### list-style-type (列表标记)

| 值                   | 描述                   |
| -------------------- | ---------------------- |
| none                 | 无标记                 |
| disc                 | 默认；实心圆           |
| circle               | 空心圆                 |
| square               | 实心方块               |
| decimal              | 数字                   |
| decimal-leading-zero | 0开头的数字(01,02,03…) |
| lower-roman          | 小写罗马字母           |
| upper-roman          | 大写罗马字母           |
| lower-alpha          | 小写英文字母           |
| upper-alpha          | 大写英文字母           |



## Border（边框）

### border-style (边框样式)

| 值      | 描述                               |
| ------- | ---------------------------------- |
| none    | 无边框                             |
| hidden  | 与 "none" 相同，用于解决表边框冲突 |
| dotted  | 点状                               |
| dashed  | 虚线                               |
| solid   | 实线                               |
| double  | 双实线                             |
| groove  | 3D 凹槽边框                        |
| ridge   | 3D 垄状边框                        |
| inset   | 3D inset 边框                      |
| outset  | 3D outset 边框                     |
| inherit | 从父元素继承边框样式               |

### border-width (边框宽度)


| 值                 | 描述                           |
| ------------------ | ------------------------------ |
| thin               | 细的边框                       |
| medium             | 默认；中等的边框               |
| thick              | 粗的边框                       |
| *length* (例：5px) | 自定义边框的宽度               |
| inherit            | 从父元素继承 border-width 的值 |

### border-color (边框颜色)

| 值                 | 描述                           |
| ------------------ | ------------------------------ |
| white              | 规定颜色值为颜色名称的背景颜色     |
| #ffffff            | 规定颜色值为十六进制值的背景颜色   |
| rgb(255, 255, 255) | 规定颜色值为 rgb 代码的背景颜色    |



## Outline（轮廓）

### outline-color (轮廓颜色)

(可选值同 border-color)

### outline-style (轮廓样式)

(可选值同 border-style)

### outline-width (轮廓宽度)

(可选值同 border-width)



## Margin（外边距）和 Padding（内边距）

### margin (外边距)

- margin-bottom
- margin-left
- margin-right
- margin-top

### padding (内边距)

- padding-bottom
- padding-left
- padding-right
- padding-top

| 值                  | 描述                             |
| ------------------- | -------------------------------- |
| auto                | 浏览器计算距离                   |
| *length* (例：50px) | 以具体单位计算的距离             |
| %                   | 基于父元素的宽度的百分比的内边距 |
| inherit             | 从父元素继承属性的值             |

## Display（显示）

| 值                 | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| **none**           | 此元素不会被显示                                             |
| **block**          | 此元素将显示为块级元素，此元素前后会带有换行符               |
| **inline**         | 默认；此元素会被显示为内联元素，元素前后没有换行符           |
| **inline-block**   | 行内块元素                                                   |
| list-item          | 此元素会作为列表显示                                         |
| run-in             | 此元素会根据上下文作为块级元素或内联元素显示                 |
| table              | 此元素会作为块级表格来显示（类似 \<table>），表格前后带有换行符 |
| inline-table       | 此元素会作为内联表格来显示（类似 \<table>），表格前后没有换行符 |
| table-row-group    | 此元素会作为一个或多个行的分组来显示（类似 \<tbody>）        |
| table-header-group | 此元素会作为一个或多个行的分组来显示（类似 \<thead>）        |
| table-footer-group | 此元素会作为一个或多个行的分组来显示（类似 \<tfoot>）        |
| table-row          | 此元素会作为一个表格行显示（类似 \<tr>）                     |
| table-column-group | 此元素会作为一个或多个列的分组来显示（类似 \<colgroup>）     |
| table-column       | 此元素会作为一个单元格列显示（类似 \<col>）                  |
| table-cell         | 此元素会作为一个表格单元格显示（类似 \<td> 和 \<th>）        |
| table-caption      | 此元素会作为一个表格标题显示（类似 \<caption>）              |
| inherit            | 从父元素继承 display 的值                                    |



## Visibility（可见性）

| 值       | 描述                                                         |
| :------- | ------------------------------------------------------------ |
| visible  | 默认值；元素是不可见的                                       |
| hidden   | 元素是不可见的                                               |
| collapse | 当在表格元素中使用时，此值可删除一行或一列，但是它不会影响表格的布局。被行或列占据的空间会留给其他内容使用。如果此值被用在其他的元素上，会呈现为 "hidden" |
| inherit  | 从父元素继承 visibility 的值                                 |



## Position（定位）

| 值       | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| absolute | 生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位 |
| fixed    | 生成绝对定位的元素，相对于浏览器窗口进行定位                 |
| relative | 生成相对定位的元素，相对于其正常位置进行定位                 |
| static   | 默认值；没有定位，元素出现在正常的流中                       |
| inherit  | 从父元素继承 position 的值                                   |



## Float（浮动）

### float (浮动方向)

| 值      | 描述                    |
| ------- | ----------------------- |
| left    | 元素向左浮动            |
| right   | 元素向右浮动            |
| none    | 默认值；元素不浮动      |
| inherit | 从父元素继承 float 的值 |

### clear (清除浮动)

| 值      | 描述                           |
| ------- | ------------------------------ |
| left    | 在左侧不允许浮动元素           |
| right   | 在右侧不允许浮动元素           |
| both    | 在左右两侧不允许浮动元素       |
| none    | 默认值；允许浮动元素出现在两侧 |
| inherit | 从父元素继承 clear 的值        |

