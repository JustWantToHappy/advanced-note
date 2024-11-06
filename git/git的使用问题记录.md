## git clone、git push出现超时问题
配置代理，找到.ssh文件下的config并做配置
![alt text](image-1.png)
- 后续克隆新的项目时使用git clone ssh地址
- 如果之前的项目是使用https克隆下来的，后续可以使用如下命令切换到ssh:git remote set-url origin git@github.com:facebook/react.git,之后使用git clone、git push命令就都是正常的了