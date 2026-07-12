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
		System.out.println(Math.ceil(-12.4));//-12.0
		//floor:与ceil相反，反向减一
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
### equals方法
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
### clone方法
对象克隆：方法在底层会创建一个对象，并把原对象中的数据拷贝过去
1. 重写Object中的clone方法
2. 让javabean类实现Cloneable接口
3. 创建原对象并调用clone方法
```java
 //Cloneable这个接口中并没有抽象方法，表示当前接口是一个标记性接口，表示当前类实现了这个接口，可被克隆
        class Student implements Cloneable {
            private String name;

            public Student(String name){
                this.name=name;
            }

            @Override
            public String toString() {
                return this.name;
            }

            @Override
            protected Object clone() throws CloneNotSupportedException {
                return super.clone();
            }

            @Override
            public boolean equals(Object obj) {
                return this.name.equals(((Student) obj).name);
            }
        }
        Student s1=new Student("S1");
        Student s2=(Student) s1.clone();
        System.out.println(s1.equals(s2));//true
```
以上方法是浅拷贝，如果成员变量中的是引用数据类型，则克隆的对象与原对象使用的成员变量的地址值是同样的，以下是深拷贝方法：
1. 基本数据类型拷贝
2. String类型复用(串池)
3. 其他引用数据类型重新创建
```java
	public class App {
    //Cloneable这个接口中并没有抽象方法，表示当前接口是一个标记性接口，表示当前类实现了这个接口，可被克隆
    static class Student implements Cloneable {
        String name;
        int[] data = new int[]{1, 2, 3};

        // No-arg constructor required by Gson for deserialization
        public Student() {
        }

        public Student(String name) {
            this.name = name;
        }

        @Override
        public String toString() {
            return this.name + ", data=" + java.util.Arrays.toString(data);
        }

        @Override
        protected Object clone() throws CloneNotSupportedException {
            //获取原数组
            int[] newData = new int[data.length];
            for (int i = 0; i < data.length; i++) {
                newData[i] = data[i];
            }
            Student s = (Student) super.clone();
            s.data = newData;
            return s;
        }
    }

    public static void main(String[] args) throws IOException, CloneNotSupportedException {
        Student s1 = new Student("S1");
        Gson gson = new Gson();

        String json = gson.toJson(s1);
        System.out.println("JSON: " + json);
        
        Student s2 = gson.fromJson(json, Student.class);
        System.out.println("s1: " + s1);
        System.out.println("s2: " + s2);
    }
}
```
## BigInteger
BigInteger底层采用的是数组存储，将数字转换为二进制之后，每32个一组作为数组中的某一项
```java
			//获取指定的大整数（字符串必须是整数，否则报错）
			BigInteger bigInteger = new BigInteger("999999999999999999999999999");
			System.out.println(bigInteger);
			//获取指定进制的大整数
			BigInteger bigInteger1 = new BigInteger("100",2);
			System.out.println(bigInteger1);//100对应的2进制值转换为10进制结果为10
			//静态方法获取到BigInteger的对象,能表示的范围比较小，在long取值范围之内
			BigInteger bigInteger2 = BigInteger.valueOf(99999999999999999L);
			//对内部常用数字：-16-16进行了优化，提前创建了-16-16之间的对象
			BigInteger bigInteger3 = BigInteger.valueOf(16);
			BigInteger bigInteger4 = BigInteger.valueOf(16);
			System.out.println(bigInteger3==bigInteger4);//true
```

## BigDecima
- 用于小数的精准计算，可以用来表示很大的小数
- BigDecima底层采用的也是数组存储：先将每位上的数字转换为ASCII码，然后存储在数组中的每一项，包括小数点
```java
        //使用BigDecimal(double)构造方法可能不精确
        BigDecimal decimal1 = new BigDecimal(0.01);
        System.out.println(decimal1);//0.010000000...
        //使用BigDecimal(String)构造方法是精确的
        BigDecimal decimal2 = new BigDecimal("0.01");
        System.out.println(decimal2);//0.01
        //BigDecimal提供的方法计算，精度是准确的
        BigDecimal decimal3 = new BigDecimal("0.09");
        System.out.println(decimal2.add(decimal3));//0.10
        //通过静态方法获取对象
        BigDecimal  decimal4 = BigDecimal.valueOf(0.01);
        System.out.println(decimal4);//0.01
        //如果我们要传递的是0-10的整数，包含0，包含10，那么方法就会返回已经创建好的对象，不会重新new
        BigDecimal  decimal5 = BigDecimal.valueOf(10);
        BigDecimal  decimal6 = BigDecimal.valueOf(10);
        System.out.println(decimal6==decimal5);//true
```
## 正则表达式
- [a-d[m-p]]:a到d或者m-p，等同于[a-dm-p]
- [a-z&&[def]]:a-z和def的交集，为d,e,f
- [a-z&&[^bc]]:a-z和非bc的交集
- \表示的是转义字符，比如"\\"表示的就是斜杆，第一个\转义后面的\为普通的斜杆，再比如"\\d"，第一个\表示的是转义，而后面\d表示一个正则字符，而如果只写"\d"，	java编译器不认识这个转义序列，就会报错(转义序列比如"\n"换行，"\t"制表符，"\""双引号)
- 分组：通过()将正则表达式当做一个整体，比如"abab".matches("(ab)+");的结果是true，一个()表示的就是一个分组，正则表达式中每个分组都有序号，从左到右，左括号出现的位置表示的就是序号位置，比如(\\d+(\\s+))(0|1)，\\d前面的()表示的就是第一个分组，\\s+前面的()表示的就是第二个分组，0|1前面的表示的就是最后一个分组
```java
			String regex1="a(?i)bc";
			//忽略(?i)后面字符串的大小写规则
			System.out.println("aBC".matches(regex1));//true
			//忽略(?i)外层括号里面字符串的大小写规则
			String regex2="a((?i)B)c";
			System.out.println("aBC".matches(regex2));//false
			System.out.println("aBc".matches(regex2));//true
```
- \w表示的是单词字符：[a-zA-Z_0-9](注意有个下划线)
- \W表示的是非单词字符
- x?:一次或者0次
- x*:零次或者多次
- x{n,}:至少n次
- (?i):忽略大小写
- []:表示里面的内容只会出现一次，例如[a-z0-9A-Z]
- \\D表示非0-9
- \\S表示非空白字符
- 字符串常用的正则表达式相关的方法:replaceAll&split
```java
			String str="I 123 you";
			String result=str.replaceAll("\\d+","love");
			System.out.println(result);//I love you
			String arr[]=result.split("\s");//按照空白字符分割
			for(int i=0;i<arr.length;i++){
					System.out.println(arr[i]);
			}
```
### 捕获分组
后续还要使用本组的数据
1. 正则内部使用:\\组号
2. 正则外部使用:$组号
```java
					//判断字符串开始和结束字符是否相同
			String str="a123a";
			//\\组号表示的是把第X组的内容拿出来再用一次
			System.out.println(str.matches("(.).+\\1"));//true
			//判断字符串开始部分和结束部分是否一致，同时开始部分每个字符都要一样
			String str1="aaa123aaa";
			//(.)这个括号表示的就是第二个分组了，因为从左到右数(.)的左括号是第二个
			System.out.println(str1.matches("((.)\\2*).+\\1"));//true
			String str3="我要吃饭饭饭";
			System.out.println(str3.replaceAll("(.)\\1+","$1"));//我要吃饭
```
### 非捕获分组
分组之后不需要再使用本组数据，仅仅是将数据括起来
- (?:正则)获取所有
- (?=正则)获取前面部分
- (?!正则)获取不是指定内容的前面部分
- 非捕获分组是不占用组号的
```java
	  String str="Java的长期版本Java8";
		Pattern pattern = Pattern.compile("Java(?=8|11|17)");//匹配上Java8或者Java11或者Java17,但是只获取前面的部分，也就是Java
		Matcher matcher = pattern.matcher(str);
		while (matcher.find()) {
				System.out.println(matcher.group());//结果只会打印一次，输出Java8前面的Java
		}
```

### Pattern类
```java
		String str="Java是一门高级语言，其中Java8、Java11、Java17是长期支持版本";
		//1. 获取正则表达式的对象
		Pattern p=Pattern.compile("Java\\d{0,2}");
		//2. 获取文本匹配器的对象:拿m读取str，找符合p规则的子串
		Matcher m=p.matcher(str);
		while(m.find()){
				System.out.println(m.group());
				/**
				 * Java
				 * Java8
				 * Java11
				 * Java17
				 */
		}
```