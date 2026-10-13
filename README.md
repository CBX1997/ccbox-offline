# CCBox Offline

Codeman 1.41.0 + a shared API request queue, packaged for offline Linux x86_64 use with glibc 2.17.

## 下载 / Download

- [离线安装包 ccbox.tgz](https://github.com/CBX1997/ccbox-offline/releases/latest/download/ccbox.tgz)
- [安装说明](https://github.com/CBX1997/ccbox-offline/releases/latest/download/ccbox-README.txt)
- [SHA256](https://github.com/CBX1997/ccbox-offline/releases/latest/download/ccbox.tgz.sha256)
- [验证结果](https://github.com/CBX1997/ccbox-offline/releases/latest/download/ccbox-validation.txt)

## 离线安装

服务器需已有可运行的 Node.js 22+、Python 3.8+、tmux 和 Claude Code。
将压缩包导入服务器后，在 csh 中逐条执行：

```sh
tar xzf ccbox.tgz
cd ccbox
sh install.sh
```

安装过程不联网，不执行 npm/pip，不要求 root，也不替换系统 glibc。
安装器会先检查文件校验和及原生模块兼容性。

公司 API 地址是现有 Claude 配置中的 `ANTHROPIC_BASE_URL`，不是 API 密钥。
看板密码由安装者自行设置，登录用户名是 `admin`。包内不包含个人运行配置。

## 全局限流

通过本包入口启动的 Claude 会话共用滚动 300 秒最多 100 次的额度，超额排队。
额外使用 3.1 秒发起间隔，满负载约 96–97 次 / 5 分钟；首次启动等待 300 秒。
重试也计数，重启保留窗口记录。直接绕过代理的会话和其他用户的用量不在统计范围内。
现有运行会话需正常退出后从新入口恢复。

## 验证范围

本地已通过代理单元测试、PTY 测试、Codeman/tmux/模拟 API 集成和离线安装流程。
`node-pty` 的目标为 glibc 2.17，最高引用符号版本为 glibc 2.16。
尚未在用户公司的 CentOS 7.9 机器和真实公司 API 上验证；详见发布附件。

## 来源

本项目是离线集成包，不是 Codeman 官方发行版本。
上游：[Ark0N/Codeman](https://github.com/Ark0N/Codeman)。
上游依赖许可证与静态运行库许可证随压缩包保留，集成代码和测试也包含在包内。
