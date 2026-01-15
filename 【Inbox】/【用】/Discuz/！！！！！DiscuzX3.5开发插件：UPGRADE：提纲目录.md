**【AI辅助编程】**

  

**提示词**

  
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

1. document.addEventListener('DOMContentLoaded', function() {
2.     ///[FIX#点击提纲条目后，高亮的条目可能不是点击的条目！]解决：加入控制变量isScrolling
3.     ///原因：点击提纲条目后，调用scrollIntoView()，滚动又触发滚动事件，然后又反过来重新定位提纲条目，从而造成可能与点击的那个条目不一致！
4.     let isScrolling = false;
5.     const button = document.getElementById('outline_toggle');
6.     if (button == null) {
7.         return;
8.     }
9.     button.addEventListener('click', function (e) {
10.         e.preventDefault();
11.         const container = document.getElementById('outline_container');
12.         const list = document.getElementById('outline_list');
13.         const content = document.getElementById('postlist');
14.         if (container.classList.contains('outline_collapsed')) {
15.             container.classList.remove('outline_collapsed');
16.             container.classList.add('outline_expanded');
17.             list.style.display = 'block';
18.             content.classList.add('content_shifted');
19.             this.textContent = '◀';  ///折叠提纲
20.         } else {
21.             container.classList.remove('outline_expanded');
22.             container.classList.add('outline_collapsed');
23.             list.style.display = 'none';
24.             content.classList.remove('content_shifted');
25.             this.textContent = '▶';    ///展开提纲
26.         }
27.     });
28.     const items = document.querySelectorAll('#outline_list li');
29.     if (items == null) {
30.         return;
31.     }
32.     items.forEach(item => {
33.         item.addEventListener('click', function (e) {
34.             e.preventDefault();
35.             isScrolling = true;
36.             // 移除所有高亮
37.             items.forEach(li => li.classList.remove('active'));
38.             // 高亮本条目
39.             this.classList.add('active');
40.             // 滚动到对应标题
41.             const targetId = this.getAttribute('data-id');
42.             const targetElement = document.getElementById(targetId);
43.             if (targetElement) {
44.                 targetElement.scrollIntoView({behavior: 'smooth'});
45.             }
46.             setTimeout(() => {
47.                 isScrolling = false; // 过一段时间后恢复监听
48.             }, 1000);
49.         });
50.     });
51.     // 监听滚动，高亮当前对应提纲标题
52.     const headers = document.querySelectorAll('.outline_item');
53.     if (headers == null) {
54.         return;
55.     }
56.     document.addEventListener("scroll", () => {
57.         if (isScrolling) return; // 如果是程序触发的滚动，则直接返回
58.         let currentHeader = headers[0];
59.         headers.forEach(header => {
60.             if (header.getBoundingClientRect().top < window.innerHeight / 10) {
61.                 currentHeader = header;
62.             }
63.         });
64.         // 移除所有高亮
65.         items.forEach(el => el.classList.remove("active"));
66.         // 高亮本条目
67.         document.querySelector(`[data-id="${currentHeader.id}"]`).classList.add("active");
68.     });
69. });

  
  
  
  
  

**【效果】**

  
![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437428887.jpeg)  
  

**【注意事项】**

  
  
1）回帖不应搜索并加id！只处理第一个postlist  
2）翻页后，如果没有原帖，则不显示提纲目录！  
  
  

**[FIX#点击提纲条目后，高亮的条目可能不是点击的条目！]**

原因：点击提纲条目后，调用scrollIntoView()，滚动又触发滚动事件，然后又反过来重新定位提纲条目，从而造成可能与点击的那个条目不一致！  
![！！！！！DiscuzX3.5开发插件：UPGRADE：提纲目录](https://repo.in4tree.com/2026/01/14_1768437429184.jpeg)