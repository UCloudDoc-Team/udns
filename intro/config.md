
# 配置说明

在使用UDNS产品时，需要将UHost的主机默认DNS修改为以下配置。

```
100.90.90.90
100.90.90.100
```

下面介绍不同操作系统下的DNS修改方式。

## CentOS

1. 修改/etc/resolv.conf ：

```
sudo vim /etc/resolv.conf
```

修改为以下内容：

```
nameserver 100.90.90.90
nameserver 100.90.90.100
```

2. 保存退出，即可生效。

## Ubuntu

1. 查看网卡配置文件，如下：
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

2，修改dns-nameservers 这一行为：

```
dns-nameservers 100.90.90.90 100.90.90.100
```
并退出保存。

3，修改当前的/etc/resolv.conf 配置文件：
```
sudo vim /etc/resolv.conf
```
修改为：

```
nameserver 100.90.90.90
nameserver 100.90.90.100
```
并退出保存，即可生效。

## Windows

1. 右键点击start,选择 network connections。
![images](/images/windows1.png)

2. 右键点击 Ethernet，选择Properties.
![images](/images/windows2.png)

3. 选择Internet Protocol Version4(TCP/IPv4）,并修改Preferred DNS server和Alternnate DNS server:
![images](/images/windows3.png)

4. 点击OK，即可修改成功。


