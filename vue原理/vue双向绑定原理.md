## 双向绑定&单向绑定
vue的双向绑定，即数据与视图的响应式设计，具体表现为:view的改变能够让Model发生变化，同时Model的变化也能够实时更新View。
什么情况下用户可以更新View呢?比如：填写表单，当用户填写表单时，View的状态也就被更新了，如果此时MVVM框架可以自动更新Model的状态，那就相当于把Model和View做了双向绑定。
注意区别:单向数据绑定，所有数据只有一份，一旦数据发生变化，就去更新页面(只有data->DOM，没有DOM->data)。
## 原理概述
Vue数据双向绑定原理是通过数据劫持+发布者——订阅者模式的方式实现的，首先是通过Es5提供的Object.defineProperty()方法来劫持各个属性的getter、setter,并在当监听的属性发生变化的时候通知订阅者，是否需要更新，若更新就会执行对应的更新函数
常见的基于数据劫持的双向绑定有两种实现:

   - 一个是vue2中使用的Object.defineProperty
   - 一个是ES52015中新增的Proxy,vue3中使用Proxy代替Object.defineProperty
## 几种实现双向绑定的做法
目前几种主流的mvc框架都实现了单向数据绑定，而双向数据绑定可以理解为在单向绑定的基础上给可输入元素填入change事件，来动态修改model和view。
实现数据绑定的做法大致如下几种：

   - 发布者——订阅者模式
   - 脏值检查(angular.js)
   - 数据劫持(vue.js)

数据劫持:vue.js则是采用数据劫持结合发布者——订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter,getter,在数据变动的时候发布消息给订阅者，触发相应的监听回调。
### 数据劫持的优势
目前业界分成两个大的流派，一个是以React为首的单向数据绑定，另一个就是以Angular，Vue为主的双向数据绑定。
> 三大框架都是即可以双向绑定也可以单向绑定，如React可以手动绑定onChange和value实现双向绑定，也可以调用一些双向绑定库，vue也加入了props这种单向流的api

对比其他双向绑定的实现方法，数据劫持的优势所在:

1. **无需显示调用**，例如Vue运用数据劫持+发布订阅，直接可以通知变化并驱动视图，react需要显示调用setState
2. **可以精确得知变化数据**，劫持了属性的setter，当属性值改变时，可以精准获知变化的内容newVal,因此在这部分不需要额外的diff操作，否则只知道数据发生了变化而不知道具体哪些数据发生了变化，这个时候就需要大量的diff来找出变化值是额外性能损耗。
### 数据劫持实现思路

1. 利用Proxy或者Object.defineProperty生成的Observer针对对象/对象的属性进行劫持，在属性变化后通知订阅者。
2. 解析器Complie解析模板中Directive(指令),收集指令所依赖方法和数据，等待数据变化后然后进行渲染。
3. Watcher属于Observer和Compile桥梁，它将接受到的Observer产生的数据变化，并根据Compile提供的指令进行视图渲染，使的数据变化促使视图变化。
## 数据代理

- 数据代理:通过一个对象代理对另一个对象中属性的操作(读/写)
- vue数据代理:通过vm对象来代理data对象中所有属性的操作
- 好处:更加方便操作data中的数据
- 基本实现过程:
   - 通过Object.defineProperty(vm,key,{})给vm添加与data对象的属性对应的属性
   - 所有添加的属性都包含get/set方法
   - 在get/set方法中去操作data中对应的属性。

示例:
```javascript
 let obj = { _data: {} }
    Object.defineProperty(obj, "age", {
        enumerable: true,
        configurable: false,
        get() {
            console.info("有人访问");
            return obj._data.age;
        },
        set(age) {
            obj._data.age = age;
        }
    })
    obj.age = 1345;
    console.info(obj.age);
```
## 模板解析
### 模板解析的流程

1. 将el的所有子节点取出，添加到一个新建的fragment文档对象中。
2. 对fragment中的所有层次子节点递归进行编译解析处理。
   1. 对大括号表达式文本节点进行解析
   2. 对元素节点的指令属性进行解析
      1. 事件指令解析(v-on:click等)
      2. 一般指令解析(v-bind,v-for等)
3. 将解析后的fragment添加到el中显示。
## 数据劫持
**observe(data,this)**

1. 数据劫持是vue中用来实现数据绑定的一种技术。
2. 基本思想:通过Object.defineProperty()来监视data中所有属性数据的变化，一旦变化就去更新界面。例如:this.xxx=3，此时this是vm，改变vm的set的值，然后这里set变化了，会改变data中xxx的值，（vm-M）当data中xxx的值改变时，data的set值也会发生变化，就会去更新页面了。(M-V)
   1. vm中的set是用来实现数据代理的
   2. data中的set是用来实现数据绑定的
### 四个重要对象

- 模板编译(Compile)
- 数据劫持(Observer)
- 发布的订阅(Dep)
- 观察者(Watcher)
> MVVM模式就是要将这些模板进行整合，实现**模板和数据的绑定**

### Complier

- 用来解析模板页面的对象的构造函数(一个实例)
- 利用compiler对象解析模板页面
- 每解析一个表达式(非事件指令)都会创建一个对应的watcher对象，并建立watcher和dep的关系。
- compiler与watcher关系:一对多的关系.
- **Compiler** 对象中的绑定的回调函数就是指指令中定义的回调函数，例如 **v-model** 中的 **input** 事件回调函数(vue内置的一个实现视图更新数据的方法)或者自定义指令中的回调函数等等。

MVVM中调用了Compile类来编译我们的页面，开始实现模板编译。
### Observer

- 用来对data中所有属性数据进行劫持的构造函数
- 给data中所有属性重新定义属性描述(get/set)
- 为data中的每个属性创建对应的dep对象
> 可以利用Object.defineProperty()来监听属性变动，那么将需要observev的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter，这样的话，给这个对象的某个值赋值，就会触发setter，那么就能够监听到数据变化了。

### Watcher
更新显示内容的

- 模板中每个非事件指令或者表达式都对应一个watcher对象。
- 监视当前表达式数据的变化。
- 创建的时机：在初始化编译模板时。
- 对象的组成：
> {
> vm,//vm对象
> exp,//对应的指令的表达式
> cb,//当表达式所对应的数据发生变化时候的回调函数
> value,//表达式当前的值
> depIds,//表达式中各级属性对应的dep对象的集合对象
> }

观察者的目的就是给需要变化的那个元素增加一个观察者，用新值和老值进行对比，如果数据发生变化就执行对应的方法。
### Dep(发布的订阅)

- data中的每个属性（所有层次）都对应一个dep对象
- 创建的实际：
   - 在初始化definedata中各个属性时创建对应的dep对象。
   - 在data中某个属性值被设置为新的对象。
- 对象的结构:
> {
> id,//每个dep都有一个唯一的id
> subs//包含n个对应的watcher的数组
> }

- subs属性的说明：
   - 当watcher被创建时，内部将当前watcher对象添加到对应的dep对象的subs中。
   - 当此data属性的值发生变化时，subs中所有的watcher都会收到更新的通知，从而最终更新对应的界面。
```javascript
 class Dep {
    constructor() {
      // 订阅的数组
      this.subs = []
    }
    addSub(watcher) {
      this.subs.push(watcher);
    }
    notify() {
      this.subs.forEach(watcher => watcher.update());
    }
  }
```
### dep和watcher的关系
**多对多**

- 一个dep中可能包含了多个watcher(模板中有几个表达式中使用到了同一个属性)
- 模板中的一个非事件表达式对应一个watcher，一个watcher中可能包含了多个dep(表达式是多层，比如a.b)
## MVVM原理图分析
原理图分析(个人观点):

- 最开始肯定是进行一个数据的劫持和数据的代理(Observer)。
- 当初始化时，Compile会初始化视图对象，里面包含了绑定指令的所有DOM元素，同时将data数据用来初始化DOM元素。
- Observer当数据发生变化的时候就会通知dep
- dep可以看做发布的订阅，watcher可以看做观察者，两者之间是多对多的关系，dep发布变化后，watcher调用回调函数，触发Compiler对象中绑定的回调。

