# linux 虚拟机设置
## 常用指令
- `top` [查看系统资源占用情况](https://blog.csdn.net/daniel_ustc/article/details/12872991)
- `lsof -i` [查看文件和网络端口打开情况](http://blog.51cto.com/xiaofengge315/1410247)
- `netstat -aop|grep java` 查看进程情况,捕获关键字进程
- `find / -name sysctl.conf` [查找文件](https://blog.csdn.net/ydfok/article/details/1486451)
- `nohup npm start & exit` [守护进程启动](https://blog.csdn.net/qq_27231343/article/details/73330280)
- `tar -xvf xxxx` tar 解压
- `unzip xxx` zip 解压
## 问题
1. 安装好之后没有网络
   - virtualbox 虚拟机 网络改为桥接模式
   - 设置网卡为自启动
   > vi /etc/sysconfig/network-scripts/ifcfg-eth0
   > ONBOOT=yes
   - 重启服务
   > service network restart
如果不支持DHCP,需要自己手动配置IP,[参考](https://www.jianshu.com/p/a3c1f720d6ff)

1. yum 查询包,安装包
    - `yum list *name` vs `yum search name`
    > list通过通配符查找, search 模糊查找name desc等
    - `yum -y install name`
    - 添加 epel 下载最新的包
    > 方式一 `yum install epel-release -y`  
    > 方式二 `# rpm -ivh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm` `yum clean all && yum makecache`
    > 通过 `yum repolist` 查看安装的文件

1. nodejs 包升级
    > 解决epel安装版本低问题
    - `npm install -g n  n stable` 
    - `npm -g install npm@next`

1. 关闭防火墙
   `systemctl stop firewalld.service #停止firewall`  
   `systemctl disable firewalld.service #禁止firewall开机启动`
2. [免密码使用sudo和su](https://www.jianshu.com/p/5d02428f313d)
    1. `visudo  //或者vi /etc/sudoers`
    2. 到一行root ALL=(ALL) ALL的下一行,输入 your_user_name ALL=(ALL) NOPASSWD: ALL
## 附录
[快速理解VirtualBox的四种网络连接方式](https://www.cnblogs.com/york-hust/archive/2012/03/29/2422911.html)
[CentOS7安装EPEL的两种方式](https://www.jianshu.com/p/1882cd3b2295)
[升级node.js和npm](https://segmentfault.com/a/1190000009025883)
