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

### 字符串拼接的底层原理
1. 无变量参与的拼接
```java
String str="a"+"b"+"c";//等同于String str="abc"，编译层会优化
```
2. 有变量参与的拼接
jdk8之前，底层使用的是StringBuilder
```java
String s1="a";
String s2=s1+"b";//等同于new StringBuilder().append(s1).append("b").toString();这里至少创建了两个对象，一个StringBuilder以及toString()方法也会创建一个对象
String s3=s2+"c";//与上面保持一致
```

jdk8的拼接底层
```java
String s1="a";
String s2=s1+"b";//创建一个字符串数组，预估长度为2，将字符串放入数组后拼接成字符串对象
String s3=s2+"c";//与上面保持一致
```

最终结论：不要使用+拼接字符串变量，浪费内存空间
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
#### StringBuilder底层原理
初始化一个默认容量16的数组，比如容量不够，比如我们放入了a-z26个英文字母之后，StringBuilder就会扩容：老容量*2+2=34，如果我们放入的字符串长度为36，超过了34，那就默认以最终的字符串长度为准，也就是扩容到36

### StringJoiner
是一个容器，内容可发生变化，JDK8出现
```java
			int arr[]=new int[]{1,2,3};
			//将数组拼接成字符串，第一个参数是分隔符号，第二个字符串参数是拼接字符串的开始，第三个字符串参数是拼接字符串的结束
			StringJoiner sj=new StringJoiner(",","[","]");
			for(int i=0;i<arr.length;i++){
					sj.add(arr[i]+"");
			}
			System.out.println(sj.toString());//[1,2,3]
```
## 集合
- 自动扩容
- 只能存储引用数据类型，如果要存储基本数据类型，需要转换为包装类
```java
//集合的增删改查
	ArrayList<String> list=new ArrayList<String>();
	list.add("a");
	list.add("b");
	list.add("a");
	list.remove("a");
	System.out.println(list);//[b,a]
	list.remove(1);//删除a
	System.out.println(list);//[b]
	list.set(0,"ac");//设置索引0的元素为ac
	System.out.println(list);//[ac]
	System.out.println(list.get(0));//ac
	//遍历集合
	for(int i=0;i<list.size();i++){
			System.out.println(list.get(i));
	}
	//添加基础数据类型，使用包装类：比如int的包装类型是Integer
	ArrayList<Integer> intList=new ArrayList<>();
	intList.add(1);
```