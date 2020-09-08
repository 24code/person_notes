# elasticsearch 安装指南
## 安装项
1. elasticsearch
2. elasticsearch-head 
## 安装环境
- centos 7 单核,2G
- java 1.8
- nodejs 10.1
## 场景分析
### 导入mysql数据到ES
1. [logstash + jdbc-mysql-connector](https://segmentfault.com/a/1190000014387486)
    * 官方产品,支持 6.0以上
    * 不用修改mysql配置,无侵入
    * 接近实时导入,稳定性好
    * 增量导入不友好,只支持自增主键或timestamp
2. [go-mysql-elasticsearch + go env + mysqldump](https://github.com/siddontang/go-mysql-elasticsearch)
    * 支持binlog形式导入,对数据表结构无要求
    * 性能和稳定性不确定,尚待验证
    * 不能实时在线修改数据表结构,缓存原因?
    * mysql < 8.0,es < 6.0
## 参考
- [es 配置修改](http://www.cnblogs.com/ljhdo/p/4959412.html)
- [高效索引](https://blog.csdn.net/cyony/article/details/65437708)
## 问题
1. 关闭防火墙
   `systemctl stop firewalld.service #停止firewall`  
   `systemctl disable firewalld.service #禁止firewall开机启动`
2. 权限问题-can not run elasticsearch as root
    1. 添加用户 `groupadd elsearch  useradd elsearch -g elsearch`
    2. 授权文件夹 `chown -R elsearch:elsearch  elasticsearch`
    3. 切换用户 `su elsearch cd elasticsearch/bin`
3. linux 配置过低问题-max file descriptors [65535] for elasticsearch process is too low
   ```
   ——————–
    报错如下：
    ERROR: [2] bootstrap checks failed
    [1]: max file descriptors [65535] for elasticsearch process is too low, increase to at least [65536]
    [2]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
    —————-

    解决办法：
    sudo vi /etc/sysctl.conf

    添加下面配置：
    vm.max_map_count=655360 

    并执行命令：
    sysctl -p

    sudo vi /etc/security/limits.conf
    添加如下内容:

    * soft nofile 65536

    * hard nofile 131072

    * soft nproc 2048

    * hard nproc 4096

    重启 elasticsearch。
   ```
4. 安装head插件,解决跨域问题
`vi elasticsearch.yml`
``` yaml
http.cors.enabled: true
http.cors.allow-origin: "*"
```
