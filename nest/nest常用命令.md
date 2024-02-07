## nest常用命令
- nest -h:查看nest提供的常用命令
- --no-spec表示不生成测试文件
- --flat表示平铺，不生成目录
- 创建路由中间件：`nest g middleware log --no-spec --flat`
- 创建路由守卫：`nest g guard login --no-spec --flat
`
- 创建拦截器：`nest g interceptor time --no-spec --flat
`
- 创建管道：`nest g pipe validate --no-spec --flat
`
- 创建过滤器：`nest g filter test --no-spec --flat
`

