
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


# **===安装Apache===**

## **安装Apache2**

`sudo apt install apache2 -y`


## **检查 Apache 运行状态**

`sudo systemctl status apache2`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463534473.jpeg)


## **设置 Apache 开机自启**

`sudo systemctl enable apache2`


## **允许防火墙访问（可选）**

`sudo ufw allow 'ApacheFull'`


## **查看防火墙规则（缺省不启动ufw）**

`sudo ufw status`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463534926.jpeg)


**测试**

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463535133.jpeg)  

  
## **查看日志**

`cat /var/log/apache2/error.log`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463535371.jpeg)


`cat /var/log/apache2/access.log`
![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463535626.jpeg)


## **重启 Apache**

`systemctl restart apache2`
`systemctl start apache2 ` 
`systemctl stop apache2`


## **主配置文件：`vi /etc/apache2/apache2.conf`**


## **虚拟主机配置：`cd /etc/apache2/sites-available/`**


## **检查 Apache 站点启用情况：`sudo apachectl -S`**

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463535849.jpeg)


## **修改根目录方法：**

缺省目录：`/var/www/html`

Ubuntu 24.04 使用 `000-default.conf` 作为默认站点配置文件：  

80端口：`vi/etc/apache2/sites-enabled/000-default.conf`

443端口：`vi /etc/apache2/sites-available/default-ssl.conf`
![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463536089.jpeg)


443端口：`vi /etc/apache2/sites-available/000-default-le-ssl.conf`
![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463536283.jpeg)


## **新目录设置权限**

`sudo chown-R www-data:www-data /wwwroot/html/*`

网站目录权限为750，网站文件权限为640，个别目录设置可写权限770


## **修改 Apache 配置**

`vi /etc/apache2/apache2.conf`
![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463536537.jpeg)


## **如果网站使用 `.htaccess` 规则，还需要启用 `mod_rewrite`**

`sudo a2enmod rewrite`

`sudo systemctl restart apache2`



## **配置多个网站创建多个网站的文件目录，并新建 `index.html` 内容为域名**

`sudo chown -R www-data:www-data *`

网站目录权限为750，网站文件权限为640，个别目录设置可写权限770


## **创建虚拟主机配置文件**

`vi /etc/apache2/sites-available/ibrainbook.conf`
```apache
<VirtualHost *:80>

   ServerAdmin webmaster@site1.com

   ServerName ibrainbook.com

   ServerAlias www.ibrainbook.com

   DocumentRoot /wwwroot/html/ibrainbook

   <Directory /wwwroot/html/ibrainbook>

       Options -Indexes +FollowSymLinks

       AllowOverride All

       Require all granted

</Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log

   CustomLog ${APACHE_LOG_DIR}/access.log combined

RewriteEngine on

RewriteRule ^https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

</VirtualHost>  
  
vi /etc/apache2/sites-available/ebrainbook.conf  
<VirtualHost *:80>  
   ServerAdmin webmaster@site1.com  
   ServerName ebrainbook.com  
   ServerAlias www.ebrainbook.com
   DocumentRoot /wwwroot/html/ebrainbook  
  
   <Directory /wwwroot/html/ebrainbook >  
       Options -Indexes +FollowSymLinks  
       AllowOverride All  
       Require all granted  
</Directory>  
  
   ErrorLog ${APACHE_LOG_DIR}/error.log  
   CustomLog ${APACHE_LOG_DIR}/access.log combined  
  
RewriteEngine on  
RewriteRule ^https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]  
</VirtualHost>

vi /etc/apache2/sites-available/in4tag.conf

<VirtualHost *:80>

   ServerAdmin webmaster@site1.com

   ServerName in4tag.com

   ServerAlias www.in4tag.com

DocumentRoot/wwwroot/html/in4tag

   <Directory /wwwroot/html/in4tag >

       Options -Indexes +FollowSymLinks

       AllowOverride All

       Require all granted

</Directory>

   ErrorLog ${APACHE_LOG_DIR}/error.log

   CustomLog ${APACHE_LOG_DIR}/access.log combined

RewriteEngine on

RewriteRule ^https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

</VirtualHost>
```


## **禁用（默认)站点**

`sudo a2dissite 000-default.conf`

`sudo a2dissite 000-default-le-ssl.conf`

（恢复用）`sudo a2dissite ibrainbook.conf`

（恢复用）`sudo a2dissite ibrainbook-le-ssl.conf`

（恢复用）`sudo a2dissite ebrainbook.conf`

（恢复用）`sudo a2dissite ebrainbook-le-ssl.conf`

`systemctl reload apache2`


##  **启用（默认）站点**

（恢复用）`sudo a2ensite 000-default.conf`

（恢复用）`sudo a2ensite 000-default-le-ssl.conf`

`sudo a2ensite ibrainbook.conf`

`sudo a2ensite ibrainbook-le-ssl.conf`

`sudo a2ensite ebrainbook.conf`

`sudo a2ensite ebrainbook-le-ssl.conf`

`systemctl reload apache2`


# **===安装和配置SSL**

## **启用 Apache SSL 模块**

`sudo a2enmod ssl`

`sudo systemctl restart apache2`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463536751.jpeg)


## **启用 SSL（HTTPS），可以使用 `Let's Encrypt`（推荐）安装  `Certbot` **

`sudo apt update`

`sudo apt install certbotpython3-certbot-apache -y`


## **获取并安装 SSL 证书增加域名**

`certbot –-apache`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463537006.jpeg)

或

`certbot --apache -d ibrainbook.com -d www.ibrainbook.com -d ebrainbook.com -d www.ebrainbook.com`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463537213.jpeg)


## **添加证书（需要域名已经指向本AWS服务器！）**

`certbot --cert-name ibrainbook.com -d ibrainbook.com -d www.ibrainbook.com -d in4tag.com-d www.in4tag.com`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463537417.jpeg)

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463537619.jpeg)

## **删除证书**

`certbot delete --cert-name www.in4cell.com`

`certbot delete --cert-name tikard.com,in4tag.com,in4cell.com,www.tikard.com,www.in4tag.com,www.in4cell.com`


## **设置自动续期**

`sudo certbot renew --dry-run`


## **检查 `CertBot` 是否有启动**

systemctlstatus certbot.timer

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463537779.jpeg)


## **手动续期(AWS必须开放80端口！)**

`ufw allow 80`

`ufw allow 443`

`certbot renew`


## **查看过期时间**

`certbot certificates`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463537968.jpeg)


## **（可选）配置 `Apache` 的80端口自动转向443**

`vi /etc/apache2/sites-enabled/000-default.conf`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463538191.jpeg)


## **（可选）修改 `apache2 https/SSL`  端口**

`vi /etc/apache2/ports.conf`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463538381.jpeg)

`vi /etc/apache2/sites-enabled/000-default-le-ssl.conf`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463538644.jpeg)  

`netstat -tnlp`

![Ubuntu24安装（3）安装Apache、SSL](https://repo.in4tree.com/2026/01/14_1768463538832.jpeg)

