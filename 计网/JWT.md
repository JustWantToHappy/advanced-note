## JWT（JSON Web Token）
JWT就是一个字符串（身份令牌），三部分组成：header(json对象base64编码,记录了整个令牌的类型和签名算法).payload(用户信息对象base64编码，密码，身份证，手机号这些敏感信息不要存放在payload，可存用户id，以及角色).signature（前面两部分连接起来之后，按照头部固定的签名算法对整个令牌进行签名，带密钥的hash加密得到的字符串经过base64编码）。这部分主要用来验证是否被篡改，下次服务端接收到jwt，利用签名算法以及header+payload重新计算，是否和signature匹配。
### header
```javascript
{
	"alg":"HS256",
	"type":"JWT"
}
```
### payload
```javascript
{
	"exp":"到期时间",
	"jti":"jwt唯一编号",
	//...以及一些自定义信息
}
```

## JWT对比Cookie
- 分布式系统下，多微服务节点，Session需要Redis同步，JWT只需要共享密钥
- 多端跨域：web/app/第三方 JWT走请求头: Authorization: Bearer <你的JWT>，app以及小程序没有cookie
- 高并发：JWT零存储，服务端存储压力小

## 双token机制
- access token：直接用于接口鉴权，存活时间短，一般几十分钟
- refresh token：只在access token过期后用来换新的access token，一般存活时间一个星期甚至一个月
登录之后每次用户访问接口，携带access token，服务端判断token是否过期：如果过期，则响应401，客户端拦截响应后请求刷新access token的请求，请求参数是refresh token，如果refresh token没过期：服务端就会返回新的access token，客户端重新请求失败的业务接口。否则抛出401错误或者让用户页面重定向到登录界面。（refresh token一般存放在httpOnly的cookie中,access token只存放在内存中）
```javascript
	instance.interceptors.response.use(null, async err => {
		if (err.response?.status === 401 && !err.config._retried) {
			const { accessToken } = await refreshToken(); // 用 refresh token
			err.config._retried = true;
			err.config.headers.Authorization = `Bearer ${accessToken}`;
			return instance(err.config); // 重发原请求
		}
		return Promise.reject(err);
	});
```