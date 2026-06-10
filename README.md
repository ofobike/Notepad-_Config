# Notepad++ 配置备份

个人 Notepad++ 开发环境配置，方便在不同电脑间同步。

## 📁 文件说明

| 文件 | 作用 |
|------|------|
| `config.xml` | 主配置文件（界面、行为、插件布局等） |
| `stylers.xml` | 样式配置文件（语法高亮、符号颜色等） |

## ⚙️ 已优化的配置项

### 显示优化
- ❌ 关闭深色模式 → 白色背景
- ❌ 隐藏行尾符（LF/CRLF）
- ❌ 隐藏空格符号（橙色点点）
- ❌ 隐藏非打印字符
- ✅ 自动换行（长行自动折行）
- ✅ 光标加宽 3px（更易定位）
- ✅ 显示行号、缩进参考线
- ✅ Tab 替换为 4 空格

### 开发功能
- ✅ 自动补全（输入 2 个字符触发）
- ✅ 括号自动配对（`()`、`[]`、`{}`、`""`）
- ✅ UTF-8 编码
- ✅ 会话记忆（关闭后恢复上次打开的文件）
- ✅ 智能高亮（选中变量自动高亮同名变量）
- ✅ 快照模式（每 7 秒自动保存临时快照）

### 自动备份
- ✅ 每次保存时自动备份到 `C:\Users\ysj\Documents\NppBackup`
- ✅ 快照模式开启，防止意外关闭丢失代码

## 🔌 推荐插件

在新电脑上通过 **插件 → Plugin Admin** 安装：

| 插件 | 用途 | 安装方式 |
|------|------|----------|
| **JSON Viewer** | JSON 格式化/压缩 | Plugin Admin 搜索安装 |
| **ComparePlus** | 文件对比，高亮差异 | Plugin Admin 搜索安装 |
| **XML Tools** | XML 格式化、校验、XPath | Plugin Admin 搜索安装 |
| **DSpellCheck** | 拼写检查 | 通常已内置 |
| **NppExport** | 导出带格式的代码 | 通常已内置 |

### 已内置功能（无需安装）
- **Function List** — 视图 → Function List，侧栏显示函数列表

## 🚀 在新电脑上配置

### 方法一：手动复制（推荐）

1. 安装 [Notepad++](https://notepad-plus-plus.org/downloads/)（64位）
2. 关闭 Notepad++
3. 找到配置目录：
   - 标准安装：`%APPDATA%\Notepad++\`
   - 便携安装：Notepad++ 安装目录本身
4. 将 `config.xml` 和 `stylers.xml` 复制到配置目录，覆盖原文件
5. 重新打开 Notepad++
6. 通过 Plugin Admin 安装推荐插件

### 方法二：PowerShell 一键配置

```powershell
# 关闭 Notepad++
Get-Process notepad++ -ErrorAction SilentlyContinue | Stop-Process -Force

# 备份原有配置
$cfgDir = "$env:APPDATA\Notepad++"
Backup-Item "$cfgDir\config.xml" -DestinationPath "$cfgDir\config.xml.bak"
Backup-Item "$cfgDir\stylers.xml" -DestinationPath "$cfgDir\stylers.xml.bak"

# 复制新配置
Copy-Item ".\config.xml" "$cfgDir\config.xml" -Force
Copy-Item ".\stylers.xml" "$cfgDir\stylers.xml" -Force

# 创建备份目录
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\Documents\NppBackup"

Write-Output "配置完成！请打开 Notepad++ 并安装推荐插件。"
```

## 📌 备份目录说明

配置中设置了自动备份目录为：
```
C:\Users\ysj\Documents\NppBackup
```

如果新电脑用户名不同，需要在 Notepad++ 中修改：
**设置 → 首选项 → 备份 → 自定义备份目录**，改为对应路径。

## 🔄 更新配置

修改 Notepad++ 设置后，更新本仓库：

```powershell
Copy-Item "$env:APPDATA\Notepad++\config.xml" ".\config.xml" -Force
Copy-Item "$env:APPDATA\Notepad++\stylers.xml" ".\stylers.xml" -Force
git add . && git commit -m "更新配置" && git push
```
