
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

# 在 AWS 账户之间迁移资源

https://aws.amazon.com/cn/blogs/architecture/migrate-resources-between-aws-accounts/

## **注意：可以在旧AWS账户开放共享，然后新AWS账户即可**

![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765044.jpeg)  
  



# 如何关闭AWS账户
https://repost.aws/knowledge-center/close-aws-account

https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-closing.html




# **==注册新的AWS账户（可1年内每月免费750小时）==**

![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462764604.jpeg)


![image.png](https://repo.in4tree.com/2026/02/23_1771919090662.png)



## **MFA安全登录**

![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765283.jpeg)  



# **==安装过程最佳实践==**

## **新建EC2实例； Associate IP；SecureCRT连接**

Ubuntu，t3micro，30GB，创建密钥（aws_ubuntu24_20260223.pem）

![image.png](https://repo.in4tree.com/2026/02/23_1771919228063.png)

![image.png](https://repo.in4tree.com/2026/02/23_1771919239918.png)



## **更新系统软件包**

```sh
sudo apt update && sudo apt upgrade -y
apt update -y && apt install -y curl && apt install -y socat && opt install wget -y
```

reboot或重启实例！



# 注意：Nginx：主要用来做反向代理！（Apache不能！）


# 宝塔面板 1Panel LDNMP 三大建站系统谁搭建网站更简单 横向对比部署WordPress


## 安装宝塔国际版（aaPanel）

Amazon Linux EC2 部署宝塔面板
https://aws.amazon.com/cn/blogs/china/deploy-baota-panel-using-amazon-linux-ec2/


### 安装宝塔面板

https://www.aapanel.com/new/download.html

（aaPanel 7.0.30最高支持到：Ubuntu 22.04）

安装前最好清空（Apache、PHP、MySQL、FTP等）！最好从安装服务器后再立即开始安装宝塔面板！

```sh
URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh ipssl
```


### 安装BBR（网站加速！）

https://www.bilibili.com/video/BV16C411p7n9/

```sh
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh

```

![image.png](https://repo.in4tree.com/2026/02/23_1771910122189.png)


1. **选择内核**：
    - 在弹出的菜单中，选择 **1** 安装 BBR 原版内核。
    - 安装完成后，按提示输入 `y` **重启服务器**。
2. **开启 BBR**：
    - 重启后，再次运行 `./tcp.sh` 命令。
    - 选择 **2** 开启 BBR/BBR+FQ。
3. **验证**：输入 `sysctl net.ipv4.tcp_available_congestion_control`，如果返回结果包含 `bbr`，则说明安装成功。

![image.png](https://repo.in4tree.com/2026/02/23_1771910802969.png)



### 宝塔面板安装Tools：

https://zhitoo.site/bt-aapanel-step-by-step-beginner-setup-tutorial/

点击宝塔面板 =》Tools，这里面建议只安装下面两个：

- Linux Tools：这个可以设置时区、虚拟内存等
- Log cleanup：清理日志使用

![image.png](https://repo.in4tree.com/2026/02/23_1771908130525.png)



可以关闭面板 SSL 访问，直接使用 http 访问，就是去掉 https 中的 s，关闭 SSL 的方法如下：

![image.png](https://repo.in4tree.com/2026/02/23_1771907861207.png)


### 如何增加Server（比如Mail）？更改（比如Apache改为Ngnix）

![image.png](https://repo.in4tree.com/2026/02/23_1771911333586.png)


# =====

## **安装Apache2；PHP（安装常用扩展）；MariaDB（创建远程用户修改本地用户密码）**

**测试**  
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765503.jpeg)  

  
http://54.148.142.35/
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765715.jpeg)  

  
http://54.148.142.35/index.php
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462765925.jpeg)  

  
http://54.148.142.35/test.php
![Ubuntu24安装（1）注册新的AWS账户；安装过程最佳实践](https://repo.in4tree.com/2026/01/14_1768462766129.jpeg)  
  

**如果出现错误（如`[BUG#MySQL8.0.41#PHP Fatal error:  Uncaught mysqli_sql_exception: Access deniedfor user 'root'@'localhost']`），则重新安装或更换配置**


## **AWS备份快照**

**snap_ubuntu_24_20250222**  

## **Mount数据盘(/wwwroot)**


## **创建SFTP用户sftpuser**


## **安装和配置SSL**


## **修改Apache根目录**


## **修改数据库目录**


## **安装phpMyAdmin；RAR等**