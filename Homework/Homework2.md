# Homework2

## 1.

(1)错。

(2)对。HTTP/1.1引入了持续连接，允许在同一TCP连接上发送多个HTTP请求和响应。

(3)错。在非持续连接（HTTP/1.0 默认）中，每个请求/响应对都需要一个新的TCP连接，因此一个TCP报文段不能携带两个HTTP请求。

(4)错。HTTP 响应报文中的 "Date:" 首部表示消息是何时被发送的。表示资源最后修改时间的是 "Last-Modified:" 首部。

(5)错。有些HTTP响应（例如204 No Content）确实没有响应体。

## 3.

DNS，TCP，UDP

服务器IP地址最初不知道，所以先要通过DNS将主机名转换为IP地址，即应用层需要DNS和HTTP协议；

DNS的运输协议为UDP，HTTP的运输层协议为TCP。

## 7.

**计算从点击超链接到接收对象的总时间**:

1. **DNS查询时间**:
   如果主机从DNS得到IP地址之前已经访问了n个DNS服务器，并且相继产生的$RTT$依次为$ (RTT_1, RTT_2, ... RTT_n)$，那么DNS查询的总时间可以使用求和符号来表示。

   $DNS_{\text{total}} = \sum_{i=1}^{n} RTT_i$
   
2. **TCP连接建立**:
   从客户端到服务器的一个RTT时间。对于TCP三次握手，需要一个完整的RTT。

3. **HTTP请求和响应时间**:
   客户端发送HTTP请求并从服务器接收HTTP响应的时间，即一个RTT。

因此，从客户点击超链接到它接收到对象的总时间为：

$Total_{\text{time}} = DNS_{\text{total}} + 2 \times RTT_0= \sum_{i=1}^{n} RTT_i+2RTT_0$

其中，$RTT_0$ 是本地主机和包含对象的服务器之间的RTT值。

## 8.

a.相当于是第七题多了8个$2RTT_0$

$Total_{\text{time}} = DNS_{\text{total}} + 2RTT_0+8\times2 \times RTT_0= \sum_{i=1}^{n} RTT_i+18RTT_0$

b.5个HTTP并行连接

$Total_{\text{time}} = DNS_{\text{total}} + 2RTT_0+2\times2 \times RTT_0= \sum_{i=1}^{n} RTT_i+6RTT_0$

c.持续HTTP，多增加一个RTT

$Total_{\text{time}} = DNS_{\text{total}} + 2RTT_0+ \times RTT_0= \sum_{i=1}^{n} RTT_i+3RTT_0$

## 9.

a.发送大小为L的一个目标通过一个链接的时间是$\frac{L}{R}$。

平均时间是R除以对象的平均大小：$\Delta=\frac{(850,000 bits)} { (15,000,000 bits}s) = 0.0567 s $

链路上的流量强度由 $\beta\Delta = 16\times0.0567 = 0.907$给出。因此，平均接入延迟是 $\frac{0.0567 } {(1 - 0.907)} ≈ 0.61s$。

因此，总的平均响应时间是 $0.61 + 3 = 3.61秒。$

b.

因为命中率为0.4即40%可以通过缓存器立即响应，

故平均响应时间为 $\frac{850000 \text{bit}}{100\text{Mbps}} = 0.0085s$

有60%未命中，此时 $\beta = 16 \times 0.6 = 9.6 请求/s$

平均接入时延$=\frac{\Delta}{1-\Delta\beta} = \frac{0.0567}{1-0.0567 \times 9.6} = 0.1244s$

总响应时间 $= 0.0085 \times 0.4 + (0.1244 + 3) \times 0.6 = 1.878s$