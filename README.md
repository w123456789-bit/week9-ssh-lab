# 第九周 · 研讨课一：SSH 密钥与 GitHub

本仓库用于记录并验证「SSH 密钥 + GitHub」配置流程：本地生成 ed25519 密钥，把公钥登记到 GitHub，把仓库的 `origin` 从 HTTPS 切换为 SSH，并完成一次 SSH 推送。

## 环境

| 项目 | 值 |
| --- | --- |
| 系统 | Windows（OpenSSH_for_Windows_9.5p2） |
| git | 2.56.0.windows.4 |
| 密钥类型 | ed25519 |
| 密钥指纹 | `SHA256:dBfxr6+2ClxAeWPfoPdOee6O/8g0IzozBqE+MpA6Uiw` |
| GitHub 账号 | `w123456789-bit` |

## 操作记录

| 检查项 | 本组记录 |
| --- | --- |
| SSH 连接测试 | `ssh -T git@github.com` → `Hi w123456789-bit! You've successfully authenticated, but GitHub does not provide shell access.` |
| 仓库链接 | `git@github.com:w123456789-bit/week9-ssh-lab.git` |
| SSH 推送结果 | `git push -u origin main` 成功（见 `git log` 与远端提交） |

## 复现步骤

```bash
# 1. 生成密钥（每人生成自己的，勿共用）
ssh-keygen -t ed25519 -C "week9-lab@$(hostname)"

# 2. 把公钥整行粘贴到 GitHub：Settings → SSH and GPG keys → New SSH key
#    公钥文件为 ~/.ssh/id_ed25519.pub，以 ssh-ed25519 开头，仅一行；
#    私钥 ~/.ssh/id_ed25519 绝不提交、截图或外发。

# 3. 验证
ssh -T git@github.com

# 4. 远端改为 SSH 后再推送
git remote set-url origin git@github.com:w123456789-bit/week9-ssh-lab.git
git remote -v
git push -u origin main
```

## 排错笔记

- `Permission denied (publickey)`：先确认公钥是否**整行**粘贴、是否粘到了正确的账号。
- 推送时仍提示输入密码：`git remote -v` 看地址是否还是 `https://`，是则执行第 4 步改回 `git@`。
