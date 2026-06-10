# Notepad++ 个人开发环境配置

> 一套开箱即用的 Notepad++ 开发配置，适用于日常编码、SQL 开发、JSON/XML 处理。
> 支持一键部署到新电脑，告别重复配置。

**适用版本**：Notepad++ 8.x+ （64位）

---

## 目录

- [快速开始](#-快速开始)
- [配置文件说明](#-配置文件说明)
- [显示优化](#-显示优化)
- [开发功能](#-开发功能)
- [备份策略](#-备份策略)
- [推荐插件](#-推荐插件)
- [新电脑部署](#-新电脑部署)
- [同步更新](#-同步更新)
- [常见问题](#-常见问题)

---

## 🚀 快速开始

```powershell
# 1. 克隆仓库
git clone https://github.com/ofobike/Notepad-_Config.git
cd Notepad-_Config

# 2. 关闭 Notepad++
Get-Process notepad++ -ErrorAction SilentlyContinue | Stop-Process -Force

# 3. 复制配置文件（标准安装路径）
$cfgDir = "$env:APPDATA\Notepad++"
Copy-Item ".\config.xml" "$cfgDir\config.xml" -Force
Copy-Item ".\stylers.xml" "$cfgDir\stylers.xml" -Force

# 4. 创建备份目录
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\Documents\NppBackup"

# 5. 打开 Notepad++，通过 Plugin Admin 安装插件
Write-Output "✅ 配置完成！请打开 Notepad++ 并安装推荐插件。"
```

---

## 📁 配置文件说明

| 文件 | 位置 | 作用 |
|------|------|------|
| `config.xml` | `%APPDATA%\Notepad++\` | 主配置：界面布局、行为设置、插件位置、备份策略 |
| `stylers.xml` | `%APPDATA%\Notepad++\` | 样式配置：语法高亮颜色、符号显示颜色、字体设置 |

**注意**：便携版 Notepad++ 的配置文件在安装目录本身，不在 AppData。

---

## 👁️ 显示优化

告别杂乱的编辑界面，专注于代码本身：

| 配置项 | 修改前 | 修改后 | 说明 |
|--------|--------|--------|------|
| 深色模式 | 开启 | **关闭** | 白色背景，长时间编码更舒适 |
| 行尾符 (LF/CRLF) | 显示 | **隐藏** | 不再每行末尾显示 LF 标记 |
| 空格符号 | 显示（橙色点） | **隐藏** | 空格不再显示为点点 |
| 非打印字符 | 显示 | **隐藏** | 隐藏不可见控制字符 |
| 自动换行 | 关闭 | **开启** | 长行自动折行，无需横向滚动 |
| 光标宽度 | 2px | **3px** | 光标更明显，快速定位当前位置 |
| 行号 | 显示 | 保持 | 方便调试定位 |
| 缩进参考线 | 显示 | 保持 | 可视化缩进层级 |
| Tab 设置 | - | 4 空格 | Tab 键输入 4 个空格，保持代码风格一致 |

---

## 🛠️ 开发功能

提升编码效率的智能功能：

| 功能 | 说明 |
|------|------|
| **自动补全** | 输入 2 个字符即触发补全提示，支持单词和函数补全 |
| **括号自动配对** | 输入 `(` 自动补 `)`，支持 `()` `[]` `{}` `""` |
| **UTF-8 编码** | 新建文件默认 UTF-8 编码，避免中文乱码 |
| **会话记忆** | 关闭 Notepad++ 后重新打开，自动恢复上次的文件和标签 |
| **智能高亮** | 选中一个变量，同名变量自动高亮显示 |
| **快照模式** | 每 7 秒自动保存临时快照，意外关闭不丢失代码 |
| **HTML/XML 标签配对** | 输入 `<div>` 自动补 `</div>` |

---

## 💾 备份策略

采用双重备份机制，确保代码安全：

### 第一层：快照备份
- **频率**：每 7 秒自动保存
- **位置**：Notepad++ 内部临时目录
- **场景**：意外断电、程序崩溃

### 第二层：保存时备份
- **频率**：每次手动保存时
- **位置**：`C:\Users\ysj\Documents\NppBackup`
- **场景**：误操作覆盖、需要回退历史版本

### ⚠️ 新电脑注意
备份目录路径包含用户名，新电脑需要修改：
**设置 → 首选项 → 备份 → 自定义备份目录** → 改为新电脑的路径

---

## 🔌 推荐插件

### 必装插件（通过 Plugin Admin 安装）

菜单：**插件 → Plugin Admin → Available**

| 插件 | 用途 | 快捷操作 |
|------|------|----------|
| **JSON Viewer** | JSON 格式化/压缩/验证 | 选中文本 → Plugins → JSON Viewer → Format JSON |
| **ComparePlus** | 两个文件差异对比 | 打开两个文件 → Plugins → ComparePlus → Compare |
| **XML Tools** | XML 格式化、校验、XPath 查询 | Plugins → XML Tools → Pretty Print |

### 已内置功能（无需安装）

| 功能 | 入口 | 说明 |
|------|------|------|
| **Function List** | 视图 → Function List | 侧栏显示当前文件的函数/方法列表，点击跳转 |
| **列编辑** | Alt + 鼠标选择 | 矩形选择，批量编辑 |
| **宏录制** | 宏 → 开始录制 | 录制重复操作，一键回放 |

### 其他已有插件

| 插件 | 说明 |
|------|------|
| DSpellCheck | 拼写检查（通常已内置） |
| NppExport | 导出带语法高格的 RTF/HTML 代码 |
| NppConverter | 编码转换工具 |
| mimeTools | MIME 编解码工具 |

---

## 💻 新电脑部署

### 方法一：PowerShell 一键脚本（推荐）

```powershell
# ===== Notepad++ 配置一键部署 =====
# 前提：已安装 Notepad++ 64位

# 1. 关闭 Notepad++
Get-Process notepad++ -ErrorAction SilentlyContinue | Stop-Process -Force
Start-Sleep -Seconds 2

# 2. 定位配置目录
$cfgDir = "$env:APPDATA\Notepad++"
if (-not (Test-Path $cfgDir)) {
    Write-Error "未找到 Notepad++ 配置目录，请确认已安装 Notepad++"
    exit 1
}

# 3. 备份原有配置（如果存在）
if (Test-Path "$cfgDir\config.xml") {
    Copy-Item "$cfgDir\config.xml" "$cfgDir\config.xml.bak" -Force
    Write-Output "已备份原 config.xml"
}
if (Test-Path "$cfgDir\stylers.xml") {
    Copy-Item "$cfgDir\stylers.xml" "$cfgDir\stylers.xml.bak" -Force
    Write-Output "已备份原 stylers.xml"
}

# 4. 复制新配置
Copy-Item ".\config.xml" "$cfgDir\config.xml" -Force
Copy-Item ".\stylers.xml" "$cfgDir\stylers.xml" -Force
Write-Output "✅ 配置文件已复制"

# 5. 创建备份目录
$backupDir = "$env:USERPROFILE\Documents\NppBackup"
New-Item -ItemType Directory -Force -Path $backupDir | Out-Null
Write-Output "✅ 备份目录已创建：$backupDir"

# 6. 提醒安装插件
Write-Output ""
Write-Output "=========================================="
Write-Output "  配置完成！请执行以下步骤："
Write-Output "  1. 打开 Notepad++"
Write-Output "  2. 插件 → Plugin Admin → Available"
Write-Output "  3. 安装：JSON Viewer、ComparePlus、XML Tools"
Write-Output "  4. 设置 → 首选项 → 备份 → 修改备份目录"
Write-Output "=========================================="
```

### 方法二：手动复制

1. 安装 [Notepad++](https://notepad-plus-plus.org/downloads/)（选择 64 位）
2. **完全关闭** Notepad++（任务栏右键 → 退出）
3. 打开配置目录：
   - 按 `Win + R`，输入 `%APPDATA%\Notepad++`，回车
4. 将本仓库的 `config.xml` 和 `stylers.xml` 复制进去，覆盖原文件
5. 重新打开 Notepad++
6. 安装插件：**插件 → Plugin Admin → Available** → 搜索安装

---

## 🔄 同步更新

在任意电脑上修改了 Notepad++ 配置后，同步到仓库：

```powershell
# 从 Notepad++ 复制最新配置
$cfgDir = "$env:APPDATA\Notepad++"
Copy-Item "$cfgDir\config.xml" ".\config.xml" -Force
Copy-Item "$cfgDir\stylers.xml" ".\stylers.xml" -Force

# 提交并推送
git add .
git commit -m "更新配置：$(Get-Date -Format 'yyyy-MM-dd')"
git push
```

在其他电脑拉取更新：

```powershell
git pull
# 然后重新执行部署脚本
```

---

## ❓ 常见问题

### Q: 深色模式想改回来？
编辑 `config.xml`，找到 `<GUIConfig name="DarkMode"`，将 `enable="no"` 改为 `enable="yes"`

### Q: 想显示行尾符？
菜单：**视图 → 显示符号 → 勾选 "显示行尾符"**

### Q: 自动补全不生效？
**设置 → 首选项 → 自动完成** → 确认勾选"启用自动完成"，触发字符数设为 2

### Q: 便携版 Notepad++ 怎么配置？
便携版配置文件在 Notepad++ 安装目录本身，直接复制 `config.xml` 和 `stylers.xml` 到安装目录即可

### Q: 备份目录路径不对？
**设置 → 首选项 → 备份** → 修改"自定义备份目录"为你的实际路径

---

## 📋 配置变更日志

| 日期 | 变更内容 |
|------|----------|
| 2026-06-10 | 初始配置：关闭深色模式、隐藏符号显示、开启自动备份、安装开发插件 |

---

## 📄 License

MIT - 自由使用和修改
