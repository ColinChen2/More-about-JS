## 目标：
1. 研究事件的定位，捕获，冒泡。
2. 时间循环和事件流的合作机制。

## 问题
1. 网景公司和IE的事件流模型，捕获和冒泡。
2. 鼠标点击怎么定位的呢，什么时候确定的？
3. e.target 在捕获的时候就已经得到，做个试验。
4. event dispatch and event flow. 是怎么和 event loop(scripting) 合作的

## 解决方案

### 查看W3C官方文档确认。
1. uievents: event dispatch and event flow.
2. html5-webappapis: event loop.

### 解答
1. 网景公司用捕获，IE用冒泡，最后W3C标准为先捕获再冒泡，默认冒泡阶段回调。
2. 当鼠标点击，根据鼠标的位置信息创建出MouseEvent.最后的target将用一些算法在dispatch之前确定出targetEvent。
3. 见上面的例子，[domEvent.html](domEvent.html).
4. 他们需要一起合作，比如鼠标点击。整个过程是鼠标点击-》产出mouse event -》task queue in event loop -》当空闲时候，处理event，task queue dispatch event e.target这时候就已经存在，就是谁dispatch的-》event flow，捕获，直到找到目标，冒泡-》回调。

## 常见问答：
Q.events loop 和 task queue的关系？
A.events loop has many task queues.

Q. 点击鼠标，产生task到task queue in event loops, 那task是不是一个event，如mourseEvent？
A. 是的，task只能包含特定的几种类型（Events，Parsing，Callbacks，Using a resource，Reacting to DOM manipulation），其中一个就是task。

一个很好的例子，[mdn event](https://developer.mozilla.org/zh-CN/docs/Web/API/MouseEvent)

## 参考文档：
1. [event loops](https://www.w3.org/TR/html5/webappapis.html#task-queue)
2. [event flow](https://www.w3.org/TR/uievents/#event-flow)
