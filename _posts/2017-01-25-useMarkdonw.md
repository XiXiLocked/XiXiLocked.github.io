---
layout: minimal
title: 试试看用markdown
---

现在好像什么都是这个样子的，有一份源文件，然后根据源文件生成一份实际的结果
于是从[这里][cheatsheet]看来了一下常用的记号，这里二手记录一下我觉得有用的。  
~~上传之后发现和github的markdown有不兼容，去找了github的说明发现[看github给的例子本身][githubmarkdown]就很好懂。~~


### 链接和图片
这段都算链接相关的。基本的有两种写法，一是*Inline-style*的，一是*Reference-style*的。  
大概格式都是一样的，只是带**!**的是图片，不带的是普通链接。  
inline的`[]`之后是`()`,引用的`[]`后面是`[]`，`[]: `的不输出到最终的结果里。
下面中文都是可替换内容，`[]()!: <>`都是格式。  


``` markdown

[文本](实际链接)
[文本][引用1]

[引用1]: 实际链接

![可选文本2](图片链接 可选文本1)
![可选文本2][图片引用1]

[图片引用1]: 图片链接 可选文本1   

```

### 代码高亮和引用
功能和效果上相似，语法上没什么看出什么直接关系。  
代码高亮表现上有*span*和*block* 2种，*span*是和文章连在一起的，*block*是另起一段的。
基本是用`` ` ` ``括住*span*的代码，```` ``` ``` ````括住*block*。
但是一个很蛋疼的问题是，怎么在代码里面显示`` ` ` ``和```` ``` ``` ````？escape不能用在这里哦。  
答案是要用更多的`` ` ``来括住更少的`` ` ``，比如要括住`` ` ``就要用``` `` ```,括住``` `` ```就要用```` ``` ````。
这样一来会产生一个例外的情形，就是```` ``` ````有时候不是*block*的，要在前后补上一个换行才是*block*。  
然后在*block*上面能标注语言，这样就能语法高亮了。语言名试了一下要**小写**，有效的语言列表在这里[highlightjs]。  

````markdown

inline `inline`  
block 
```javascript
function foo() {}
```

````

>
inline `inline`  
block 
```javascript
function foo() {}
```


引用就是把`>`放在行首，引用中的`markdown`会生效。

```markdown
>引用的文本
```

>引用的文本


### 标题，粗体，斜体，删除线
标题取H1~H6是在前面打对应个的`#`。  

```markdown

# H1
## H2
### H3
#### H4
##### H5
###### H6

```
>
# H1
>
>
## H2
>
>
### H3
>
>
#### H4
>
>
##### H5
>
>
###### H6

```markdown
_斜体_ *斜体*  
__粗体__ **粗体**  
___粗斜体___ ***粗斜体***  
~~删除线~~
```

>
_斜体_ *斜体*  
__粗体__ **粗体**  
___粗斜体___ ***粗斜体***  
~~删除线~~

### 横线和列表
横线用3个以上相同的`-`, `*`,`_`来表示。因为断行和符号复用的原因，前后都放一个换行，并且多放几个符号不要吝啬只放3个。

```markdown
hyphen -

----------
underscore _

___________
asterisk *

************
```
>
hyphen -
>
----------
underscore _
>
___________
asterisk *
>
************


有序列表前面加`1.`, `2.`之类的序号，并且序号并不要紧。无序列表前面加`*` `-` `+`表示一个个条目。

```markdown
1. 第一
2. 第二
  * 一个条目
  - 又一个条目
  + 又又一个条目
1. 只要是数字就不要紧,第三条
5. 第四条
```

>
1. 第一
2. 第二
  * 一个条目
  - 又一个条目
  + 又又一个条目
1. 只要是数字就不要紧,第三条
5. 第四条

[cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
[highlightjs]: https://highlightjs.org/static/demo/
[githubmarkdown]: https://guides.github.com/features/mastering-markdown/
