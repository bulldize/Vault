# GitHub 同步配置记录

## 基本信息

- 本地 vault：`/Users/bulldize/Desktop/Obsidian`
- GitHub 远端：`github-obsidian-vault:bulldize/Vault.git`
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
- 生成 Obsidian vault 专用 deploy key：`~/.ssh/obsidian_vault_ed25519`。
- 配置专用 SSH Host：`github-obsidian-vault`。
- 在 `bulldize/Vault` 添加 deploy key 并开启 write access。
- 已成功 push `main` 到 GitHub。

## 认证过程记录

首次 HTTPS push 失败：

```text
fatal: could not read Username for 'https://github.com': Device not configured
```

随后已改为 SSH。SSH 通道可连接 `ssh.github.com:443`，但 GitHub 账号尚未登记本机 public key，因此 SSH 认证失败：

```text
git@ssh.github.com: Permission denied (publickey).
```

GitHub 公开 key 列表当前为空，说明需要先把本机 public key 添加到 GitHub 账号。

后来改用仓库专用 deploy key，避免个人 `id_ed25519` passphrase 影响定时自动化。

专用 deploy public key：

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEjpUXYT8AbQN7pE+7BM1nshjrGSw2BmLoJb16p8hiQU obsidian-vault-sync
```

指纹：

```text
SHA256:RQGZ1B58lvqiYwc0AvfAHJ1NwzTTZ65gpTDKHK6bBR0
```

## 后续处理

当前远端已正常可用。手动推送命令：

```bash
cd /Users/bulldize/Desktop/Obsidian
git push
```

3 天一次的 Codex 自动化只做本地 Git 快照与日志记录，不自动 `push`。
需要推送到远端时，必须由用户明确下达“推到远端”之类的命令。
