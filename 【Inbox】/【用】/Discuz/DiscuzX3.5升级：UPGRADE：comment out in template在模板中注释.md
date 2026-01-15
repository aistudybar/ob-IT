**  
[UPGRADE#comment out `<!--//` and `-->` in template]**

![DiscuzX3.5升级：UPGRADE：comment out in template在模板中注释](https://repo.in4tree.com/2026/01/14_1768437587227.jpeg)  

可注释掉：空格换行、中文等任意字符

  

**[UPGRADE#comment out `<!---` and `--->` in template]**

![DiscuzX3.5升级：UPGRADE：comment out in template在模板中注释](https://repo.in4tree.com/2026/01/14_1768437588592.jpeg)  
  
  
  

**示例：**

![DiscuzX3.5升级：UPGRADE：comment out in template在模板中注释](https://repo.in4tree.com/2026/01/14_1768437588930.jpeg)  
  
  

**后来发现BUG：subtemplate无法注释，解决：**

![DiscuzX3.5升级：UPGRADE：comment out in template在模板中注释](https://repo.in4tree.com/2026/01/14_1768437589199.jpeg)

  

**参考**

  
  

**正则表达式匹配任何中英文字符（含空格）：\w*|\W*|[\u4e00-\u9fa5]**

[http://blog.csdn.net/u011734144/article/details/52118700](http://blog.csdn.net/u011734144/article/details/52118700)

  

**正则表达式匹配任意字符：[\s\S]**

[http://blog.csdn.net/u011734144/article/details/52118700](http://blog.csdn.net/u011734144/article/details/52118700)