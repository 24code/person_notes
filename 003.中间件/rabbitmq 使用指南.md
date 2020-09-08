#rabbitmq 使用指南
## 教程
1. [王磊RabbitMQ系列](https://www.cnblogs.com/vipstone/category/1236196.html)
2. [朱小厮](https://blog.csdn.net/u013256816/article/cate1gory/6532725)
3. [消息中间件总结](https://blog.csdn.net/u013256816/article/details/54743481)

## 原理
1. [AMQP模型](http://rabbitmq.mr-ping.com/AMQP/AMQP_0-9-1_Model_Explained.html)
   1. ![模型](https://www.rabbitmq.com/img/tutorials/intro/hello-world-example-routing.png)
   2. 交换机(exchange)
      1. direct 默认,message 根据 queue name直接投递
      2. fanout 广播到所有绑定的queue,用于 公告同步,全局广播
      3. topic 根据模式匹配,投递到对应的queue
      4. header,和topic类似,基本可替代.
      5. dead letter exchange,通过设置 queue 或者 message 延时, binding 对应 queue,达到延时投递
   3. 队列(Queue)
      1. Name 队列名称
      2. Durable（消息代理重启后，队列依旧存在）
      3. Exclusive（只被一个连接（connection）使用，而且当连接关闭后队列即被删除）
      4. Auto-delete（当最后一个消费者退订后即被删除）
      5. Arguments（一些消息代理用他来完成类似与TTL的某些额外功能）
      6. 以"amq."开始的队列名称被预留做消息代理内部使用
   4. 绑定(binding)
      1. 如果AMQP的消息无法路由到队列（例如，发送到的交换机没有绑定队列），消息会被就地销毁或者返还给发布者。如何处理取决于发布者设置的消息属性
   5. 消息(message)
      1. AMQP模型中的消息（Message）对象是带有属性（Attributes）的,大多数是开放给接收它们的应用解释器用的
         - Content type（内容类型）
         - Content encoding（内容编码）
         - Routing key（路由键）
         - Delivery mode (persistent or not)
         - 投递模式（持久化 或 非持久化）
         - Message priority（消息优先权）
         - Message publishing timestamp（消息发布的时间戳）
         - Expiration period（消息有效期）
         - Publisher application id（发布应用的ID）
      2. 消息体(body),publisher 发送的内容,可以为空
   6. 消费者(consumer)
      1. push api(推送) 和 pull api(拉取)
      2. 消息确认(ack),主动确认(manual),自动确认(auto ack)
         - 如果一个消费者在尚未发送确认回执的情况下挂掉了，那AMQP代理会将消息重新投递给另一个消费者。如果当时没有可用的消费者了，消息代理会死等下一个注册到此队列的消费者，然后再次尝试投递
         - 一般在client端建议全局捕获异常,遇到消费错误,重新推入错误队列进行容错性处理
      3. 拒绝消息
         1. 当拒绝某条消息时，应用可以告诉消息代理如何处理这条消息——销毁它或者重新放入队列。当此队列只有一个消费者时，请确认不要由于拒绝消息并且选择了重新放入队列的行为而引起消息在同一个消费者身上无限循环的情况发生
      4. 预取消息,明确指定在收到下一个确认回执前每个消费者一次可以接受多少条消息是非常有用的,提升I/O,负载均衡.
   7. 虚拟主机(virtual host)
      1. exchange,queue,user,user group 完全隔离
      2. 支持多租户模型,一台服务器多个virtual host
   8. 连接,信道(channel)
      1. 基于TCP连接的通道复用,本质就是在一个TCP连接中定义多个channel
      2. 在涉及多线程/进程的应用中，为每个线程/进程开启一个通道（channel）是很常见的，并且这些通道不能被线程/进程共享
      3. 一个特定通道上的通讯与其他通道上的通讯是完全隔离的，因此每个AMQP方法都需要携带一个通道号，这样客户端就可以指定此方法是为哪个通道准备的
2. [消息持久化原理](https://blog.csdn.net/u013256816/article/details/60875666)
3. [消息确认,事务原理](https://blog.csdn.net/u013256816/article/details/55515234)
4. [消息可靠性保证](https://blog.csdn.net/u013256816/article/details/79147591)
## 场景
1. 多业务耦合场景
2. 订单计时场景
## 特性
1. exchange 类型
2. dead letter exchange(dlx)/延迟队列
3. [集群]()
## 实战
1. [技术选型,kafka 和 rabbitmq 对比](https://blog.csdn.net/u013256816/article/details/79838428)
2. [rabbitmq 监控]
