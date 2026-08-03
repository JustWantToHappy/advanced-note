## JWT（JSON Web Token）
JWT就是一个字符串（身份令牌），三部分组成：header(json对象base64编码).payload(用户信息对象base64编码，密码，身份证，手机号这些敏感信息不要存放在payload，可存用户id，以及角色).signature（前面两部分连接起来之后，通过一个密钥加密得到的字符串经过base64编码）

## JWT对比Cookie
- 分布式系统下，多微服务节点，Session需要Redis同步，JWT只需要共享密钥
- 多端跨域：web/app/第三方 JWT走请求头: Authorization: Bearer <你的JWT>，app以及小程序没有cookie
- 高并发：JWT零存储，服务端存储压力小

## 双token机制
- access token：直接用于接口鉴权，存活时间短，一般几十分钟
- refresh token：只在access token过期后用来换新的access token，一般存活时间一个星期甚至一个月

