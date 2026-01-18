
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

使用 cloudflare KV作为数据库,无其他依赖. 兼容静态博客的速度,以及动态博客的灵活性,方便搭建不折腾.很稳定

![image.png](https://repo.in4tree.com/2026/01/17_1768718659398.png)

![image.png](https://repo.in4tree.com/2026/01/17_1768718672649.png)

# 特点

- 使用workers提供的KV作为数据库
- 使用cloudflare缓存html来降低KV的读写
- 所有html页面均为缓存,可达到静态博客的速度
- 使用KV作为数据库,可达到wordpress的灵活性
- 后台使用markdown语法,方便快捷
- 一键发布(页面重构+缓存清理)


# 部署步骤

1. 创建workers 和KV
    - 新建一个KV(名字随意)和一个workers,并绑**定新建的KV**到**新建的workers**,变量名称`CFBLOG`注意大写,绑定后是这效果  
        
        > 补充一下绑定步骤:workers->点击刚才新建的worker—>设置—>KV 命名空间绑定—>编辑变量—>变量名称:”CFBLOG”—>KV 命名空间:选择刚才的新建的KV![](https://www.freedidi.com/wp-content/uploads/2025/10/883c0d059b20251031230754.png)
        
2. 域名设置
    - 添加一个域名DNS: 例如`blog.gezhong.vip`,IP随意,橙色云朵必须打开
    - 域名绑定到workers:域名—> workers —>添加路由 `https://blog.gezhong.vip/*`
    - 获取缓存API token:域名概述—>右下角,记录`区域ID`,以及`获取一个清理缓存的 API 令牌`,如图![](https://www.freedidi.com/wp-content/uploads/2025/10/8977d20a0b20251031230902.png)
3. 粘贴源码中index.js内容到workers,根据需求修改参数
4. 进入`/admin`进行设置 和发布文章

# 主题扩展性

可以用任意主题为参照,快速开发出新主题,默认主题在[Iconic One](https://www.freedidi.com/?golink=aHR0cHM6Ly90aGVtb25pYy5jb20vaWNvbmljLW9uZS8=&nonce=7cd34930e1 "iconic one")基础上做的,回头补充专题

# 关于评论系统

### 由于本博客的缓存效果类似静态博客,评论依赖于第三方,这里推荐`Valine`,其他的我都对比过了,大家不用去看了


# 【参考】

[Cloudflare 免费用到爽！Workers/Pages 搭建无限图床、个人导航站、博客等全搞定！ | 零度解说](https://www.youtube.com/watch?v=VrYfC85Bj0o)

搭建动态博客：[https://www.freedidi.com/21363.html](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbXo1aHNpU0k2SHhYcWtrTmdqSkduRXJsekhqQXxBQ3Jtc0tuamIyNzNmN1pQdTAzUWVSOGs2QktkcWRXYndMcGoycThORUF3cDhOLXBWVmtOOVlyZ0dfaXZ3RWsxRGZ5NzNrUHlmU1UzQ0stZlVRM2NQbExEb3NhSXdiUVVlNzlmbnA1YTBzQzJMRktQZUVlMGJnbw&q=https%3A%2F%2Fwww.freedidi.com%2F21363.html&v=VrYfC85Bj0o)
