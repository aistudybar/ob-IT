
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

  
\source\class\class_tag.php  
注释掉以下代码：  

```php
///[UPGRADE#取消tag数量限制为5]
if($tagcount > 4) {
    unset($tagarray);
    break;
}
```