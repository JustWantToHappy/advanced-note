## jdk
JDK 21 是 LTS（长期支持版），至此为止，目前有 JDK8、JDK11、JDK17 和 JDK21 这四个长期支持版

## javac&java命令
- javac:jdk提供的编译工具,把 .java 源代码编译成 .class 字节码文件
- java：java 命令用于启动 JVM，并运行 .class 字节码
## jdk&jre&jvm
JDK > JRE > JVM

- jdk：包含jvm和核心类库以及开发工具(javac编译工具，java运行工具，jdb调试工具等)
- jre：包含jvm和核心类库以及运行工具（java的运行环境）
- jvm：只识别class字节码文件

所以jdk能写java，编译java和调试java
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
## java跨平台的原理
Java 不直接运行在操作系统上，而是运行在 JVM（Java 虚拟机）上，针对每个操作系统安装不同的jvm
