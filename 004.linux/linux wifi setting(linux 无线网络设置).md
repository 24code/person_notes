# linux WIFI 连接
## 手动连接
`wlp3s0` 是linux分配的固件名称,通过 `ifconfig` 或 `nmcli` 指令就可以看到
1. 查看是否需要安装固件  
大多无线网卡还需要固件。内核一般会自动探测并加载两者，如果您得到类似 SIOCSIFFLAGS: No such file or directory 的输出，意味着您得手动加载固件。若不确定，用 dmesg 查询内核日志，看看有没有来自无线网卡的固件请求。比如您有 Intel 芯片组，输出大概是这样：
> dmesg | grep firmware
firmware: requesting iwlwifi-5000-1.ucode
若无输出，表明系统的无线芯片不需要固件。

1. 查看无线网口：
> iw dev(interface后面即为无线网口号)

1. 激活无线网络接口：
> ip link set wlp3s0 up 
为了检验接口是否激活成功，您可以查看以下命令的输出：
> ip link show wlp3s0
```
3: wlp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000 link/ether 00:11:22:33:44:55 brd ff:ff:ff:ff:ff:ff 
```
<BROADCAST,MULTICAST,UP,LOWER_UP> 中的UP 表明该接口激活成功，后面的 state DOWN 无关紧要。

1. 查看无线网络连接情况：
> iw wlp3s0 link
刚开始应该会显示无连接

1. 扫描可连接的wifi
> iw wlp3s0 scan | grep SSID

1. 扫描可用的网络
连接指定的SSID
> wpa_supplicant -B -i wlp3s0 -c <(wpa_passphrase "ssid" "psk") 
将ssid 替换为实际的网络名称，psk 替换为无线密码，请保留引号。

1. 用dhcp 获得 IP 分配：
> dhclient wlp3s0 

1. 测试是否成功地从路由器获取了ip(重要)
>ip addr show wlp3s0
如果分配有ip，即可上网，也可以有ping直接测试

## 设置自动连接
1. 在CentOS 7中 默认没有安装nmcli，nmcli的全称是NetworkManager，安装的命令如下：
> yum -y install NetworkManager NetworkManager-wifi  
> systemctl restart NetworkManager

1. 加入托管,设置自动启动
> nmcli dev set wlp9s0 autoconnect yes managed yes

1. 连接wifi
> nmcli dev wifi connect CC password 123456789

## 参考
[centos7使用无线wifi连接](https://www.cnblogs.com/kluan/p/4457903.html)  
[笔记本安装CentOS 7连接wifi](https://kknews.cc/digital/nq65vg3.html)
