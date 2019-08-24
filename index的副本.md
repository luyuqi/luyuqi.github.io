https://www.zhihu.com/question/19739907

## event loop(事件循环)
* 每个event loop由一个或者多个task组成
* https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/（演示）

### 任务队列
* 任务队列（宏观）和微观任务队列
* 异步操作有了结果，会加入到任务队列中
* 当微观task全部执行完，再执行宏观task
* 一次事件循环只会在任务队列中（mac）提取一个方法

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
https://github.com/ccforward/cc/issues/48
https://juejin.im/entry/58d4df3b5c497d0057eb99ff
http://v.youku.com/v_show/id_XODA0MDYyNTcy.html

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

##  浏览器将rem转成px时有精度误差
http://taobaofed.org/blog/2015/11/04/mobile-rem-problem/

##  you need to know css
https://lhammer.cn/You-need-to-know-css/#/

## JavaScript 浮点数陷阱及解法
### sign(1)   exponent(11)  mantissa(52)
 http://www.binaryconvert.com/convert_double.html
 https://github.com/camsong/blog/issues/9 (浮点数)
 
 
##内联首屏关键CSS（Critical CSS）
###  https://juejin.im/post/5b6133a351882519d346853f

* 内联首屏显示关键CSS
* 异步加载CSS  meida  rel  js控制
* 压缩代码  
* 去除无用的css代码
* 加载性能的优化  文件体积  并发请求  异步  不阻塞
* 选择器的优化 从右往左  
* 渲染的优化  text-shadow box-shadow
* 可维护性  命名规范bem  block  element   Modifiers

##浏览器利用GPU来加速页面渲染  CSS3 动画优化
###主线程
* Javascript的执行
* CSS样式计算
* 计算Layout
* 将页面元素绘制成位图（paint）
* 发送位图给合成线程
###合成线程
* 将位图发送给GPU
* 计算页面的可见部分和即将可见部分（滚动）
* 通知GPU绘制位图到屏幕上（draw）
* http://zencode.in/14.CSS%E5%8A%A8%E7%94%BB%E7%9A%84%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96.html

##  https://mp.weixin.qq.com/s/C2Zx3KPNPkgj-aHnOY43Iw（Web性能优化地图）


## https://hit-alibaba.github.io/interview/basic/network/HTTP.html

## HTTP 协议
### 状态行 请求头 消息主体
* get post put delete 
* 200 客户端请求成功
* 301 请求永久重定向
* 302 请求暂时重定向
* 304 文件未修改  用缓存文件
* 400 客户端请求语法错误  服务器无法理解
* 401 未授权
* 403 服务器收到请求 拒绝提供服务
* 404 路径没有找到
* 500 服务器错误
* 503 服务器当前不能处理客户端的请求  一段时间后可能恢复正常

## TCP 协议
###三次握手
#### 所谓三次握手(Three-way Handshake)，是指建立一个 TCP 连接时，需要客户端和服务器总共发送3个包。
* 第一次握手(SYN=1, seq=x):

```
客户端发送一个 TCP 的 SYN 标志位置1的包，指明客户端打算连接的服务器的端口，
以及初始序号 X,保存在包头的序列号(Sequence Number)字段里。
发送完毕后，客户端进入 SYN_SEND 状态。
```
* 第二次握手(SYN=1, ACK=1, seq=y, ACKnum=x+1)

```
服务器发回确认包(ACK)应答。即 SYN 标志位和 ACK 标志位均为1。
服务器端选择自己 ISN 序列号，放到 Seq 域里，同时将确认序号(Acknowledgement Number)设置为客户的 ISN 加1，即X+1。 
发送完毕后，服务器端进入 SYN_RCVD 状态。
```
* 第三次握手(ACK=1，ACKnum=y+1)

```
客户端再次发送确认包(ACK)，SYN 标志位为0，ACK 标志位为1，
并且把服务器发来 ACK 的序号字段+1，放在确定字段中发送给对方，并且在数据段放写ISN的+1
发送完毕后，客户端进入 ESTABLISHED 状态，
当服务器端接收到这个包时，也进入 ESTABLISHED 状态，TCP 握手结束。
```

###  四次挥手
* 第一次挥手(FIN=1，seq=x)

```
假设客户端想要关闭连接，客户端发送一个 FIN 标志位置为1的包，
表示自己已经没有数据可以发送了，但是仍然可以接受数据。
发送完毕后，客户端进入 FIN_WAIT_1 状态。
```

* 第二次挥手(ACK=1，ACKnum=x+1)

```
服务器端确认客户端的 FIN 包，发送一个确认包，
表明自己接受到了客户端关闭连接的请求，但还没有准备好关闭连接。
发送完毕后，服务器端进入 CLOSE_WAIT 状态，客户端接收到这个确认包之后，进入 FIN_WAIT_2 状态，等待服务器端关闭连接。
```

* 第三次挥手(FIN=1，seq=y)

```
服务器端准备好关闭连接时，向客户端发送结束连接请求，FIN 置为1。
发送完毕后，服务器端进入 LAST_ACK 状态，等待来自客户端的最后一个ACK。
```

* 第四次挥手(ACK=1，ACKnum=y+1)

```
客户端接收到来自服务器端的关闭请求，发送一个确认包，并进入 TIME_WAIT状态，
等待可能出现的要求重传的 ACK 包。
服务器端接收到这个确认包之后，关闭连接，进入 CLOSED 状态。
客户端等待了某个固定时间（两个最大段生命周期，2MSL，2 Maximum Segment Lifetime）之后，
没有收到服务器端的 ACK ，认为服务器端已经正常关闭连接，
于是自己也关闭连接，进入 CLOSED 状态。
```

### SYN 攻击

```
攻击客户端在短时间内伪造大量不存在的IP地址，
向服务器不断地发送SYN包，服务器回复确认包，并等待客户的确认。
由于源地址是不存在的，服务器需要不断的重发直至超时，
这些伪造的SYN包将长时间占用未连接队列，正常的SYN请求被丢弃，
导致目标系统运行缓慢，严重者会引起网络堵塞甚至系统瘫痪。
```

## UDP 是一个简单的传输层协议
* UDP 缺乏可靠性。UDP 本身不提供确认，序列号，超时重传等机制。UDP 数据报可能在网络中被复制，被重新排序。即 UDP 不保证数据报会到达其最终目的地，也不保证各个数据报的先后顺序，也不保证每个数据报只到达一次

* UDP 数据报是有长度的。每个 UDP 数据报都有长度，如果一个数据报正确地到达目的地，那么该数据报的长度将随数据一起传递给接收方。而 TCP 是一个字节流协议，没有任何（协议上的）记录边界。

* UDP 是无连接的。UDP 客户和服务器之前不必存在长期的关系。UDP 发送数据报之前也不需要经过握手创建连接的过程。

* UDP 支持多播和广播。