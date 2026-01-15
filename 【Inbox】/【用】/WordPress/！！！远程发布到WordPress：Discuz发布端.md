**【数据表】**

  

**修改数据表pre_forum_post，增加字段：wp_post_id**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437803976.jpeg)  
  

**修改数据表pre_common_setting，增加记录：plugin_remote_post_update_start_at**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437804430.jpeg)  
  

**【Discuz计划任务】自动查询未更新的post，自动上传到wordpress**

  

**后台新添一个定时任务CRON：\discuz_pkb\source\include\cron_remote_post_to_wordpress**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437804637.jpeg)  

**\discuz_pkb\remote_post_to_wordpress.inc.php**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437804882.jpeg)  
  
  

**新建插件：全局变量**

  

**/source/plugin/global_vars/admin.inc.php**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437805252.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437805784.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437806070.jpeg)  
  

**日志：\discuz_pkb\data\log\202503_remote_post_to_wordpress_log.php**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437806407.jpeg)  
  

**【UPGRADE#贴子显示页面上方添加远程发布到WordPress按钮】**

  

**template/default/forum/viewthread_node.htm**

![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437806702.jpeg)  
  

**\discuz_pkb\config\config_global.php**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437806885.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437807179.jpeg)  
  

**【UPGRADE#贴子列表页面选取框中添加远程发布到WordPress按钮】**

  

**template/default/forum/topicadmin_modlayer.htm**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437807389.jpeg)  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437807627.jpeg)  
  

**template/default/forum/topicadmin.htm**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437807855.jpeg)  

**source/include/topicadmin/topicadmin_moderate.php**

  
![！！！远程发布到WordPress：Discuz发布端](https://repo.in4tree.com/2026/01/14_1768437808048.jpeg)