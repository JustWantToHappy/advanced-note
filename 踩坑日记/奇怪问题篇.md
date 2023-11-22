- prisma存入数据库的日期默认是UTC时间，dayjs().format不会将UTC时间转换为本地时间，需要使用dayjs特定的插件
- class-transformer中的@Type(()=>Boolean)为什么只会返回一个true
```typescript
//nestjs中的service
class XXXService{
    //controller会调用create方法，create方法会调用createS方法
    async create(){
        createS();//错误，nest不能够捕获此异常
        await createS();//正确写法
    }
    async createS(){
        if(xxx){
            throw new BadRequestExeception("");
        }
    }
}

```