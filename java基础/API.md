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

## Math类
```java
   System.out.println(Math.abs(-2147483648));//-2147483648，取绝对值，但是对于int的左边界不能取，因为int类型的右边界的范围比左边界范围小1
		System.out.println(Math.abs(-2147483647));//2147483647
		System.out.println(Math.round(4.5));//四舍五入
		System.out.println(Math.pow(2,3));//result：8.0，获取a的b次幂
		System.out.println(Math.random());//[0,1)之间的随机小数
		//ceil:进一法，往数轴的正方向进一
		System.out.println(Math.ceil(-12.4));//12.0
		//floor:与ceil相反，正反向减一
		//开平方根
		Math.sqrt(4);//2.0
		//开立方根
		Math.cbrt(8);//2.0
```

## System
```java
			Scanner sc = new Scanner(System.in);
			//0：表示当前虚拟机是正常停止
			//非0：表示当前虚拟机异常停止
			System.exit(0);
			//此处代码不再执行
			sc.nextLine();
```
```java
		long l=System.currentTimeMillis();
		System.out.println(l);//是一个时间戳，表示从时间原点到当前系统时间，使用场景：获取程序前后运行的时间
		int arr1[]={1,2,3,4,5};
		int arr2[]=new int[5];
		//参数2：从数据源数组中的第几个索引开始拷贝
		//参数4：目的地数组的索引（arr2）
		//参数5:拷贝的个数
		System.arraycopy(arr1,0,arr2,1,arr1.length-1);
```

## RunTime
```java
		Runtime r=Runtime.getRuntime();//获取当前运行环境，这是个静态方法，单例模式获取到的Runtime对象，保证整个程序生命周期使用的运行环境是一致的
		System.out.println(r.availableProcessors());//获取CPU线程数
		System.out.println(r.maxMemory());//单位字节；jvm能从操作系统获取到的最大内存大小
		System.out.println(r.totalMemory());//单位字节；jvm已经从操作系统获取到的内存大小
		System.out.println(r.freeMemory());//单位字节：jvm剩余的内存大小
		r.exec("notepad");//运行cmd命令
		r.exit(0);//System.exit底层调用的就是这个方法
```

## Object
- Object是java的顶级父类，所有的类都直接或间接继承于父类
- Object中的方法是可以被子类去访问的
- Object只有无参的构造方法

当我们打印一个对象的时候，底层会调用toString方法，把对象变成字符串
```java
		Object obj=new Object();
		System.out.println(obj);//与obj.toString一样的效果
		System.out.println(obj.toString());//result:java.lang.Object@b4c966a（包名@对象地址值）
```
重写equals方法
```java
  class Student{
            private String name;

            public Student(String name){
                this.name=name;
            }
            @Override
            public boolean equals(Object o) {
                if (o == null || getClass() != o.getClass()) return false;
                Student student = (Student) o;
                return Objects.equals(name, student.name);
            }
        }
        Student s1=new Student("123");
        Student s2=new Student("123");
        System.out.println(s1.equals(s2));//默认调用的是Object的equals（==判断地址值）方法，如果需要自定义，可以重写
```