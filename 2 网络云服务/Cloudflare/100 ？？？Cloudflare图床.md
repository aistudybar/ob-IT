
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

# 利用 CF 的 Workers 创建无限的免费图床！

![image.png](https://repo.in4tree.com/2026/01/17_1768718004713.png)
![image.png](https://repo.in4tree.com/2026/01/17_1768718131725.png)

1. 支持图片审查API，可根据需要开启，开启后不良图片将自动屏蔽，不再加载
2. 1. 支持后台图片管理，日志管理，查看访问前20的Referer、IP、img,可以对上传的图片进行在线预览，添加白名单，黑名单等操作

# 免费图床开源项目：【[链接](https://github.com/x-dr/telegraph-Image?tab=readme-ov-file)】

### 利用Cloudflare pages部署

1. 点击[Use this template](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL3gtZHIvdGVsZWdyYXBoLUltYWdlL2dlbmVyYXRl&nonce=7cd34930e1)按钮创建一个新的代码库。
    
2. 登录到[Cloudflare](https://www.freedidi.com/?golink=aHR0cHM6Ly9kYXNoLmNsb3VkZmxhcmUuY29tLw==&nonce=7cd34930e1)控制台.
    
3. 在帐户主页中，选择`pages`>  `Create a project` > `Connect to Git`
    
4. 选择你创建的项目存储库，在`Set up builds and deployments`部分中，`Framework preset(框架)`选`Next.js`即可。
    

![](https://www.freedidi.com/wp-content/uploads/2025/10/872c79338420251031230402.jpg)

5. 点击`Save and Deploy`部署 。
    
6. 设置环境变量&开启图片管理功能
    
    1. 创建D1数据库 如图
    
    ![](https://www.freedidi.com/wp-content/uploads/2025/10/bb6663c2e020251031230426.png)
    
    ![](https://www.freedidi.com/wp-content/uploads/2025/10/723965462920251031230443.png)
    
    2. 执行sql命令创建表（在控制台输入框粘贴下面语句执行即可）
        
```sql
DROP TABLE IF EXISTS tgimglog;
CREATE TABLE IF NOT EXISTS tgimglog (
 `id` integer PRIMARY KEY NOT NULL,
 `url` text,
 `referer` text,
 `ip` varchar(255),
 `time` DATE
);
DROP TABLE IF EXISTS imginfo;
CREATE TABLE IF NOT EXISTS imginfo (
 `id` integer PRIMARY KEY NOT NULL,
 `url` text,
 `referer` text,
 `ip` varchar(255),
 `rating` text,
 `total` integer,
 `time` DATE
);
```
        
7. 设置兼容性标志，前往后台依次点击`设置`->`函数`->`兼容性标志`->`配置生产兼容性标志` 填写 `nodejs_compat`
    

![](https://www.freedidi.com/wp-content/uploads/2025/10/fdc1496ea220251031230511-scaled.png)

8. 前往后台点击`部署` 找到最新的一次部署点`重试部署`。

![](https://www.freedidi.com/wp-content/uploads/2025/10/09496f7c5720251031230533-scaled.png)

> 环境变量

|变量名称|值|type|
|---|---|---|
|PROXYALLIMG|反向代理所有图片（默认为false）|boolean|
|BASIC_USER|后台管理页面登录用户名称|string|
|BASIC_PASS|后台管理页面登录用户密码|string|
|ENABLE_AUTH_API|是否开启访客验证 （默认为false）|boolean|
|REGULAR_USER|普通用户 （访客验证）|string|
|REGULAR_PASS|普通用户密码|string|
|ModerateContentApiKey|审查图像内容的API key|string|
|RATINGAPI|[自建的鉴黄api](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL3gtZHIvbnNmd2pzLWFwaQ==&nonce=7cd34930e1)|string|
|CUSTOM_DOMAIN|[https://your-custom-domain.com](https://www.freedidi.com/?golink=aHR0cHM6Ly95b3VyLWN1c3RvbS1kb21haW4uY29tLw==&nonce=7cd34930e1) (自定义加速域名)|string|
|TG_BOT_TOKEN|123468:AAxxxGKrn5 (从 [@BotFather](https://www.freedidi.com/?golink=aHR0cHM6Ly90Lm1lL0JvdEZhdGhlcg==&nonce=7cd34930e1))|string|
|TG_CHAT_ID|-1234567 (频道的ID,TG Bot要是该频道或群组的管理员)|string|

> TG_BOT_TOKEN

> 获取ID机器人 [@VersaToolsBot](https://www.freedidi.com/?golink=aHR0cHM6Ly90Lm1lL1ZlcnNhVG9vbHNCb3Q=&nonce=7cd34930e1)

> `TG_CHAT_ID`为目标对话的唯一标`ID`或目标频道的用户名（eg: @channelusername），当目标对话为个人或私有频道是只能是`ID`,当为公开频道或群组是可以为目标频道的用户名（eg: `@channelusername`）



# ？？？？？图床开发：[telegraph-Image](https://github.com/x-dr/telegraph-Image?tab=readme-ov-file)（Cloudflare + Github）

1. 无限图片储存数量，你可以上传不限数量的图片；
2. 无需购买服务器，托管于Cloudflare的网络上，当使用量不超过Cloudflare的免费额度时，完全免费；
3. 无需购买域名，可以使用Cloudflare Pages提供的*.pages.dev的免费二级域名，同时也支持绑定自定义域名；
4. 支持图片审查API，可根据需要开启，开启后不良图片将自动屏蔽，不再加载；
5. 支持后台图片管理，日志管理，查看访问前20的Referer、IP、img,可以对上传的图片进行在线预览，添加白名单，黑名单等操作

### 利用Cloudflare pages部署

1. 点击[Use this template](https://github.com/x-dr/telegraph-Image/generate)按钮创建一个新的代码库。    
2. 登录到[Cloudflare](https://dash.cloudflare.com/)控制台.    
3. 在帐户主页中，选择`pages`>  `Create a project` > `Connect to Git`    
4. 选择你创建的项目存储库，在`Set up builds and deployments`部分中，`Framework preset(框架)`选`Next.js`即可。


# 【参考】

[Cloudflare 免费用到爽！Workers/Pages 搭建无限图床、个人导航站、博客等全搞定！ | 零度解说](https://www.youtube.com/watch?v=VrYfC85Bj0o)

利用 CF 的 Workers 创建无限的免费图床：[https://www.freedidi.com/21354.html](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqa2xPRFJsQ2J6bE91bXFWb0RuYmhGdXRCLUZVUXxBQ3Jtc0tuUGswUDFLVkIyenZPSm5WQVNpZFhoak1lcTcxM1pZUHlxMlVZNWc3X1hXd2d2eE5HcWt3R2FOT2RKVWlVM09fNFg4cVgwSk9vdXEtUTJhb0RublVDQ3I3VW51akpURXh6TUNjdnkwd25vcDNKVHZLUQ&q=https%3A%2F%2Fwww.freedidi.com%2F21354.html&v=VrYfC85Bj0o)
