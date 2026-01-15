
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**当本地或非SSL的PHP代码（如Discuz）使用curl访问服务端（如WordPress）时，可能由于无法验证客户端根证书导致会出现此错误！**


**解决方法一：临时跳过 SSL 验证（不推荐用于生产环境）**

```php
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, false);
```


**解决方法二：**

下载最新的证书cacert.pem存放到本地文件夹：[https://curl.se/docs/caextract.html](https://curl.se/docs/caextract.html"%20\t%20"_blank)  
在本地PHP环境配置文件php.ini中搜索"curl.cainfo"，添加：  

```php
curl.cainfo = "C:\Users\admin\cacert.pem"  
openssl.cafile = "${curl.cainfo}"
```