
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


# **【数据表】**

**修改数据表pre_forum_post，增加字段：wp_post_id**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437447870.jpeg)  
  

**修改数据表pre_common_setting，增加记录：plugin_remote_post_update_start_at**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437448294.jpeg)  
  

# **【Discuz计划任务】自动查询未更新的post，自动上传到wordpress**

**后台新添一个定时任务CRON：\discuz_pkb\source\include\cron_remote_post_to_wordpress**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437448550.jpeg)  


**\discuz_pkb\remote_post_to_wordpress.inc.php**
  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437448795.jpeg)  

  
**新建插件：全局变量**

**/source/plugin/global_vars/admin.inc.php**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437449022.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437449245.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437449520.jpeg)  
  

**日志：\discuz_pkb\data\log\202503_remote_post_to_wordpress_log.php**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437449779.jpeg)  

  
# **【UPGRADE#贴子显示页面上方添加远程发布到WordPress按钮】**

**template/default/forum/viewthread_node.htm**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437450055.jpeg)  
  

**\discuz_pkb\config\config_global.php**
  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437450274.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437450526.jpeg)  
  

# **【UPGRADE#贴子列表页面选取框中添加远程发布到WordPress按钮】**

**template/default/forum/topicadmin_modlayer.htm**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437450765.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437450974.jpeg)  
  

**template/default/forum/topicadmin.htm**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437451170.jpeg)  


**source/include/topicadmin/topicadmin_moderate.php**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437451384.jpeg)