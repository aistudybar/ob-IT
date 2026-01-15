
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


目前，不支持在一个文件中**同时设置 PHP 和 JavaScript 断点**。  
例如，以下代码中不能设置 JavaScript 断点： 

```html
<?php // ... ?>
<!doctype html>
<html lang="en">
<head>
<script> /* javascript 代码 */ </script>
</head>
<body>
</body>
</html>
```
 
<html lang="en">  
<head>  
<script> /* javascript 代码 */ </script>  
</head>  
<body>  
</body>  
</html>  
  
  
请将 JavaScript 代码移动到单独的.js文件中并从 HTML 中引用它：  

```html
<?php // ... ?>
<!doctype html>
<html lang="en">
<head>
<script src="index.js"></script>
</head>
<body>
</body >
</html>


```
 