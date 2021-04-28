
# 配置说明

> 建议后台关闭nscd、systemd-resolved进程，以免导致UDNS解析失败。

在使用UDNS产品时，需要将UHost的主机默认DNS修改为以下配置。

```
北京二、上海二、广州
100.90.90.90
100.90.90.100

上海金融云
10.15.255.1

拉各斯


注：100.90.90.90、100.90.90.100可用于任何地域，但在上海金融云、拉各斯等地，托管需配置本地域DNS服务地址才可访问UDNS。

```

下面以北京二的配置为例，介绍不同操作系统下的DNS修改方式。

## CentOS（含CentOS6/7/8）

1. 修改/etc/resolv.conf ：

```
sudo vim /etc/resolv.conf
```

修改为以下内容：

```
nameserver 100.90.90.90
nameserver 100.90.90.100
```

保存退出，即可生效。

2. 进行持久化。查看当前网卡的配置文件 /etc/sysconfig/network-scripts/ifcfg-eth0 

```
sudo vim /etc/sysconfig/network-scripts/ifcfg-eth0
```

内容可能如下：
```
BOOTPROTO=none
DEFROUTE=yes
DEVICE=eth0
DNS1=10.23.255.1
DNS2=10.23.255.2
DNS3=114.114.114.114
GATEWAY=172.16.0.33
HWADDR=52:54:00:ab:98:0b
IPADDR=172.16.0.45
MTU=1454
NETMASK=255.255.255.240
NM_CONTROLLED=no
ONBOOT=yes
STARTMODE=auto
TYPE=Ethernet
USERCTL=no
```

修改DNS相关配置如下：
```
DNS1=100.90.90.100
DNS2=100.90.90.90
```
保存并退出。

## Ubuntu(含14.04/16.04/18.04)

1，修改当前的/etc/resolv.conf 配置文件：
```
sudo vim /etc/resolv.conf
```
修改为：

```
nameserver 100.90.90.90
nameserver 100.90.90.100
```
DNS配置即可生效。

2.持久化， 查看网卡配置文件，如下：
### 非cloud init启动管理
```
sudo vim /etc/network/interfaces
```
其内容可能如下：

```
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet static
address 172.16.0.35
netmask 255.255.255.240
gateway 172.16.0.33
mtu 1454
dns-nameservers 10.23.255.1 10.23.255.2 114.114.114.114
```
修改dns-nameservers 这一行为：

```
dns-nameservers 100.90.90.90 100.90.90.100 114.114.114.114
```
并退出保存。

### 使用cloud init进行启动管理
```
sudo vim /etc/network/interfaces.d/50-cloud-init.cfg
```

其内容可能如下：

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.1.248/26
    dns-nameservers 10.23.255.1 10.23.255.2 114.114.114.114
    gateway 192.168.1.193
    mtu 1454
```

修改dns-nameservers 这一行为：

```
dns-nameservers 100.90.90.90 100.90.90.100 114.114.114.114
```
并退出保存。


## Windows(含2008/2012/2016)

1. 右键点击start,选择 network connections。
![images](/images/windows1.png)

2. 右键点击 Ethernet，选择Properties.
![images](/images/windows2.png)

3. 选择Internet Protocol Version4(TCP/IPv4）,并修改Preferred DNS server和Alternnate DNS server:
![images](/images/windows3.png)

4. 点击OK，即可修改成功。

## Debian(含8/9/10)

1，修改当前的/etc/resolv.conf 配置文件：
```
sudo vi /etc/resolv.conf
```
修改为：

```
nameserver 100.90.90.90
nameserver 100.90.90.100
```
DNS配置即可生效。

2.持久化， 查看网卡配置文件，如下：
### 非cloud init启动管理
```
sudo vi /etc/network/interfaces
```
其内容可能如下：

```
auto lo
iface lo inet loopback
auto eth0
iface eth0 inet static
address 172.16.0.35
netmask 255.255.255.240
gateway 172.16.0.33
mtu 1454
dns-nameservers 10.23.255.1 10.23.255.2 114.114.114.114
```
修改dns-nameservers 这一行为：

```
dns-nameservers 100.90.90.90 100.90.90.100 114.114.114.114
```
并退出保存。

### 使用cloud init进行启动管理
```
sudo vi /etc/network/interfaces.d/50-cloud-init
```

其内容可能如下：

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
    address 192.168.1.248/26
    dns-nameservers 10.23.255.1 10.23.255.2 114.114.114.114
    gateway 192.168.1.193
    mtu 1454
```

修改dns-nameservers 这一行为：

```
dns-nameservers 100.90.90.90 100.90.90.100 114.114.114.114
```
并退出保存。


## Redhat 6.X

1. 修改/etc/resolv.conf ：

```
sudo vim /etc/resolv.conf
```

修改为以下内容：

```
nameserver 100.90.90.90
nameserver 100.90.90.100
```

保存退出，即可生效。

2. 进行持久化。查看当前网卡的配置文件 /etc/sysconfig/network-scripts/ifcfg-eth0 

```
sudo vim /etc/sysconfig/network-scripts/ifcfg-eth0
```

内容可能如下：
```
BOOTPROTO=none
DEFROUTE=yes
DEVICE=eth0
DNS1=10.23.255.1
DNS2=10.23.255.2
DNS3=114.114.114.114
GATEWAY=172.16.0.33
HWADDR=52:54:00:ab:98:0b
IPADDR=172.16.0.45
MTU=1454
NETMASK=255.255.255.240
NM_CONTROLLED=no
ONBOOT=yes
STARTMODE=auto
TYPE=Ethernet
USERCTL=no
```

修改DNS相关配置如下：
```
DNS1=100.90.90.100
DNS2=100.90.90.90
```
保存并退出。
