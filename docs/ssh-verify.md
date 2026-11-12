# SSH 验证记录

| 项目 | 结果 |
| --- | --- |
| 公钥文件 | `C:\Users\1\.ssh\id_ed25519.pub`（ed25519，指纹 `SHA256:dBfxr6+2ClxAeWPfoPdOee6O/8g0IzozBqE+MpA6Uiw`） |
| `ssh -T git@github.com` | `Hi w123456789-bit! You've successfully authenticated, but GitHub does not provide shell access.` |
| 远端地址 | `git@github.com:w123456789-bit/week9-ssh-lab.git`（SSH，非 HTTPS） |
| 推送结果 | `git push origin main` 成功，本地 `main` 与 `origin/main` 一致 |

本仓库只包含公钥对应的说明，私钥 `id_ed25519` 始终保存在本机 `~/.ssh`，未上传、未截图、未外发。
