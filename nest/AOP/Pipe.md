## 定义
pipe就是在参数传给handler之前对参数做一些验证和转换的class

内置的Pipe有这些：
- ValidationPipe
- ParseIntPipe
- ParseBoolPipe
- ParseArrayPipe
- ParseFloatPipe
等等

```typescript
	@Get()
	sayHello(@Query('page', ParseIntPipe) aa: number) {
		return aa + 1;
	}
```

## 自定义pipe
继承PipeTransform接口即可
```typescript
@Injectable()
export class ParseRolePipePipe implements PipeTransform {
	transform(value: string, metadata: ArgumentMetadata) {
		if (Role['USER'] == value) {
			return '普通用户';
		} else if (Role['ADMIN'] === value) {
			return '管理员';
		} else {
			//没有权限，直接抛出错误
			throw new ForbiddenException('没有权限');
		}
	}
}
class Bbb{
    @Get(':role')
	getRole(@Param('role', ParseRolePipePipe) role: any) {
		return role;
	}
}
```