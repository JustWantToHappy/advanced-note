## 实现思路
它有一个放置对象的容器，程序初始化的时候会扫描class上声明的依赖关系，(在class上声明依赖的方式，大家都选择了装饰器的方式)然后把这些class都给new一个实例放到容器中。创建对象的时候，还会把他们依赖的对象注入进去，这就完成了自动的对象创建和组装。**从主动创建依赖到被动等待依赖注入，这就是反转控制**
<br>

![Alt text](image-3.png)
AppService声明了@Injectable,代表这个class支持依赖注入
![Alt text](image-4.png)
![Alt text](image-5.png)

AppController声明了@Controller,代表这个class支持依赖注入
前者AppController的构造器参数依赖了AppService，后者通过属性的方式声明了AppService,两种方式都可以

## nest中4种对象
### Module
Module可以理解成大家长，手下有四种孩子。如果某个service想要使用另一个module下的service的话，就必须在imports中导入其对应的module，因为provider想要服务别人，就必须需要"大家长"的同意.

### providers
声明本模块提供的服务（“依赖注入容器里的注册项”，所有可被注入的东西都必须通过 providers 声明，在启动时实例化并放入IOC容器中，比如Service、Repository、工厂函数创建的对象、工具类等）
### imports
引入其他模块的功能
### exports
暴露出本模块的服务给其他模块使用
