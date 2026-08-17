## xss

跨站脚本攻击（恶意脚本（通常是 JavaScript）注入到网页中，当其他用户访问该页面时，浏览器就会执行这些脚本）。本质原因：应用把用户输入的数据直接插入 HTML，而没有进行安全处理

1. 存储型（危害最大），举个例子：评论区输入<script>alert('xss')</script>，数据库保存之后，返回给前端渲染，所有人都可以看到，都会执行这段恶意脚本
2. dom型，漏洞发生在前端 JavaScript，不管服务器的事，JS 直接把 URL 参数写入 DOM。举个例子：URL是`https://example.com/?name=<img src=x onerror=alert(1)>`,js代码是：

```javascript
const name = location.search.split("=")[1];
document.getElementById("msg").innerHTML = name;
```

页面就会渲染图片并执行恶意脚本

3. 反射型，举个例子：恶意脚本 通过 URL 参数提交，服务器返回页面时 原样输出，比如攻击者构造`https://example.com/search?q=<script>alert('XSS')</script>`，服务端返回`<p>搜索内容：<script>alert('XSS')</script></p>`，用户点攻击者伪造的这个链接机会中招

解决方法：

1. 过滤：服务器去掉一些危险的标签，去掉一些危险的属性
2. 编码：服务器对危险的标签进行HTML实体编码，比如<script></script>变成`&lt;script&gt;&lt;script/&gt;`，也可以让前端插入一段文本内容的时候使用textContent(编码后的)而不是innerHTML
3. CSP(内容安全策略)：相当于白名单，限制网页可以加载和执行哪些资源。比如用户中招了，访问了xss攻击的script第三方js，使用csp可以限制执行

### CSP

- 前端设置CSP:

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'" />
<!-- 可以访问 -->
<script src="/app.js"></script>
<!-- 无法访问 -->
<script src="https://evil.com/hack.js"></script>
限制页面只能加载当前域名的 JavaScript。
```

- 服务端设置CSP：在网站主页面xxx/index.html中设置响应头：例如：

```javascript
Content-Security-Policy:
  default-src 'self';
  script-src 'self' https://cdn.jsdelivr.net;
  style-src 'self' 'unsafe-inline';
  img-src 'self' data:;
  connect-src 'self' https://api.example.com;
```

## csrf

跨站请求伪造(攻击者诱导用户在“已登录状态下”向目标网站发送恶意请求,利用浏览器“自动带上 Cookie”的机制)。举个简单的例子，用户登录了银行的网站，这时候突然一个广告弹窗（实际上是攻击者构造的网站），点击之后，执行下面的脚本：因为请求的目标网站是银行，所以会携带上bank的cookie，导致被成功转账

```html
<img src="https://bank.com/transfer?amount=1000&to=attacker" />
```

解决方法

1. csrf token，一次性token，给容易发生csrf攻击且对用户影响大的请求加上，跨站请求不会携带这个token。比如上面的case,用户登录银行转账页面的时候，服务器发送一个csrf token回来，用户点击提交转账的时候同时提交这个token，后续
2. SameSite Cookie,cookie的指令(Set-Cookie: session=xxx; samesite=strict)，现代网站基本都开启，解决的是浏览器要不要自动带上cookie的问题。
	- 如果设置strict,跨域请求不会携带此cookie
	- 如果设置lax，跨站请求是GET（"用户主动点链接"的 GET）会带，不是则不会带
3. 服务器验证 Referer / Origin
4. 二次确认，邮箱验证，手机短信验证码验证等
