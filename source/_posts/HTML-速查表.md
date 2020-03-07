---
title: HTML 速查表
date: 2019-11-29 00:31:56
categories: [Dev, HTML]
tags:
    - HTML
toc: true
---
<!-- more -->
## 文本

```html
<h1>一级标题</h1>
<h2>二级标题</h1>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>

<p>段落</p>

<br> （换行）
<hr> （水平线）
```

## 格式化

```html
<b>粗体文本</b>
<code>计算机代码</code>
<em>强调文本</em>
<i>斜体文本</i>
<kbd>键盘输入</kbd> 
<pre>预格式化文本</pre>
<small>更小的文本</small>
<strong>重要的文本</strong>
 
<abbr> （缩写）
<address> （联系信息）
<bdo> （文字方向）
<blockquote> （从另一个源引用的部分）
<cite> （工作的名称）
<del> （删除的文本）
<ins> （插入的文本）
<sub> （下标文本）
<sup> （上标文本）
```

## 实体

| 显示结果 | 描述     | 实体名称 |
| -------- | -------- | -------- |
|          | 空格     | \&nbsp;  |
| &        | 与       | \&amp;   |
| ©        | 版权     | \&copy;  |
| ®        | 注册商标 | \&reg;   |
| ™        | 商标     | \&trade; |

## 链接

```html
普通的链接：<a href="链接地址">链接文本</a>
图像链接： <a href="http://www.example.com/"><img src="URL" alt="替换文本"></a> 
邮件链接： <a href="mailto:abc@example.com">发送e-mail</a>
书签： <a id="tips">
提示部分</a> <a href="#tips">跳到提示部分</a>
```

## 图片

```html
<img src="URL" alt="替换文本" height="42" width="42">
```

## 区块

```html
<div>文档中的块级元素</div>
<span>文档中的内联元素</span>
```

## 列表

```html
<!-- 无序列表 -->
<ul>
	<li>项目</li>
  <li>项目</li>
</ul>

<!-- 有序列表 -->
<ol>
  <li>第一项</li>
  <li>第二项</li>
</ol>

<!-- 定义列表 -->
<dl>
  <dt>项目一</dt>
  	<dd>描述项目一</dd>
  <dt>项目二</dt>
  	<dd>描述项目二</dd>
</dl>
```

## 框架

```html
<iframe src="example.html"></iframe>
```

## 表格

```html
<table>
  <thead>
    <tr>
      <th>表格标题A</th>
      <th>表格标题B</th>
      <th>表格标题C</th>
   </tr>
  </thead>
	<tbody>
   <tr>
     <td>表格内容A</td>
     <td>表格内容B</td>
     <td>表格内容C</td>
   </tr>
  </tbody>
 </table>
```

## 表单

```html
<form action="demo_form.php" method="post/get">

<input type="text" name="email" size="40" maxlength="50"> 
<input type="password"> 
<input type="checkbox" checked="checked"> 
<input type="radio" checked="checked"> 
<input type="submit" value="Send"> 
<input type="reset"> 
<input type="hidden"> 

<select> 
<option>iPad</option> 
<option selected="selected">iPhone</option> 
<option>iPod</option> 
</select>

<textarea name="comment" rows="60" cols="20">
</textarea> 
</form>
```