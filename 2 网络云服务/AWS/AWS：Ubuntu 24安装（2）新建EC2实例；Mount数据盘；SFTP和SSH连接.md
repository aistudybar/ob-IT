
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


# ==新建EC2实例（注意：必须符合Freetier的条件）==

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437137946.jpeg)  

  
## **生成key pair，并保存到本地（推荐C:\Users\admin），用于SecureCRT配置**

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437138374.jpeg)  
![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437138743.jpeg)  

  
**空间默认8GB即可（以后可新建另一个数据盘，比如12GB，将来可随时增加）**


# **SecureCRT配置**

## **新建对话：**

用户名：ubuntu

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437138976.jpeg)

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437139290.jpeg)


## **如果有两个以上session，建议使用session setting，而不是global**  

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437139524.jpeg)  
  

**点击Export Public Key即可导出pub后缀的文件。同时把后缀pem的文件去掉后缀！！！**

# **创建Volume（数据盘）**

**注意：必须与系统盘相同的区域！大小先选12GB，以后可扩充（8GB+12GB《30GBfreetier）**

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437139734.jpeg)  
  

  
# **Mount数据盘(`/wwwroot`)**

## **创建一个vlolume（20GB），然后Attach到系统volume（8GB）**

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437139985.jpeg)  

  
## **ChatGPT: ubuntu 24.04, i attached a 2nd 12GB ebs to it,format, mount, and configure it for persistent use**

**1️⃣ Identify the New Disk**Run the following command to list available block devices:  
lsblk  

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437140231.jpeg)  
  
**2️⃣ Format the Disk (if needed)**If the disk is new and unformatted, format it with ext4(or another filesystem of your choice):  

`sudo mkfs.ext4 /dev/xvdbb  # Replace with actual device name`

**3️⃣ Create a Mount Point**Choose where to mount the new volume (e.g., /mnt/data):  

`sudo mkdir -p /wwwroot`

**4️⃣ Mount the Disk**Mount the volume to the new directory:  

`sudo mount /dev/xvdbb /wwwroot`

Verify with:  `df -h` 

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437140462.jpeg)  

  
**5️⃣ Make the Mount Persistent**  
To ensure the disk mounts automatically after a reboot,edit `/etc/fstab`: 

`sudo vi /etc/fstab`

Add this line at the bottom (replace nvme1n1with your actual device):  

`/dev/xvdbb  /wwwroot  ext4  defaults,nofail  0  2`

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437140681.jpeg)  

Save and exit, then test with:  

`sudo mount -a` 
  
That’s it! Your second 12GB EBS volume is now ready to use.  

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437140914.jpeg)  

  
## **重启验证是否安装成功**

- **能SSH登录；**
- **自动挂载20GB数据盘**


# **创建SFTP用户sftpuser（根目录/wwwroot，用户组sftpusers）**

`adduser sftpuser`

（按照提示设置密码等）


## **查看用户的用户组**

`id sftpuser`


## **修改用户组名称**

`groupmod -n sftpusers sftpuser`


## **新建并设置 /wwwroot 目录**

`mkdir -p /wwwroo`t

`sudo chown root:root /wwwroot`

`sudo chmod 755 /wwwroot`

**注意：确保目录 “/wwwroot” 归 root 所有，否则 SFTP 可能会因权限问题拒绝访问**  
  

## **修改配置文件，允许密码方式登录，并允许sftp客户端传输文件**

`vi /etc/ssh/sshd_config`

```
Match User sftpuser

   ForceCommand internal-sftp

   ChrootDirectory /wwwroot    #指定用户被锁定到此目录，为了能够chroot成功，该目录必须属主是root，并且其他用户或组不能写

   AllowTCPForwarding no

   X11Forwarding no

   PermitTunnel no

   PasswordAuthentication yes  #允许密码方式登录
```



## **重启SSH 服务**

`systemctl restart ssh`


## **测试 SFTP和SSH连接**

`sftp sftpuser@54.148.142.35`

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437141201.jpeg)

`ssh sftpuser@54.148.142.35` （应返回错误信息！只允许Key方式登录）

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437141446.jpeg)


## **查看SSH登录日志**

`tail/var/log/auth.log`

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437141696.jpeg)


**让sftpuser拥有读写Web目录中文件的权限给用户sftpuser添加另一个用户组www-data**

`usermod -a -G www-data sftpuser`


**查看用户所属的所有用户组**

`id sftpuser`

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437141972.jpeg)


**赋予sftpuser根目录下相应的子目录权限775（根目录权限必须755且用户组必须root:root！）**

`chmod -R 775 /wwwroot/html`

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437142223.jpeg)


## **验证FileZilla成功连接**

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437142471.jpeg)  

  
## **SecureFX成功连接**

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437142756.jpeg)  

  
## **WinSCP成功连接**

![Ubuntu24安装（2）新建EC2实例；Mount数据盘；SFTP和SSH连接](https://repo.in4tree.com/2026/01/14_1768437142982.jpeg)