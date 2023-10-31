webSocket是html5开始提供的一种在单个TCP连接上进行全双工通讯的协议
webSocket使的客服端和服务器之间的数据交换变得更加简单，**允许服务端主动向客服端推送数据**，在webSocket API中，**浏览器和服务器只要完成一次连接，两者之间就直接可以创建持久性的连接，并进行双向数据传输**
浏览器通过javascript向服务器发出建立WebSocket连接的请求，连接建立之后，客服端和服务器端就可以通过TCP连接直接交换数据，当你获取Web Socket连接后，你可以通过send()方法来向服务端发送数据，并通过onmessage事件来接收服务器返回的数据
以下API用来创建WebSocket对象
var socket =new WebSocket(url,[protocol]);以上代码的一个参数url，指定连接的URL，第二个参数protocol是可选的，指定了可接受的子协议。
## WebSocket属性
| 属性 | 描述 |
| --- | --- |
| Socket.readyState | 只读属性readyState表示连接状态，
- 0表示连接尚未建立
- 1表示连接已经建立，可以进行通信
- 2表示链接正在进行关闭
- 3表示连接已经关闭或者连接不能打开
 |
| Socket.bufferedAmount | 只读属性bufferedAmount已经被send()放入正在队列中等待传输，但是还没有发出的UTF-8文本字节数 |

## WebSocket事件
| open | Socket.onopen | 连接建立时候触发 |
| --- | --- | --- |
| message | Socket.onmessage | 客服端接收服务端数据时触发 |
| error | Socket.onerror | 通信发生错误时触发 |
| close | Socket.onclose | 连接关闭时触发 |

## WebSocket方法
以下时候WebSocket对象的相关方法，假定我们使用了以上代码创建了Socket对象

| 方法 | 描述 |
| --- | --- |
| Socket.send() | 使用连接发送数据 |
| Socket.close() | 关闭连接 |

为了建立一个WebSocket连接，客服端浏览器首先要向浏览器发起一个HTTP请求，这个请求和通常HTTP请求不同，包含了一些附加的头信息，其中附加的头信息"Upgreade:webSocket"表明这是一个申请协议升级的HTTP请求，服务器端解析这些附加的头信息然后产生应答信息返回给客服端，客服端和服务器端的webSocket连接就建立起来了，双方就可以通过这个连接通道自由的传递信息，并且这个连接会持续到客服端或者服务端的某一方主动关闭连接。
