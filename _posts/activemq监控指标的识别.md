<!-- TOC -->

- 1. 分类
    - 1.1. broker本身
    - 1.2. 监控队列
    - 1.3. 监控主题：
    - 1.4. 监控订阅者：

<!-- /TOC -->

# 指标

## 1. 分类

### 1.1. broker本身
&#160; &#160; &#160; &#160;ActiveMQ有3个重要的参数，存储空间百分比，内存空间百分比和临时空间百分比。这三个参数的意义很明显，如果值到了100，则表明硬件空间已满，Broker不能再接受任何的消息了，除非有消息消费并且删除，Broker才可以再接收消息。
如果这些值长时间都比较高，接近阀值，则表示硬件的配置不能满足要求，建议更换硬件，或者给予ActiveMQ的环境配置比较小，建议给予更多的资源给ActiveMQ。
如果平时保持在一个稳定值，有一段时间突然增高，则有两种可能。一种可能是用户量大增（当然大家都希望是这样），另一种可能是某个或者某几个消息消费者死机了。需要人工干预重启。还有一种可能是平时保持在一个稳定值，但是一段时间内突然降低了，则表示消息的生产者可能出现问题了。

### 1.2. 监控队列
&#160; &#160; &#160; &#160;如果ActiveMQ使用队列，需要监控队列的未消费消息数量，消费者数量，消息入队和出队的数量。
未消费消息数量的含义和监控硬件的内存和硬盘空间差不多，过多的消息堆积可能是有消息消费者死机。
消费者数量应该是一个相对固定的值，这个值减少，就直接表示有的消费者已经死机。
消息入队和出队数量如果增长缓慢或者不增长，则表示消息发送者已经死机。一般是通过增量监控。

### 1.3. 监控主题：
&#160; &#160; &#160; &#160;如果ActiveMQ使用主题，需要监控的内容和队列相似，但是没有未消费的消息数量。这里指的注意的是，ActiveMQ提供AdvisoryMessage，用于帮助使用统计一些额外信息，详细情况在后面介绍。

### 1.4. 监控订阅者：
&#160; &#160; &#160; &#160;同样，如果ActiveMQ使用主题，订阅者的信息就十分重要。需要监控已经下线的订阅者。介绍完需要监控的内容，下面介绍一下ActiveMQ提供的几种监控方法。