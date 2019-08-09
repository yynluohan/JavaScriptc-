# HTML5新特性

## 目录

   1. [拖放(drag/drop)](#href1)
   2. [正则表达式](#href2)
   3. [语义标签](#href3)



### <a name="href1">拖放(drag/drop)</a>

html5为元素添加了可拖拽的属性 `draggable`,这个属性决定元素是否能被拖拽。如果 draggable="true"，
则表示元素可以被拖拽，反之则不能。

```
<div draggable="true">drag me</div>
```


### <a name="href2">正则表达式</a>

html5加入了 `pattern`属性，属性值为正则表达式，可以检验电话、邮箱等格式。

```
<input pattern="[^ @]*@[^ @]*"/>
```


### <a name="href3">语义标签</a>

```
标签	                           描述

<header></header>	         定义了文档的头部区域
<footer></footer>	         定义了文档的尾部区域
<nav></nav>	               定义文档的导航
<section></section>	       定义文档中的节（section、区段）
<article></article>	       定义页面独立的内容区域
<aside></aside>	           定义页面的侧边栏内容
<detailes></detailes>	     用于描述文档或文档某个部分的细节
<summary></summary>	       标签包含 details 元素的标题
<dialog></dialog>	         定义对话框，比如提示框
```
