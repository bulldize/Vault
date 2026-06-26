# GitHub 同步配置记录

## 基本信息

- 本地 vault：`/Users/bulldize/Desktop/Obsidian`
- GitHub 远端：`https://github.com/bulldize/Vault.git`
- 分支：`main`
- 首次 commit：`39bf562 Initialize Obsidian vault`

## 已完成

- 初始化本地 Git 仓库。
- 创建 `.gitignore`。
- 排除本地缓存、Obsidian UI 状态、本地 REST API secret、MCP 配置脚本。
- 创建首次 commit。
- 添加远端 `origin`。

## 当前阻塞

首次 push 失败：

```text
fatal: could not read Username for 'https://github.com': Device not configured
```

原因：当前机器没有可用的 GitHub HTTPS 凭据。`gh auth status` 也显示未认证或不可用。

## 后续处理

完成 GitHub 凭据配置后，运行：

```bash
cd /Users/bulldize/Desktop/Obsidian
git push -u origin main
```

之后 3 天一次的 Codex 自动化会继续执行 commit + push。
