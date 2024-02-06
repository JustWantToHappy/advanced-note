## 注入provide类
```typescript
@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
```
以上是简写方式，如下是全写
```typescript
@Module({
	imports: [],
	controllers: [AppController],
	providers: [
		{
            //provide表示指定的token，当然也可以是字符串
			provide: AppService,
            //指定要注入的对象的类
			useClass: AppService,
		},
	],
})
```
如果token是字符串，注入的时候需要用@Inject手动指定对象的token了:
```typescript
export class AppController {
	constructor(
		@Inject(Provider_Token.APP_SERVICE) private readonly appService: AppService,
	) {}
}
```

## 注入provide值
```typescript
{
    provide: 'person',
    useValue: {
        name: 'aaa',
        age: 20
    }
}
//使用
@Inject('person') private readonly person: any,
```
动态提供provider的值
```typescript
{
    provide: 'person2',
    useFactory() {
        return {
            name: 'bbb',
            desc: 'cccc'
        }
    }
}

```
`useFactory`支持通过参数注入到别的provider
```typescript
{
  provide: 'person3',
  useFactory(person: { name: string }, appService: AppService) {
    return {
      name: person.name,
      desc: appService.getHello()
    }
  },
  //inject表示注入的token，useFactory的参数接收
  inject: ['person', AppService]
}
```
useFactory支持异步,nest会等拿到异步方法的结果之后再注入
```typescript
{
			provide: 'student',
			async useFactory(person: any, appService: AppService) {
				await new Promise((resolve) => setTimeout(() => resolve(''), 3000));
				return { name: person.name, desc: appService.getHello() };
			},
			inject: ['person', Provider_Token.APP_SERVICE],
		},
```
token别名
```typescript
//token：person是已经存在的token，student相当于别名
	{
		provide: 'student',
		useExisting: 'person',
	},
```

## 总结
默认的 token 就是 class，这样不用使用 @Inject 来指定注入的 token。
但也可以用字符串类型的 token，不过注入的时候要用 @Inject 单独指定。