# himalaya-qq-fix

针对 QQ 邮箱（`imap.qq.com`）及其它对 IMAP 序列号语法要求严格的邮件服务器定制修复的 Himalaya (CLI 邮件客户端) 核心库。

## 修复内容 (Patches)

1. **IMAP 序列号正序修复 (Sequence Set Fix)**：
   - 修复了 `envelope list` 命令在拉取多封邮件时发送倒序范围（如 `7036:7032`）导致 QQ 邮箱返回 `BAD response: Sequence set is inavlid!` 的问题。
   - 所有范围请求强制归一化为升序区间（如 `7032:7036`）。

2. **TUI 中文字符渲染边界修复**：
   - 修复了渲染包含多字节 UTF-8 中文字符的邮件列表时触发 `assertion failed: self.is_char_boundary(new_len)` 越界崩溃的问题。

## 编译与安装 (Build & Install)

在本地克隆本仓库并使用 Cargo 编译：

```bash
git clone https://github.com/Evan-Joseph/himalaya-qq-fix.git
cd himalaya-qq-fix

# 编译 (推荐使用 Rust 1.82+)
cargo build --release --no-default-features --features imap,smtp,wizard

# 替换系统中的 himalaya 二进制文件
sudo cp target/release/himalaya /usr/local/bin/himalaya
```

## 配置说明 (Configuration)

连接 QQ 邮箱或 Foxmail 时，需在邮箱设置中生成**授权码**作为密码，并在 `~/.config/himalaya/config.toml` 中配置对应的 IMAP/SMTP 端点。

---

*Note: This repository is a patched fork of [pimalaya/core](https://github.com/pimalaya/core).*
