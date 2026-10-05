# purecanvas CLI

PureCanvas 的独立命令行工具（**仅二进制发布，仓库不含应用源码**）：

模拟器采集（截图 / 录屏 / 流程驱动 UI 导航）→ 设备外壳 → 多语言成图 → 商店规格校验 → App Preview 视频拼接。

与 PureCanvas App 内嵌 MCP 的采集桥（`capture_*` 工具）配套使用。

## 下载安装

1. 到 [Releases](../../releases/latest) 下载 `purecanvas-cli-*.zip`
2. 解压即用（包含 `purecanvas` 与 `FlowRunner/` 采集子工程）
3. 发布包已做 **Developer ID 签名 + Apple 公证**，Gatekeeper 直接放行，无需额外操作

**要求**：macOS 14+ 与完整 Xcode（流程驱动采集需要 `xcodebuild`）。

## 快速开始

```bash
./purecanvas --version
./purecanvas help
./purecanvas capture doctor                                   # 环境体检
./purecanvas capture describe --bundle-id com.example.app     # 查看实时 UI 层级
./purecanvas capture run --engine flow --flow Flows/demo.json --new-project
./purecanvas render --project App.pcanvas --out out/          # 批量成图
./purecanvas verify --dir out/                                # 商店规格校验
./purecanvas preview --clips clips/ --out preview.mov         # App Preview 视频
```

## 常驻采集后端（供 PureCanvas App / AI 客户端调用）

```bash
./purecanvas serve        # 前台运行，Ctrl-C 退出
```

启动后 PureCanvas App 的 AI 面板会显示「采集后端运行中」；AI 客户端可通过 MCP 的
`capture_status / capture_describe / capture_ui / capture_run / capture_job` 驱动采集。

## 校验下载包

```bash
shasum -a 256 purecanvas-cli-1.1.0.zip
# 5bbda1e96e48b35d699f5870d4493de8c2700d0dd1e7d1770b06e7c50bdebcc7
codesign --verify --strict purecanvas-cli-1.1.0/purecanvas   # 应通过
```

## 说明

- 本仓库仅分发发布产物；应用源码不在本仓库，也不随包分发（包内 `FlowRunner/` 为采集功能所需的 UI 测试子工程）
- 版权归作者所有；使用本工具需遵守 PureCanvas 的用户条款
