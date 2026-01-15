
---
目录：
上一页：
下一页：
关键词：
相关链接：

---


**AI提示词**

开发discuz 3.5 提纲插件，  
提纲放在页面左侧，默认为折叠状态，点击展开按钮后即可展开提纲，同时帖子内容框左侧留出位置区域给提纲目录；  
再次点击展开按钮后即可折叠起来，同时帖子内容框左侧恢复原位置，不再留空给提纲；  
提纲目录自动提取帖子内容中的h1、h2、h3标题内容为提纲条目；  
h1、h2、h3的提纲条目依次缩进；  
点击提纲条目，则高亮该条目，然后自动滚动右侧到对应的内容，但左侧提纲保持不动。  
  

**比较Grok、ChatGPT、DeepSeek**


- 三个都无法生成正确的discuzX3.5插件的PHP代码！
- Grok的JS、CSS比较优美可行！


**【创建新插件：outline】**
  
![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437427536.jpeg)  

  
**【插件模板文件】**

**注意：无法在页面嵌入钩子PHP代码中加载插件模板文件！只能修改Discuz模板、插入子模版代码。**

在 template/default/forum/viewthread.htm 页面嵌入插件模板文件：  
![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437427976.jpeg)  
  
source/plugin/outline/template/outline.htm  
![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437428234.jpeg)  

  
**【页面嵌入钩子PHP代码】**

**加载插件JS和CSS**

![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437428432.jpeg)  
  

**获取帖子H标题，生成提纲目录**

![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437428692.jpeg)  

  
**【插件JS文件】**

```js
document.addEventListener('DOMContentLoaded', function() {
  ///[FIX#点击提纲条目后，高亮的条目可能不是点击的条目！]解决：加入控制变量isScrolling
  ///原因：点击提纲条目后，调用scrollIntoView()，滚动又触发滚动事件，然后又反过来重新定位提纲条目，从而造成可能与点击的那个条目不一致！
  let isScrolling = false;
  const button = document.getElementById('outline_toggle');
  if (button == null) {
  return;
  }
  button.addEventListener('click', function (e) {
   e.preventDefault();
   const container = document.getElementById('outline_container');
   const list = document.getElementById('outline_list');
   const content = document.getElementById('postlist');
   if (container.classList.contains('outline_collapsed')) {
     container.classList.remove('outline_collapsed');
     container.classList.add('outline_expanded');
     list.style.display = 'block';
     content.classList.add('content_shifted');
     this.textContent = '◀';///折叠提纲
   } else {
     container.classList.remove('outline_expanded');
     container.classList.add('outline_collapsed');
     list.style.display = 'none';
     content.classList.remove('content_shifted');
     this.textContent = '▶';  ///展开提纲
   }
   });
   const items = document.querySelectorAll('#outline_list li');
   if (items == null) {
   return;
   }
   items.forEach(item => {
   item.addEventListener('click', function (e) {
     e.preventDefault();
     isScrolling = true;
     // 移除所有高亮
     items.forEach(li => li.classList.remove('active'));
     // 高亮本条目
     this.classList.add('active');
     // 滚动到对应标题
     const targetId = this.getAttribute('data-id');
     const targetElement = document.getElementById(targetId);
     if (targetElement) {
       targetElement.scrollIntoView({behavior: 'smooth'});
     }
     setTimeout(() => {
       isScrolling = false; // 过一段时间后恢复监听
     }, 1000);
   });
  });
  // 监听滚动，高亮当前对应提纲标题
  const headers = document.querySelectorAll('.outline_item');
  if (headers == null) {
  return;
  }
  document.addEventListener("scroll", () => {
  if (isScrolling) return; // 如果是程序触发的滚动，则直接返回
  let currentHeader = headers[0];
  headers.forEach(header => {
    if (header.getBoundingClientRect().top < window.innerHeight / 10) {
      currentHeader = header;
    }
  });
  // 移除所有高亮
  items.forEach(el => el.classList.remove("active"));
  // 高亮本条目
  document.querySelector(`[data-id="${currentHeader.id}"]`).classList.add("active");
  });
});
```


**【效果】**

![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437428887.jpeg)  
  

**【注意事项】**

1）回帖不应搜索并加id！只处理第一个postlist  
2）翻页后，如果没有原帖，则不显示提纲目录！  

  
# \[FIX#点击提纲条目后，高亮的条目可能不是点击的条目！]

原因：点击提纲条目后，调用scrollIntoView()，滚动又触发滚动事件，然后又反过来重新定位提纲条目，从而造成可能与点击的那个条目不一致！  
![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437429184.jpeg)