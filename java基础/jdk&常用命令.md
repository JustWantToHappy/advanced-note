## jdk
JDK 21 是 LTS（长期支持版），至此为止，目前有 JDK8、JDK11、JDK17 和 JDK21 这四个长期支持版

## javac&java命令
- javac:jdk提供的编译工具,把 .java 源代码编译成 .class 字节码文件
- java：java 命令用于启动 JVM，并运行 .class 字节码

## java代码执行流程
```
.java
↓ javac
.class
↓ JVM
解释/JIT
↓
机器码
↓
CPU执行
```

