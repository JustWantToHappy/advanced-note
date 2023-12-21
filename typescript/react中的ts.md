## React中使用ts遇到的问题
无法给window对象添加属性
```typescript
decalre global{
    interface Window{
        aaa:boolean;    
    }
}
window.aaa=false;//不会报错
```
react中关于给元素绑定事件时碰到的类型问题
注意:使用react时，无法阻止合成事件的默认行为，而不得不手动阻止默认行为并停止事件冒泡。
```tsx
 const handleScroll = function (event: React.UIEvent<HTMLDivElement>) {

    };
//如果要使用原生事件类型
 const handleClick = (event: React.MouseEvent<HTMLCanvasElement>) => {
        console.info(event.nativeEvent?.offsetX);
    }
<div onScroll={handlScroll}></div>
```
## react中几种内置节点类型
- React.FC类型，可以表示函数式组件接受泛型React.FC<IProps>,也可以使用React.FunctionComponent
- React.ComponentClass，类式组件，接受泛型:React.ComponentClass<IProps,IState>
- React.JSX.Element：几乎等同于React.ReactElement
```typescript
declare global {
  namespace JSX {
    interface Element extends React.ReactElement<any, any> { }
  }
}
```
- React.ReactElement：这是一个有type、props、key的对象，被createElement函数调用，根据环境设置对应的属性
- React.ReactNode:ReactNode:<div></div>的合法类型，React.ReactElement是React.ReactNode的子类型
- React.FC<React.PropsWithChildren>
