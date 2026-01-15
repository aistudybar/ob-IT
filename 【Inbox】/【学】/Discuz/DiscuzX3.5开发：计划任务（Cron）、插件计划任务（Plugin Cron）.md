**计划任务（Cron）**

**后台=》工具=》计划任务：新增一个任务cron_test：**

  
![DiscuzX3.5开发：计划任务（Cron）、插件计划任务（Plugin Cron）](https://repo.in4tree.com/2026/01/14_1768438368919.jpeg)  
  

**系统计划任务位于 source/include/cron/ 目录中，插件计划任务位于 source/plugin/插件目录/cron/ 目录中**

  
![DiscuzX3.5开发：计划任务（Cron）、插件计划任务（Plugin Cron）](https://repo.in4tree.com/2026/01/14_1768438369411.jpeg)  

**cron_test.php**

  

1. <?php
2. //cronname:mycron     计划任务名称，可写脚本语言包中的项目
3. //week:1              设置星期几执行本任务，留空为不限制
4. //day:1               设置哪一日执行本任务，留空为不限制
5. //hour:1              设置哪一小时执行本任务，留空为不限制
6. //minute:0,30         设置哪些分钟执行本任务，至多可以设置 12 个分钟值，多个值之间用半角逗号 "," 隔开，留空为不限制
7. if(!defined('IN_DISCUZ')) {
8.         exit('Access Denied');
9. }
10. global $_G;
11. // 定义日志文件路径（DiscuzX3.5的日志通常放在data/log目录下）
12. $log_dir = DISCUZ_ROOT . 'data/log/';
13. $log_file = $log_dir . 'cron_test.log';
14. // 确保日志目录存在，如果不存在则创建
15. if (!is_dir($log_dir)) {
16.     mkdir($log_dir, 0777, true);
17. }
18. // 获取当前时间
19. // $current_time = $_G['timestamp'];
20. // $current_time = date('Y-m-d H:i:s'); // 格式如：2025-03-08 15:30:45
21. // $current_time = $_G['timenow']['time'];        //////??????有时无内容！
22. // 时区标识：在PHP中，'Etc/GMT+8'表示UTC-8（注意符号是反的：+表示西时区，-表示东时区）。
23. // 你也可以使用具体地区如'America/Los_Angeles'，但要考虑夏令时影响。
24. // 夏令时：如果需要处理夏令时（如美国西海岸时间），建议使用方法2并用'America/Los_Angeles'，它会自动调整。
25. // 如果只想要固定的UTC-8偏移，则用'Etc/GMT+8'。
26. $date = new DateTime('now', new DateTimeZone('America/Los_Angeles'));        // 创建DateTime对象并设置UTC-8时区
27. $time = $date->format('Y-m-d H:i:s');        // 格式化时间
28. // 准备要写入的日志内容
29. $log_content = "UTC-8当前时间: " . $time . "\n";
30. // 写入日志文件（追加模式）
31. file_put_contents($log_file, $log_content, FILE_APPEND | LOCK_EX);
32. // 可选：返回成功信息
33. echo "时间已记录到日志文件：$log_file";

  

**插件计划任务（Plugin Cron）**

  

- 本功能为 Discuz! X3.0 新增内容
- 计划任务模块用于拓展一个计划任务项目，本模块会在插件安装时自动添加到系统计划任务中，并在插件卸载时自动从中删除

  

**脚本位置：source/plugin/插件目录/cron/cron_name.php**