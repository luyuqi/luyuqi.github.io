## event loop(事件循环)
* 每个event loop由一个或者多个task组成
* https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/（演示）

### 任务队列
* 宏观任务队列和微观任务队列
* 异步操作有了结果，会加入到任务队列中
* 先执行macrotask,当微观task全部执行完，再执行宏观task

### macrotask
* setTimeout
* setInterval
* setImmediate
* I/O （https://www.cnblogs.com/eric-nirnava/p/IO.html）
* UI/rendering

### microtask
* new Promise()
* new MutaionObserver()

### 浏览器环境下js引擎的事件循环机制
https://zhuanlan.zhihu.com/p/33058983

## BFC与IFC
https://segmentfault.com/a/1190000009545742
### BFC规则
* 内部的Box会在垂直方向，一个接一个地放置。
* Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
* 每个元素的左外边缘（margin-left)， 与包含块的左边（contain box left）相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。除非这个元素自己形成了一个新的BFC。
* BFC的区域不会与float box重叠。
* BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
* 计算BFC的高度时，浮动元素也参与计算

### IFC规则
* 在行内格式化上下文中，框(boxes)一个接一个地水平排列，起点是包含块的顶部。水平方向上的 margin，border 和 padding在框之间得到保留。框在垂直方向上可以以不同的方式对齐：它们的顶部或底部对齐，或根据其中文字的基线对齐。包含那些框的长方形区域，会形成一行，叫做行框。

### 如何形成BFC
* 根元素或其它包含它的元素
* 浮动 (元素的 float 不是 none)
* 绝对定位的元素 (元素具有 position 为 absolute 或 fixed)
* 非块级元素具有 display: inline-block，table-cell, table-caption, flex, inline-flex
* 块级元素具有overflow ，且值不是 visible