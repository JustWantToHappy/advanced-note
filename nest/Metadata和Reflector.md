## reflect-metadata
因为Reflect相关API还在起草阶段，所以nest中内置了一个reflect-metadata的polyfill
```typescript
import "reflect-metadata";

class Guang {
  @Reflect.metadata("名字", "光光")
  public say(a: number): string {
    return '加油鸭';
  }
}

```
## nest与Metadata的联系
nest依赖注入的原理大致如此

通过装饰器给 class 或者对象添加元数据，然后初始化的时候取出这些元数据，进行依赖的分析，然后创建对应的实例对象
```typescript
const Module = (props: { controllers: any[]; provides: any[] }) => {
	const { controllers, provides } = props;
	return function (target) {
		Reflect.defineMetadata('controllers', controllers, target);
		Reflect.defineMetadata('provides', provides, target);
	};
};

@Module({ controllers: [], provides: [] })
export class AppModule {}
//这样就可以获取到定义的元数据了
//console.log(Reflect.getMetadata('controllers', AppModule));
```
## 构造器参数依赖
nest除了使用装饰器注入依赖，还可以实现构造器参数注入依赖
```typescript
@Controller('cats')
export class CatsController {
    //catService对象并没有使用装饰器，那么它是如何注入的？
  constructor(private readonly catsService: CatsService) {}
}
```
注入原理：TypeScript支持编译的时候自动添加一些metadata元数据
- `design:type`:描述装饰目标的元数据
- `design:paramtypes`:参数的类型
- `design:returntype`:返回值的类型
综上：通过design:paramtypes 来拿到构造器参数的类型
> 这也就是为什么nest会使用ts来写的原因了

## nest核心原理
**通过装饰器给 class 或者对象添加 metadata，并且开启 ts 的 emitDecoratorMetadata 来自动添加类型相关的 metadata，然后运行的时候通过这些元数据来实现依赖的扫描，对象的创建等等功能。**
## reflector与metadata的联系
```typescript
import { Observable } from 'rxjs';
import { Role } from 'src/utils/const';
import { Reflector } from '@nestjs/core';
import { CanActivate, ExecutionContext, Injectable } from '@nestjs/common';

@Injectable()
export class AaaGuard implements CanActivate {
	//注入Reflector对象
	constructor(private reflector: Reflector) {}

	canActivate(
		//ExecutionContext是ArgumentsHost的子类，ArgumentHost详情请看自定义filter
		context: ExecutionContext,
	): boolean | Promise<boolean> | Observable<boolean> {
		const requiredRoles = this.reflector.get<Role[]>(
			'roles',
			context.getHandler(),
		);

		if (Array.isArray(requiredRoles)) {
			return requiredRoles.includes(Role.ADMIN);
		}
		return true;
	}
}

```
我们知道在guard或其他切面中可以通过this.reflector.get获取自定义的元数据，而this.reflector.get的原理就是`Reflect.getMetadata`