# book诗意

个人博客，基于 Hexo + NexT 主题。

## 技术栈

- **框架**: [Hexo](https://hexo.io) 8
- **主题**: [NexT](https://theme-next.js.org) 8.28
- **包管理**: pnpm 11
- **部署**: Cloudflare Pages
- **图片**: Cloudflare R2（`assets.bookshiyi.com`）

## 本地开发

```bash
pnpm install
pnpm run build    # 生成静态文件
pnpm run clean    # 清理生成文件
```

## 目录结构

```
source/_posts/     # 文章 Markdown 源文件
source/index/      # 主页
source/project/    # 项目页
_config.yml        # Hexo 配置
_config.next.yml   # NexT 主题配置
```

## 部署

推送 `main` 分支到 GitHub，Cloudflare Pages 自动构建部署。
