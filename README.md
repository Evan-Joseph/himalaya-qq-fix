# himalaya-qq-fix

针对 QQ 邮箱（imap.qq.com）及其它对 IMAP 响应要求严格的服务器优化后的 Himalaya (CLI 邮件客户端) 核心库。

## ✨ 修复内容 (Patches)

1.  **IMAP 序列号正序修复 (Sequence Set Fix)**:
    - 修复了 `envelope list` 命令在获取多封邮件时发送“倒序范围”（如 `7036:7032`）导致 QQ 邮箱返回 `BAD response: Sequence set is inavlid!` 的问题。
    - 现在所有范围请求均强制使用“从小到大”的正序格式（如 `7032:7036`）。

2.  **TUI 中文字符渲染修复**:
    - 基于最新的 Rust 工具链和依赖库编译，解决了在渲染包含中文字符的邮件列表时可能出现的 `assertion failed: self.is_char_boundary(new_len)` 崩溃问题。

## 🚀 如何安装 (Build & Install)

如果你想直接在本地使用修复版本，可以克隆本项目并编译：

```bash
# 克隆仓库
git clone https://github.com/Evan-Joseph/himalaya-qq-fix.git
cd himalaya-qq-fix

# 编译 (推荐使用 Rust 1.82+)
cargo build --release --no-default-features --features imap,smtp,wizard

# 替换系统中的 himalaya 二进制文件
# (路径取决于你的编译输出，通常在 target/release/himalaya)
sudo cp target/release/himalaya /usr/local/bin/himalaya
```

## 🛠 配置建议 (Recommended Config)

在使用 QQ 邮箱或 Foxmail 时，请确保使用**授权码**作为密码，并在 `~/.config/himalaya/config.toml` 中正确配置 IMAP/SMTP 地址。

---

*Note: This repository is a patched fork of [pimalaya/core](https://github.com/pimalaya/core).*
