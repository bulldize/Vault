# GitHub 同步配置记录

## 基本信息

- 本地 vault：`/Users/bulldize/Desktop/Obsidian`
- GitHub 远端：`git@github.com:bulldize/Vault.git`
- 分支：`main`
- 首次 commit：`39bf562 Initialize Obsidian vault`

## 已完成

- 初始化本地 Git 仓库。
- 创建 `.gitignore`。
- 排除本地缓存、Obsidian UI 状态、本地 REST API secret、MCP 配置脚本。
- 创建首次 commit。
- 添加远端 `origin`。
- 配置 SSH 使用 GitHub 443 端口通道：`github.com -> ssh.github.com:443`。
- 指定 GitHub 使用本机 key：`~/.ssh/id_ed25519`。
- 将仓库远端切换为 SSH URL。

## 当前阻塞

首次 HTTPS push 失败：

```text
fatal: could not read Username for 'https://github.com': Device not configured
```

随后已改为 SSH。SSH 通道可连接 `ssh.github.com:443`，但 GitHub 账号尚未登记本机 public key，因此 SSH 认证失败：

```text
git@ssh.github.com: Permission denied (publickey).
```

GitHub 公开 key 列表当前为空，说明需要先把本机 public key 添加到 GitHub 账号。

本机 public key：

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAID5TonDlsVP4NH0M9skdgUWJfY9if68FxwfBUvrjMjDy bulldize@PERRYMHUANG-MC0
```

指纹：

```text
SHA256:isF0gfxqIJk9v2OQQIQnBkSwmpIL3up2v/r0giEYPBY
```

## 后续处理

在 GitHub 添加 SSH key 后，运行：

```bash
cd /Users/bulldize/Desktop/Obsidian
git push -u origin main
```

之后 3 天一次的 Codex 自动化会继续执行 commit + push。
