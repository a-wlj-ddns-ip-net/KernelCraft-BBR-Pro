## Linux一键安装常见/最新内核脚本 BBR/BBRPLUS/BBR2/BBR3/LotServer

![Uploading Linux一键安装常见最新内核脚本 BBR-BBRPLUS-BBR2-BBR3-LotServer.png…]()

## 一键加速脚本使用教程 
### 安装wget下载工具，则执行命令：
```
yum -y install wget #CentOS/RedHat
```
```
apt-get install wget #Debian/Ubuntu
```
### 在安装BBR时，不卸载内核版本，则执行命令：

```
wget -O tcpx.sh "https://github.com/tudiedie/Linux-NetSpeed-TuDieDie/raw/master/tcpx.sh" && chmod +x tcpx.sh && ./tcpx.sh
```

### 在安装BBR时，卸载内核版本，则执行命令：
```
wget -O tcp.sh "https://github.com/tudiedie/Linux-NetSpeed-TuDieDie/raw/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```

### 关联action自动编译内核

[https://github.com/tudiedie/kernel/](https://github.com/tudiedie/kernel/)

### 同时安装BBR+锐速(LotServer)
#### bbr 添加

```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.d/99-sysctl.conf
```

```
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.d/99-sysctl.conf
```

```
sysctl -p
```

#### 编辑锐速文件

```
nano /appex/etc/config
```

#### 检测代码有BUG，如果锐速正常 运行查看

```
bash /appex/bin/lotServer.sh status | grep "LotServer"
```

#### 检查bbr 内核默认bbr算法不会有输出

```
lsmod | grep bbr
```

#### 检查centos安装内核

```
grubby --info=ALL|awk -F= '$1=="kernel" {print i++ " : " $2}'
```

#### 查看当前支持TCP算法

```
cat /proc/sys/net/ipv4/tcp_allowed_congestion_control
```

#### 查看当前运行的算法

```
cat /proc/sys/net/ipv4/tcp_congestion_control
```

#### 查看当前队列算法

```
sysctl net.core.default_qdisc
```

命令： `uname -a`
<br>
作用： 查看系统内核版本号及系统名称

命令： `cat /proc/version`
<br>
作用： 查看目录"/proc"下version的信息，也可以得到当前系统的内核版本号及系统名称

真实队列查看？ 更改队列算法可能需要重启生效
<br>
`tc -s qdisc show`

`/etc/sysctl.d/99-sysctl.conf`
<br>
`sysctl --system`

## 更新日志
1.3.2.7 更新bbr的c7,c8,d9,d10 升级到5.5.3内核；
<br>
1.3.2.8 更新bbr的c6,c7,c8,d8,d9,d10 升级到5.5.5内核；
<br>
1.3.2.9 更新bbr,zen的c7,d10 升级到5.5.6内核 xanmod的c7,d10 升级到5.5.4内核 更新部分写法；
<br>
1.3.2.10 xanmod的c7,d10 升级到5.5.6内核；
<br>
1.3.2.11 两个版本可以互相切换；
<br>
1.3.2.13 更新bbr c7,d10 升级到5.5.7内核 bbrplus降级到4.14.129 不再维护；
<br>
1.3.2.14 修复debian/ubuntu bbrplus BUG bbrplus安装方法和安装内核都和原作者一致了 我彻底甩锅；
<br>
1.3.2.15 xanmod的c7,d10 升级到5.5.6内核 xanmod5 xanmod下载链接 改为onedrive 若有问题请反馈；
<br>
1.3.2.17 bbr原版,xanmod,Zen内核c7,d10分别升级到5.5.8 均为onedrive链接；
<br>
1.3.2.18 bbrplus4.14.173 centos7,debian10 均为onedrive链接；
<br>
1.3.2.20 bbr原版,Zen内核c7,d10分别升级到5.5.10 均为onedrive链接  适配oracle centos7测试；
<br>
1.3.2.21 bbr原版,c7,d10分别升级到5.6.0 均为onedrive链接；
<br>
1.3.2.28 bbr原版升级到5.6.15 添加U20支持 均为onedrive链接；
<br>
1.3.2.29 bbrplus新版升级到bbrplus4.14.182 均为onedrive链接；
<br>
1.3.2.34 xanmod C7升级到5.7.2，debian及ubuntu用的官方编译的文件，没限制常用的debian和ubuntu版本，是否翻车自己测试，增加切换到秋水BBR功能；
<br>
1.3.2.35 xanmod debian及ubuntu用的官方编译的文件5.7.3，这次直接用的官方的下载链接；
<br>
1.3.2.36 更换锐速授权地址；
<br>
1.3.2.37 xanmod更新到5.7.4，debian及ubuntu用的官方编译的文件，原版BBR centos用的elrepo版本；
<br>
1.3.2.45 xanmod更新到5.8.10，原版BBR centos7更新到5.8.10，增加切换到一键DD脚本；
<br>
1.3.2.51 去除centos6的支持，去除Zen内核，debian和ubuntu使用同一内核，增加fq_pie选项；
<br>
1.3.2.53 添加johnrosen1的优化方案，去除默认优化方案的tcp_fastopen；
<br>
1.3.2.56 注释net.ipv4.ip_forward；
<br>
1.3.2.57 仅更新了可卸载版本,增加headers的卸载测试，应用了bbr原版和xanmod；
<br>
1.3.2.59 大量调整优化代码，新的优化方案不再叠加并支持卸载，调整bbr启动，不会卸载优化；
<br>
1.3.2.63 下架bbr2方案，等正式版本再考虑添加，不卸载内核版本添加官方稳定内核，官方最新内核，XANMOD官方内核，XANMOD官方高响应内核，debian官方cloud内核；
<br>
1.3.2.68 XANMOD 5.10.9及以后内核支持BBR2 增加IPv6处理；
<br>
13.2.74 更新新版bbrplus,来自github UJX6N的编译，兼容bbr+fq/fq_pie/cake仅限Cloud VMs；
<br>
13.2.76 去除CLOUD内核，由BBRPLUS新版替代，增加下载地址检测(不包含锐速内核)；
<br>
13.2.77 部分连接解析为官方连接 见上面版本号对应关系；
<br>
13.2.86 原版内核支持debian系arm64内核；
<br>
13.2.93 bbrplus新版改为UJX6N的源，我不再维护；
<br>
13.2.96 不卸载版本debian/ubuntu增加zen内核；
<br>
13.2.97 不卸载版本增加查看排序功能和删除保留指定内核功能；
<br>
13.2.101/102 尝试添加cn下载地址加速，更换锐速接口；
<br>
13.2.104 bbrplus新版改为UJX6N的5.15版本；
<br>
100.0.0.0 版本号从原脚本岔开；
<br>
100.0.1.12 bbrplus到6.0，tcpx xanmod main区分CPU；
<br>
100.0.1.15 修复john优化方案aws ipv6问题；
<br>
100.0.1.25 下架xanmod自编译版本，支持debian和centos的通用系统安装内核如Kali，其他一些调整；
<br>
无大内容更新见上面版本号对应关系；
<br>
…….
<br>
怎么玩？
<br>
1.安装了内核重启后再开启相应加速再重启。
<br>
2.或者安装内核后，接着开启bbr加速(失败的)，这时候再重启，bbr会在重启后生效(前提是启动时候是安装的内核)。
2020.6.14 测试锐速是正常的。

## 特别鸣谢
土爹爹博客
<br>
https://www.tudiedie.com
<br>
ylx2016原作者
<br>
https://blog.ylx.me/
<br>
bbsplus算法原作者
<br>
https://blog.csdn.net/dog250/article/details/80629551
<br>
bbrplus首用名 ？
<br>
https://github.com/cx9208/bbrplus
<br>
新版bbrplus
<br>
https://github.com/UJX6N/bbrplus-5.10
<br>
xanmod官网
<br>
https://xanmod.org
<br>
Zen官网
<br>
https://liquorix.net/
<br>
锐速
<br>
https://moeclub.org/2017/03/09/14/
<br>
其他内核
<br>
https://github.com/alibaba/cloud-kernel
<br>
https://github.com/Tencent/TencentOS-kernel
<br>
官方编译好的内核
<br>
https://sourceforge.net/projects/xanmod/files/releases/current
<br>
https://elrepo.org/linux/kernel/el7/x86_64/RPMS/
<br>
https://elrepo.org/linux/kernel/el8/x86_64/RPMS/
<br>
https://kernel.ubuntu.com/~kernel-ppa/mainline/
<br>
http://mirrors.aliyun.com/alinux/2.1903/plus/x86_64/Packages/
<br>
https://mirrors.tencent.com/tlinux/2.4/tlinux/x86_64/RPMS/
<br>
https://bintray.com/multipath-tcp/mptcp_rpm/mptcp/v0.95.1#files
<br>
https://bintray.com/multipath-tcp/mptcp_deb/mptcp/v0.95.1#files

DD脚本
<br>
https://git.beta.gs/
<br>
https://www.cxthhhhh.com/network-reinstall-system-modify


服务周期
<br>
https://zh.wikipedia.org/zh/Ubuntu
<br>
https://wiki.ubuntu.com/Releases
<br>
https://wiki.debian.org/LTS
<br>
https://wiki.centos.org/zh/About/Product
