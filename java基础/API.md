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

### 字符串的一些常用方法
```java
        String a="abc";//记录的是串池中对象的地址
        String b=new String("abc");//记录的是堆中对象的地址
        System.out.println(a==b);//false
```
- 如果想要比较内容如何处理？
```java
System.out.println(a.equals(b));//true
```
- 判断字符是否是大写字母or小写字母的技巧：
```java
String a="aAz";
char c=a.charAt(index);
//char类型的变量在参与计算的时候自动类型提升为int 查询ascii码
if(c>='a'&&c<='z'){
    System.out.println("是小写字母");
}
```
- replace方法：用于替换敏感信息为*非常有用
```java
String str = "hello world";
String newStr = str.replace('l', 'x');
System.out.println(newStr); // hexxo worxd
```
### StringBuilder
StringBuilder可以看做一个容器，创建之后里面的内容是可以发生变化的
```java
//为什么使用StringBuilder
String s1=a+b+d;//这里每次都会创建新的字符串对象
//创建一个空白可变字符串对象，不含有任何内容
StringBuilder sb=new StringBuilder();
//根据字符串内容，来创建可变对象字符串
StringBuilder sb1=new StringBuilder("abc");
//打印结果是字符串,而不是对象地址，因为toString方法被重写了
System.out.println(sb1);
//添加数据，可以添加任意类型
sb1.append("123");
sb1.append(true);
sb1.append(2.3);
//反转
sb1.reverse();
System.out.println(sb1);//输出容器中反转后的内容
```