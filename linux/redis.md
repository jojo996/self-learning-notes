https://zhuanlan.zhihu.com/p/222697530

key-value非关系型内存数据库

Redis不仅仅支持简单的key-value类型的数据，同时还提供String，list，set，zset，hash等数据结构的存储。

token生成、session共享、分布式锁、自增id、验证码

1.IO多路复用的封装

epoll原理：epoll的核心是一个eventloop对象，它就是内核的一个文件描述符中，epfd，其中核心是监视列表和就绪队列，每次向其中添加关注的文件描述符，内核来监听他们的读写情况，有io就加入到就绪队列中，然后主程序通过调用epoll_wait()来获得就绪队列，如果就绪队列中有值就返回，没有就把这个进程相当于阻塞到这个epfd下，等到就绪队列有值再唤醒

异步阻塞io

reactor设计模式

## redis的过期策略以及内存淘汰机制

**定期删除+惰性删除策略**

定期检查，抽查删除

访问时判断是否过期

内存淘汰机制，移除最近最少使用的key

## 如何应对缓存穿透和缓存雪崩问题

缓存穿透：

访问数据库采用互斥锁

异步更新，单独开一个线程更新过期缓存

拦截不合理请求

缓存雪崩：

缓存同一时间大面积失效，导致请求都去往数据库，数据库异常

1. 随机化失效时间，避免集体失效
2. 访问数据库互斥锁
3. 双缓存，一个正常失效时间，另一个没有失效时间

## redis持久化

https://www.jianshu.com/p/bedec93e5a7b

### RDB持久化

RDB持久化产生的RDB文件是一个**经过压缩**的二进制文件，这个文件被保存在硬盘中，redis可以通过这个文件还原数据库当时的状态。

`SAVE`：阻塞redis的**服务器进程**，直到`RDB文件`被创建完毕。

`BGSAVE`：派生(fork)一个子进程来创建新的`RDB文件`，记录接收到`BGSAVE`当时的数据库状态，父进程继续处理接收到的命令，子进程完成文件的创建之后，会**发送信号**给父进程，而与此同时，父进程处理命令的同时，通过**轮询**来接收子进程的信号。

### AOF持久化

AOF持久化是通过保存Redis服务器锁执行的写状态来记录数据库的。

AOF持久化是备份数据库接收到的**命令**，所有被写入AOF的命令都是以redis的协议格式来保存的。

