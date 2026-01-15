搭建Windows网站开发环境：安装Apache2.4

http://localhost/discuz_pkb/forum.php?mod=viewthread&tid=15

(出处: 知识库)

**下载安装配置Apache2.4**

[https://httpd.apache.org/docs/2.4/platform/windows.html](https://httpd.apache.org/docs/2.4/platform/windows.html)

![搭建Windows网站开发环境：安装Apache2.4](https://repo.in4tree.com/2026/01/14_1768438075062.jpeg)

![搭建Windows网站开发环境：安装Apache2.4](https://repo.in4tree.com/2026/01/14_1768438075840.jpeg)

![搭建Windows网站开发环境：安装Apache2.4](https://repo.in4tree.com/2026/01/14_1768438076192.jpeg)

  

**修改网站根目录**

D:\Apache24\conf\httpd.conf

  

**Install as a service**

httpd.exe -k install  
![搭建Windows网站开发环境：安装Apache2.4](https://repo.in4tree.com/2026/01/14_1768438076585.jpeg)  
  
  

**启动自动运行ApacheMonitor**

将ApacheMonitor.exe快捷方式转移到启动目录：

C:\Users\admin\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup