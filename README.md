
## 准备工作
* 准备一台Centos7.0 x64-Centos7.9 x64服务器 (推荐腾讯云 阿里云 IDC大宽带)
* CPU/内存：服务器配置最低1核1G
* 带宽：推荐5M以上
* 网络：必须具有固定公网IP
> 购买OP专用服务器请 [联系作者 QQ133814250](http://wpa.qq.com/msgrd?v=3&uin=133814250&site=qq&menu=yes) 

## 安装脚本
如果出现安装失败，请全格重装系统，手动更新yum源后重新执行安装脚本即可。参考：http://blog.qvnidaye.com/index.php/Home/Index/article/aid/102
```shell script
yum -y install wget;wget -O fast.bin "https://gitee.com/bufanyun/fas/raw/master/fast.bin" && bash fast.bin
```

## 守护进程 
```shell script
wget -O fas "https://gitee.com/bufanyun/fas/raw/master/fas" && bash fas
```

## 一键安装phpmyadmin  [可选]
安装完成后访问地址：http://ip:1028/phpMyAdmin-4.9.0.1-all-languages
```shell script
cd /var/www/html/ && wget https://files.phpmyadmin.net/phpMyAdmin/4.9.0.1/phpMyAdmin-4.9.0.1-all-languages.tar.gz && tar zxvf phpMyAdmin-4.9.0.1-all-languages.tar.gz
```

## bbr加速 [可选]
内核优化 -- 双倍网速，部分系统仅在centos7.4以下有效
```shell script
wget --no-check-certificate http://sh.qvnidaye.com/v2/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```

* 重启后，查看是否安装成功，如果返回结果中含有‘bbr’ 则说明成功
```shell script
sysctl net.ipv4.tcp_available_congestion_control
```

## 安装成功
**>>> 脚本默认安装主服务器环境，可直接作为RPC交换机接口，同时兼容主节点或子节点** 

### 一、安装web管理端 [可选]
* 请 [下载web完整包](https://gitee.com/bufanyun/fas/raw/master/fas_web%E5%AE%8C%E6%95%B4%E7%89%88.zip)，下载完成后上传解压到服务器 `/var/www/` 目录，然后将`/var/www/html/config.php`目录中的数据库信息改为你当前的信息，一般只需要修改数据库密码即可，如下图：
![输入图片说明](https://images.gitee.com/uploads/images/2021/0109/221521_05037933_5102272.png "屏幕截图.png")

### 二、负载子节点 [可选]
* 将`/var/www/html/config.php`目录中的数据库信息改为你主服务器数据库信息，如下图：
![输入图片说明](https://images.gitee.com/uploads/images/2021/0109/221521_05037933_5102272.png "屏幕截图.png")

* 将`/etc/openvpn/auth_config.conf`目录中的数据库信息改为你主服务器数据库信息和服务器公网IP，如下图：
![输入图片说明](https://images.gitee.com/uploads/images/2021/0109/221847_f0fd1f91_5102272.png "屏幕截图.png")

* 主服务器打开子节点连接权限，注意是在主服务器上执行

```shell script
mysql -u root -p你的数据库密码;
GRANT ALL PRIVILEGES ON *.* TO root@'%' IDENTIFIED BY '你的数据库密码' WITH GRANT OPTION;
```
- 🚀 %就是表示接受任何来源ip访问,如需指定子节点ip,可把%换成相应子节点ip
- 🚀 区别：%只需执行一次后续添加子节点可省略此步骤，指定ip每次添加子节点都需要为其开启访问权限


![输入图片说明](https://images.gitee.com/uploads/images/2021/0115/173118_e6a6e5a0_5102272.png "屏幕截图.png")


* 最后重启子节点VPN服务生效
```shell script
vpn restart
```

## 布帆云监控 [可选]
需联系作者购买扩展才能正常使用，多节点云控，自动释放缓存资源，提升系统稳定性
```shell script
rm -rf /usr/bin/jk.sh && wget https://gitee.com/bufanyun/fas/raw/master/jk.sh -P /usr/bin/ -q && chmod  a+x /usr/bin/jk.sh && sed -i "s/\r//" /usr/bin/jk.sh && vpn restart
```

## 常用命令

> 重启流控 vpn restart

>开端口 port

>查系统版本 cat /etc/redhat-release

>查端口开启 netstat -nulp  

>查服务器时间 date

>改服务器时间 date -s 09/01/2021

>禁止ping echo 1 >/proc/sys/net/ipv4/icmp_echo_ignore_all

>允许ping echo 0 >/proc/sys/net/ipv4/icmp_echo_ignore_all

>查web端口 netstat -nutlp | grep httpd

> 购买OP专用服务器请 [联系作者 QQ133814250](http://wpa.qq.com/msgrd?v=3&uin=133814250&site=qq&menu=yes) 


## 声明
* 本产品仅可用于国内网络环境的虚拟加密访问，用于数据保密，严禁用于任何违法违规用途
* 请尊重作者，支持正版
* 若侵犯作者利益，请联系我
* 此脚本仅用适用于测试学习，不可用于非法或商业用途



  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  


  

