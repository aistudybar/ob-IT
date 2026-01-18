
---
目录：
上一页：
下一页：
关键词：
相关链接：

---

# Sink 一款简单/快速/安全的链接缩短服务，带有分析功能，100% 基于 Cloudflare 运行!

## 特点

- **URL缩短：**将您的URL压缩到最短长度。
- **分析：**监控链接分析并收集有见地的统计数据。
- **无服务器：**无需传统服务器即可部署。
- **可自定义别名：**支持个性化别名和区分大小写。
- **链接过期：**设置链接的过期日期。
-  **AI Slug：利用人工智能生成蛞蝓。**


# 在 Cloudflare Workers 上部署【**[链接直达](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL2NjYmlrYWkvU2luaw==&nonce=7cd34930e1)**】

1. 将此仓库[fork到您的 GitHub 帐户。](https://www.freedidi.com/?golink=aHR0cHM6Ly9naXRodWIuY29tL2NjYmlrYWkvU2luay9mb3Jr&nonce=7cd34930e1)    
2. 创建[KV 命名空间](https://www.freedidi.com/?golink=aHR0cHM6Ly9kZXZlbG9wZXJzLmNsb3VkZmxhcmUuY29tL2t2Lw==&nonce=7cd34930e1)（在**“存储和数据库”** -> **“KV”**下），并复制命名空间 ID。    
3. `kv_namespaces`将ID更新`wrangler.jsonc`为您自己的命名空间 ID。    
4. [在Cloudflare Workers](https://www.freedidi.com/?golink=aHR0cHM6Ly9kZXZlbG9wZXJzLmNsb3VkZmxhcmUuY29tL3dvcmtlcnMv&nonce=7cd34930e1)中创建一个项目。    
5. 选择`Sink`存储库，然后使用以下构建和部署命令：    
    - **构建命令**：`pnpm run build`或`npm run build`
    - **部署命令**：`npx wrangler deploy`
6. 保存并部署项目。    
7. 部署完成后，转到**“设置”** -> **“变量和密钥”** -> **“添加”**，并配置以下环境变量：    
    - `NUXT_SITE_TOKEN`必须至少包含**8 个**字符。此令牌用于授予您访问控制面板的权限。
    - `NUXT_CF_ACCOUNT_ID`查找您的[帐户 ID](https://www.freedidi.com/?golink=aHR0cHM6Ly9kZXZlbG9wZXJzLmNsb3VkZmxhcmUuY29tL2Z1bmRhbWVudGFscy9zZXR1cC9maW5kLWFjY291bnQtYW5kLXpvbmUtaWRzLw==&nonce=7cd34930e1)。
    - `NUXT_CF_API_TOKEN`创建一个至少具有相应权限的[Cloudflare API 令牌](https://www.freedidi.com/?golink=aHR0cHM6Ly9kZXZlbG9wZXJzLmNsb3VkZmxhcmUuY29tL2Z1bmRhbWVudGFscy9hcGkvZ2V0LXN0YXJ0ZWQvY3JlYXRlLXRva2VuLw==&nonce=7cd34930e1)`Account.Account Analytics`。[请参阅参考文档。](https://www.freedidi.com/?golink=aHR0cHM6Ly9kZXZlbG9wZXJzLmNsb3VkZmxhcmUuY29tL2FuYWx5dGljcy9hbmFseXRpY3MtZW5naW5lL3NxbC1hcGkvI2F1dGhlbnRpY2F0aW9u&nonce=7cd34930e1)
8. 启用分析引擎。在**“工作人员和页面”**中，转到右侧面板中的**“帐户详细信息” ，找到****“分析引擎”**，然后单击**“设置”**以启用免费层级。    
9. 重新部署项目。

![image.png](https://repo.in4tree.com/2026/01/17_1768717229772.png)



# 【参考】

[Cloudflare 免费用到爽！Workers/Pages 搭建无限图床、个人导航站、博客等全搞定！ | 零度解说](https://www.youtube.com/watch?v=VrYfC85Bj0o)

搭建短链接平台：[https://www.freedidi.com/21378.html](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbmtnY0ZRMUJxdGFjUFE3aGVJU3JZdlZOOERIUXxBQ3Jtc0trUTF3eTRFZFhjdUNrcWYwanBRN05LSEdCeXUwZUFIQWJTRUNnUm5kYXBuQUdzdG10d2RGZVI3Y3d2NlNSSi1YQlYyRmppRVhTZ0l6U2lDVWJNSWZPYzdOcmlORXpzbXFIUGRmSDBJVjNOOUpHNGZWQQ&q=https%3A%2F%2Fwww.freedidi.com%2F21378.html&v=VrYfC85Bj0o)

