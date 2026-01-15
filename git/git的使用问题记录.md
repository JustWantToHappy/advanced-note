## 查看当前git协议模式
- git remote -v
> 如果是https则打印https地址，如果是ssh，则打印ssh地址
- 实现ssh和https的切换：
1. 切换到ssh`git remote set-url origin git@github.com:JustWantToHappy/studyJS.git`
2. 切换到https:`git remote set-url origin https://github.com/JustWantToHappy/studyJS.git`

## https方式访问github失败，例如git push，git clone等
查看是否被设置了代理：
git config --global --get https.proxy 

设置代理：Git 的所有 HTTPS 请求走 Clash 的 HTTP 代理端口
1. git config --global http.proxy http://127.0.0.1:7890
2. git config --global https.proxy http://127.0.0.1:7890
取消代理：
1. git config --global --unset http.proxy
2. git config --global --unset https.proxy

如果配置了ssh，简单的方式可以通过ssh的方式，而不是https的方式连接github
例如：git remote set-url origin git@github.com:JustWantToHappy/studyJS.git，之后我们就可以对该仓库正常进行git相关的命令了

## 检测ssh是否连接成功
- ssh -T git@github.com
ssh模式下，排查问题如果无法解决，可重新生成公钥密钥，去github配置好公钥重新来一次