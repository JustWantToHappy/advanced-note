## 定义
cookie 设计的初衷就是为了弥补 http 的无状态，帮助记录客户端的用户状态，作为用户登录凭证的载体。

## cookie的组成
- key:键，比如【身份编号】id
- value:值，比如身份编号的值，它可以是任意值
- domain:域，domain指定了哪些主机可以接受cookie,(表示这个cookie属于哪个网站的，)如果不指定，该属性默认给同一个host设置Cookie,不包含子域名，如果指定了Domain,则一般包含子域名，因此，指定Domain比省略它的限制要少。例如：如果要设置Domain=niuma.org,则Cookie也包含在子域中,例如包含在sb.niuma.org
- path:路径(表示这个cookie是属于该网站哪个基路径的)，path属性指定了一个URL路径，该URL路径必须存在于请求中，以便发送给Cookie标头,用于指定哪些路径下的请求可以访问和发送包含该Cookie的信息
- secure:是否使用到安全传输
- expire:过期时间（绝对时间），表示该cookie在什么时候过期
如果一个cookie同时满足如下条件，则这个cookie会被附带到请求中：
- cookie没有过期
- cookie中的域和这次请求的域是匹配的
- cookie中的path和这个请求的path是匹配的
- 验证cookie的安全传输：
	- 如果cookie的secure属性是true,则请求协议必须是https，否则不会发送该cookie
	- 如果cookie的secure属性是false,则请求协议是可以是http，也可以是https
- max-age:设置cookie的相对有效期
- httponly:设置cookie是否仅能用于传输，如果设置了改值，表示该cookie仅能用于传输，而不允许不在客户端通过js获取，这对于防止跨站脚本攻击非常有用
## 如何设置cookie
- 服务器设置cookie，响应头按照如下格式设置set-coookie:cookie1,set-cookie:cookie2，通过这种方式，就可以一次在响应中设置多个cookie，其中每个cookie的格式如下：`键=值; path=?; domain=?; max-age=?; secure; httponly;`
- 客服端自行设置：document.cookie="键=值; path=?; domain=?; max-age=?; secure; httponly;"(可以使用js-Cookie处理cookie)
> 注意：读取document.cookie的时候，是获取不到属性的，只能获取到自定义键值( 属性（HttpOnly、Secure、Domain、Path、Expires 等）：这是 Cookie 的"配置选项"，不会出现在 document.cookie 的返回值里)

## cookie、sessionStorage、localStorage区别
1. cookie兼容性更好，浏览器针对cookie会有一些默认行为，比如响应头设置了set-cookie，浏览器会自动保存cookie的值
2. sessionStorage和localStorage是没有默认行为的，前者用于保存会话级别的数据，后者用于更持久的保存数据
3. cookie的大小是有限制的，一般浏览器同一个域下cookie的总量为4MB，而sessionStorage和localStorage则没有限制
4. cookie会与domain、path关联，而sessionStorage和localStorage只有domain关联