## TCP Flow control and the sliding window.

TCP 采用 sliding window 进行流量控制.

TCP sliding window 是如何工作的呢？

TCP sliding window 决定了数据从一个系统发送到另一个系统时，没有ack的bytes数量。

两个因素影响这个 bytes 数量级：
* 发送系统的发送缓冲区（send buffer）
* 接收系统的可用的接收缓冲区（available receive buffer

在接收数据端，TCP 缓存数据在接收缓冲区中，TCP ack 数据接收消息会同步一个新的接收窗口给发送端. 接收窗口(receive window) 表示在 receive buffer 中，还有多少可用空间. 如果 receive buffer 满了，接收端告知发送端 receive window 将设置为0 （表示我满了，你悠着点发），而此时接收端再发送更多数据之前，需要先进行等待.

接收端的 receive window （我们说的可用空间），通常取决于接收方应用从 receive buffer 里读取数据的快慢。TCP 缓存数据在 receive buffer 中，知道应用从中读取。

以下几点说明：

- maximum numbers of unack bytes = min(sender buffer size + receive window size notify sender)

-  当接收应用读数据足够快并能匹配上发送的数据，接收窗口大小接近接收缓冲区. 这样可以证明网络比较顺畅，能够比较高效利用网络带宽。而当接收的应用读取速度足够快，一个较大的接收窗口可以提高性能;

- 当接收缓冲区满了，会收到一个 receive window 为 0 的 ack，发送端必须临时暂停发送更多数据；

- 通常而言，receive window 变为0的次数越多，意味着网络传输速率整体变得很慢。

