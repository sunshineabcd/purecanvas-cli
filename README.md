# purecanvas CLI (v1.2.0)

PureCanvas 的独立命令行工具（**仅二进制发布，仓库不含应用源码**）：

SwiftUI 全工程免模拟器代码快拍（`preview-shot`） / 模拟器采集（截图 / 录屏 / 流程驱动 UI 导航）→ 设备外壳 → 多语言成图 → 商店规格校验 → App Preview 视频拼接。

与 PureCanvas App 内嵌 MCP 的采集桥（`capture_*` / `preview_shot` 工具）配套使用。

## 下载安装

### 方式一：Homebrew（推荐）

```bash
brew tap sunshineabcd/tap
brew install purecanvas
```

### 方式二：直装（免 Homebrew）

```bash
curl -fsSL https://github.com/sunshineabcd/purecanvas-cli/raw/v1.2.0/purecanvas-cli-1.2.0.zip -o /tmp/purecanvas-cli.zip && mkdir -p ~/.local ~/.local/bin && ditto -x -k /tmp/purecanvas-cli.zip ~/.local && ln -sf ~/.local/purecanvas-cli-1.2.0/purecanvas ~/.local/bin/purecanvas
```

**要求**：macOS 14+ 与完整 Xcode（原生编译快拍 `preview-shot` 与流程驱动采集需要 `xcrun` / `xcodebuild`）。

## 快速开始

```bash
./purecanvas --version
./purecanvas help

# 免模拟器 SwiftUI 全工程多语言 × 全设备快拍（支持 iphone / iphone-duo / ipad / mac / watch）
./purecanvas preview-shot \
  --views /path/to/YourSwiftUIProject \
  [--mock-data /path/to/mock.json] \
  --device iphone,iphone-duo,ipad,mac,watch \
  --lang zh-Hans,en,ja \
  --out ./shots

# 模拟器采集与自动化排版
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
`preview_shot / capture_status / capture_describe / capture_ui / capture_run / capture_job` 驱动快拍与采集。

## 校验下载包

```bash
shasum -a 256 purecanvas-cli-1.2.0.zip
# 5114ea077f2753875929a2a96a5fb7940b8353a16537cce7aaf361f9fc6a9024
```

## 说明

- 本仓库仅分发发布产物；应用源码不在本仓库，也不随包分发（包内 `FlowRunner/` 为采集功能所需的 UI 测试子工程）
- 版权归作者所有；使用本工具需遵守 PureCanvas 的用户条款
