
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


source/module/forum/forum_tag.php

```php
$recent_use_tag = array();
$i = 0;
$query = C::t('common_tagitem')->select(0, 0, 'tid', 'itemid', 'DESC', 10);
foreach($query as $result) {
///[UPGRADE#取消最近使用tag数量限制为4，默认为10]
//  if($i > 4) {
//   break;
//  }
```