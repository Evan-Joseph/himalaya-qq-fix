# himalaya-qq-fix

<p align="left">
  <img src="https://img.shields.io/badge/Rust-1.82%2B-000000?style=flat-square&logo=rust" alt="Rust 1.82+" />
  <a href="https://github.com/pimalaya/core"><img src="https://img.shields.io/badge/Upstream-pimalaya%2Fcore-2f5390?style=flat-square" alt="Upstream" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green.svg?style=flat-square" alt="License: MIT" /></a>
</p>

针对腾讯企业邮 / QQ 邮箱（`imap.qq.com`）等严格校验 IMAP 序列集升序语法的邮件服务器定制修复的 Himalaya（Rust CLI 邮件客户端）核心库分支。

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

连接 QQ 邮箱等支持授权码机制的 IMAP 服务时，需在邮箱安全设置中生成客户端专用授权码作为登录密码，并在 `~/.config/himalaya/config.toml` 中配置对应的 IMAP/SMTP 端点。

## 开源许可 (License)

本仓库 Fork 自 [pimalaya/core](https://github.com/pimalaya/core)，延续上游 [MIT License](LICENSE) 开源协议。
