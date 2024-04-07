## linux相关命令
-  vim中在一般模式下复制yy,粘贴p，删除一行dd
- 复制文件以及文件夹:cp [配置项] 1.txt /niuma(配置项有:-r表示递归)
- cal查看日历，date查看日期
- 创建空文件:touch a.txt
- 分屏查看 ls -l | more
- 添加用户(useradd 用户名),同时设置密码:(passwd 用户名)
- 删除一个用户(userdel -r 用户名)
- 删除空目录:rmdir /home
- 创建多级目录：mkdir -p /home/animal(单独使用mkdir是无法创建多级目录的，如果使用sudo即可)
- 创建一个目录：sudo mkdir /home/dog:有时候需要申请权限所以加上sudo,然后输入密码即可
- 删除目录指令：sudo rmdir /home(删除的是空目录)
- 若删除非空目录使用： rm -rf /home/dog(使用时一定要格外地小心)
- 删除普通文件:rm 文件名称
- ls -ahl命令：用于查看文件的所有者
- 移动文件：
- 目录与移动后的目录一致，仅仅是重命名:mv /home/a.txt /home/b.txt
- 目录与原目录一致，没有指定新文件名称，效果仅仅是移动：mv /home/ffxhd/a.txt /home/ffxhd
- 移动加上重命名:mv /home/ffxh/a.txt /home/ffxh/test/b.txt
- 向文件中写入:覆盖写入:echo "abc" > a.txt,追加写入:echo "abc" >> a.txt

```shell
total 28K
dr-xr-x---.  2 root root  135 Dec 16 02:34 .
dr-xr-xr-x. 17 root root  224 Dec 14 01:38 ..
-rw-------.  1 root root 1.3K Dec 14 01:38 anaconda-ks.cfg
-rw-------.  1 root root 1.2K Dec 16 02:34 .bash_history
-rw-r--r--.  1 root root   18 Dec 28  2013 .bash_logout
-rw-r--r--.  1 root root  176 Dec 28  2013 .bash_profile
-rw-r--r--.  1 root root  176 Dec 28  2013 .bashrc
-rw-r--r--.  1 root root  100 Dec 28  2013 .cshrc
-rw-r--r--.  1 root root  129 Dec 28  2013 .tcshrc
第一列共十位：第一位表示文档类型，d表示目录，-表示文件，l表示链接文件，d表示可随机存取的设备
，如U盘，c表示一次性读取设备，如鼠标，键盘等，后9位，依次对应三种身份对应的权限，身份顺序为：
owner,group,others,权限顺序为：readable,writable,excutable,如：-r-xr-r的含义是当前文档是一个
文件，拥有者可读可执行，同一个群组下的用户，可读，可执行，其他人没有任何权限
第二列表示链接数量，表示有多少个文件链接到inode号码
第三列表示拥有者
第四列表示所属群组
第五列表示文档容量大小，单位字节
第六列表示文档最后修改时间，注意不是文档的创建时间哦
第七列表示文档名称，（以.开头的表示隐藏文档）
```
- 改变用户所在组：(在root的管理权限下),可以改变某个用户所在的组
a.usermod -g 新组名 用户名
b.usermod -d 目录名 用户名，改变用户登录的初始目录
- 修改权限：使用chmod命令
```shell
第一种方式：+,-,=变更权限
u拥有者；g所在组；o其他人；a所有人(u，g，o的总和)
chmod o+w 文件/目录名(给文件的其他用户赋予写的权限)
chmod a-x 文件/目录名(将所有人关于该文件/目录的x权限去掉)
第二种方式：通过数字变更权限
r=4;w=2;x=1;rwx=4+2+1=7
chmod u=rwx,g=rx,o=x 文件/目录名相当于chmod 751 文件/目录名
```
- 修改文件的所有者chown
```shell
chown newowner 文件/目录名              改变所有者
chown newowner:newgroup 文件/目录名          改变所有者和所在组
```
- 查看文件内容的命令：cat 文件名称或者tail 文件名称或者more 文件名称