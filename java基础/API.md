## API
目前JDK中提供的各种功能的java类
## String类
- java.lang包中的String类，无需导包
- String对象在创建之后无法变更
```java
        char chrs[]={'a','b','c','d'};
        System.out.println(new String(chrs));//abcd
        byte chrs1[]={97,98,99,100};
        System.out.println(new String(chrs));//将字节转换为ascii码：abcd
```

### 字符串比较
```java
        String a="abc";//记录的是串池中对象的地址
        String b=new String("abc");//记录的是堆中对象的地址
        System.out.println(a==b);//false
```
如果想要比较内容如何处理？