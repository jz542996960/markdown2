### epoll

- `epoll_create1`: 创建一个epoll实例，文件描述符
- `epoll_ctl`: 将监听的文件描述符添加到epoll实例中，实例代码为将标准输入文件描述符添加到epoll中
- `epoll_wait`: 等待epoll事件从epoll实例中发生， 并返回事件以及对应文件描述符l



## 边沿触发vs水平触发

`epoll`事件有两种模型，边沿触发：edge-triggered (ET)， 水平触发：level-triggered (LT)

**水平触发(level-triggered)**

- socket接收缓冲区不为空 有数据可读 读事件一直触发
- socket发送缓冲区不满 可以继续写入数据 写事件一直触发

**边沿触发(edge-triggered)**

- socket的接收缓冲区状态变化时触发读事件，即空的接收缓冲区刚接收到数据时触发读事件
- socket的发送缓冲区状态变化时触发写事件，即满的缓冲区刚空出空间时触发读事件



