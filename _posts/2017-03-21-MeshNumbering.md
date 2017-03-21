---
layout: minimal
title: 抄来一个BezierPatch生成mesh的编号策略
---

在看Bezier curve, surface相关的一些东西，结论又是没有魔法。
虽然说Bezier造型光滑，各种好处，但是落到渲染，是没有好用的魔法给你用的，还是要生成mesh走老的流程。
然后偷懒卡在一个地方，可以用控制点生成各种中间点，但是怎么编号我是不想操作的，然后 [这里][numbering]正好有一份代码做了这么一件事，的得哪天需要再想一遍，正好拿来记下。

Bezier patch，有的地方也叫Bezier surface，作为输入，一般是4x4一共16个有顺序的控制点。
Mesh，作为输出，基本组成是2个数组，一个是vertice数组，一个是index数组。每个vertex的数据，基本会有position, uv, normal, color等等。第二个部分是index,就是一个整数数组，负责描述哪几个点组成一个三角形，每3个index组成一个三角形。

实际的过程是这样的，通过Bezier patch的控制点，通过B曲线插值得到需要的中间点，这些可以作为vertices直接放进mesh，最后给出一个index数组把三角形拼起来。


上面已经有代码了所以这里用图片说明，然后代码是用的3x3的控制点所以这里也是3x3的，道理是一样的而且3x3的好画一点。
首先是输入，有初始控制点和编号：  
![](/img/Bezier/bezier0.png)


然后是跳着原始编号地插值，得到中间控制点：  
![](/img/Bezier/bezier1.png)


接着另一个方向插值，得到所有的插值点。  
![](/img/Bezier/bezier2.png)


结果编号就是这个样子的，逗号后面的数字是原来的编号：  
![](/img/Bezier/bezier3.png)

最后index数组连三角形，看这张图：  
![](/img/Bezier/bezier4.png)


一共有3种模式，在一行的开始描一个三角形，在一行的结尾描一个三角形，和其他中间的一次出2个三角形。  
上面原文里的做法，~~并不是和原文一样，原文是把四边形分成左上和右下，这里的示意图都是左下和右上~~其实可以合并成一种，一次一个框，并没有觉得哪里不妥。  
![](/img/Bezier/bezier5.png)

[numbering]: https://gist.github.com/mikezila/6912950