- [OSI七层模型](#osi七层模型)
- [TCP/IP](#tcpip)
- [TCP VS UDP](#tcp-vs-udp)
- [TCP“三次握手，四次挥手”](#tcp三次握手四次挥手)
- [HTTP](#http)

# OSI七层模型
<img src="https://static.runoob.com/images/mix/v2-854e3df8ea850c977c30cb1deb1f64db_r.jpg" alt="OSI七层模型">

|    名称    |   数据格式   |                   作用                   |     常见协议/设备      |
| :--------: | :----------: | :--------------------------------------: | :--------------------: |
|   应用层   |     N/A      |               控制应用程序               |    ssh HTTP ftp DNS    |
|   表示层   |     N/A      |         格式化数据，比如提供加密         | ASCII JPEG MP4 AVI PNG |
|   会话层   |     N/A      |    控制会话，建立管理终止应用程序会话    |    SQL AHP PHP JSP     |
|   传输层   | fragment(段) | 提供可靠和尽力而为的传输,维护端到端通信  |        TCP UDP         |
|   网络层   | package(包)  |             路由选择与IP寻址             | IP BGP RIP OSPF 路由器 |
| 数据链路层 |  frame(帧)   | 定义如何格式化数据(帧定界)，支持错误检测 |         交换机         |
|   物理层   | bit(比特流)  |          定义物理传输媒介的信息          |   IEEE802 HUB集线器    |

---

# TCP/IP
* Transmission Control Protocol / Internet Protocol
* 在 TCP/IP 中包含一系列用于处理数据通信的协议：
    * TCP (传输控制协议) - 应用程序之间通信，<u>负责在发送时将数据分解为IP包，在接收时组合IP包</u>
    * UDP (用户数据报协议) - 应用程序之间的简单通信
    * IP (网际协议) - 计算机之间的通信
    * ICMP (因特网消息控制协议) - 针对错误和状态
    * DHCP (动态主机配置协议) - 针对动态寻址
* IP协议是**无连接**的
* TCP是<u>全双工</u>，因为收发双方都设有缓冲区

---

# TCP VS UDP
|          |                UDP                 |               TCP               |
| :------: | :--------------------------------: | :-----------------------------: |
| 是否连接 |               无连接               | 有连接，通过<u>三次握手</u>建立 |
| 是否可靠 |               不可靠               |     可靠，流量控制+拥塞控制     |
|  连接数  | 一对一，一对多，多对一，多对对均可 |        端到端（一对一）         |
| 传输方式 |              面向报文              |             面向流              |
| 首部开销 |           开销小，8字节            |        [20字节, 60字节]         |
| 使用场景 |      实时，如视频、通话、直播      |      可靠传输，如文件传输       |

---

# TCP“三次握手，四次挥手”
<img src="https://user-gold-cdn.xitu.io/2020/6/18/172c75a35e9eaa10?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="三次握手" width="400px"><img src="https://user-gold-cdn.xitu.io/2020/6/19/172c82ec6d39b466?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" alt="四次挥手" width="400px">

---

# HTTP
* HyperText Transfer Protocol，超文本传输协议，基于TCP/IP
* HTTP特点
  * HTTP是**无连接**：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
  * HTTP是**媒体独立**的：这意味着，只要客户端和服务器知道如何处理的数据内容，任何类型的数据都可以通过HTTP发送。客户端以及服务器指定使用适合的MIME-type内容类型。
  * HTTP是**无状态**：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。
* Uniform Resource Identifiers, URI
* 请求(Request)包含四个内容：请求行(request line)、请求头部(request header)、空行以及请求内容(request body)
* 响应(Response)也由四个部分组成，分别是：状态行、消息报头、空行和响应正文。
* 状态码
> 分类 | 描述
> :---: | :---:
> 1xx | 请求继续执行
> 2xx | 成功
> 3xx | 重定向
> 4xx | 客户端出错
> 5xx | 服务器出错
* HTTP VS HTTPS
> 可以把HTTPS理解为HTTP+SSL，即带有**加密传输**和**可靠性检测**的HTTP协议
* `POST` vs `GET`
> 1. 浏览器用`GET`请求来获取一个html页面/图片/css/js等资源；用`POST`来提交一个`<form>`表单，并得到一个结果的网页
> 2. `GET`通过TCP直接把header+body组合成一个TCP包一起发出；而`POST`先发送header，服务器返回100后再发送body，即有两个TCP包
> 3. 使用`GET`会将各种参数包含在url中，如`www.google.com/search?q=xxx`;而`POST`会将参数包含在表单里，更加安全，如`www.google.com`
> 4. `GET`可以反复执行，而`POST`会再次提交表单（浏览器可能弹出alert('刷新后需要重新提交表单')) 
> 5. `GET`可以bookmark，而`POST`不行，因为每次`POST`都是不幂等的
> 6. `GET`请求参数会被完整保留在浏览器历史记录里，而`POST`中的参数不会被保留
> 7. `GET`请求在URL中传送的参数是有长度限制的，而`POST`没有
> 8. `GET`请求会被浏览器主动cache，而`POST`不会
> 9. `GET`请求只能进行url编码，而`POST`支持多种编码方式

---