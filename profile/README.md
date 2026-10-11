## ☁️ farfarfun-drive

[farfarfun](https://github.com/farfarfun) 的**网盘 / 云存储产品线**，仓库攒够、功能做完善后从主组织独立出来的子组织。核心是一套统一的
`BaseDrive` 接口——用同一份代码操作 Google Drive、阿里云盘、百度网盘、S3、WebDAV 等
20+ 种服务，换网盘只需换一个驱动。

```python
from fundrive.drives import get_drive

drive = get_drive("lanzou")      # 换成 "alipan" / "baidu" / "webdav" … 其余代码不变
drive.login()                     # 凭据由 funsecret 统一管理
for f in drive.get_file_list("0"):
    print(f.name, f.size)
```

---

## 📦 仓库总览

### 核心框架

| 仓库 | 说明 | PyPI |
|------|------|------|
| [fundrive](https://github.com/farfarfun-drive/fundrive) | 统一网盘操作接口框架，内置 20 个驱动，含 `get_drive()` 工厂、`DriveFile` 模型与统一异常 | [![PyPI](https://img.shields.io/pypi/v/fundrive?style=flat-square)](https://pypi.org/project/fundrive/) |

### 独立驱动包

从主框架拆出来单独发版的驱动，统一走 `fundrives.*` 命名空间，按需安装、各自迭代：

| 仓库 | 网盘 | 导入路径 | PyPI |
|------|------|----------|------|
| [fundrive-alipan](https://github.com/farfarfun-drive/fundrive-alipan) | 阿里云盘 | `fundrives.alipan` | [![PyPI](https://img.shields.io/pypi/v/fundrive-alipan?style=flat-square)](https://pypi.org/project/fundrive-alipan/) |
| [fundrive-baidu](https://github.com/farfarfun-drive/fundrive-baidu) | 百度网盘 | `fundrives.baidu` | [![PyPI](https://img.shields.io/pypi/v/fundrive-baidu?style=flat-square)](https://pypi.org/project/fundrive-baidu/) |
| [fundrive-lanzou](https://github.com/farfarfun-drive/fundrive-lanzou) | 蓝奏云 | `fundrives.lanzou` | [![PyPI](https://img.shields.io/pypi/v/fundrive-lanzou?style=flat-square)](https://pypi.org/project/fundrive-lanzou/) |
| [fundrive-quark](https://github.com/farfarfun-drive/fundrive-quark) | 夸克网盘 | `fundrives.quark` | [![PyPI](https://img.shields.io/pypi/v/fundrive-quark?style=flat-square)](https://pypi.org/project/fundrive-quark/) |

### 蓝奏云专项

| 仓库 | 说明 |
|------|------|
| [funlanzou](https://github.com/farfarfun-drive/funlanzou) | 蓝奏云 Python SDK 与 PyQt6 桌面客户端：登录、上传下载、分享提取、回收站管理，并绕过上传格式与体积限制 |
| [lanzou-gui](https://github.com/farfarfun-drive/lanzou-gui) | 蓝奏云 GUI 的 fork 开发版（上游已停止维护） |

### 开发与编排

| 仓库 | 说明 |
|------|------|
| [fundrive-dev](https://github.com/farfarfun-drive/fundrive-dev) | 聚合上面 5 个包的子模块编排仓库，一次 clone 拉全产品线，供跨包联调使用 |
| [fundrive-api](https://github.com/farfarfun-drive/fundrive-api) | 占位仓库，HTTP API 形态的 fundrive，尚未开工 |
| [fundrive-web](https://github.com/farfarfun-drive/fundrive-web) | 占位仓库，Web 界面形态的 fundrive，尚未开工 |

---

## 🚀 快速开始

```bash
# 只装框架（含本地文件系统、MediaFire、OpenXLab、天池等免额外依赖的驱动）
pip install fundrive

# 按需装内置驱动的可选依赖
pip install "fundrive[google]" "fundrive[onedrive]" "fundrive[webdav]"

# 装独立驱动包
pip install fundrive-alipan fundrive-quark
```

内置驱动与独立驱动包的区别：**内置**的随 `fundrive` 一起发版，用
`fundrive[<extra>]` 装可选依赖，导入路径是 `fundrive.drives.<name>`；**独立包**单独发版，
导入路径是 `fundrives.<name>`。两者都能通过 `get_drive("<name>")` 取到。

## 🧰 支持的网盘

下面 20 个驱动均已走完「核心能力 + 高级能力 + 示例 + 规范」四项验收：

**国际**：Google Drive、OneDrive、Dropbox、Amazon S3、pCloud、MediaFire、WebDAV
**国内**：百度网盘、阿里云盘（Aligo / Open 双实现）、阿里云 OSS、蓝奏云、文叔叔
**代码托管**：GitHub、Gitee
**学术 / 数据集**：Zenodo、清华云盘、OpenXLab、天池
**本地**：本地文件系统（便于测试和统一代码路径）

外加独立包形式的夸克网盘驱动（`fundrive-quark`）。完整的驱动实现状态矩阵见
[fundrive README](https://github.com/farfarfun-drive/fundrive#支持的云存储服务)；
仓库里另有 `pan115`、`ossutil` 等尚未列入验收矩阵的在研驱动。

## 🗂️ 其他 farfarfun 组织

farfarfun 是一主多子结构：新东西默认先在主组织孵化，等某个模块仓库攒多、功能完善后独立成子组织；一开始就确定会自成一条产品线的，直接建子组织。

| 组织 | 产物 |
|------|------|
| [farfarfun](https://github.com/farfarfun) | 通用 Python 工具链：`far*` 基础库 + `fun*` 领域库 |
| [farfarfun-skill](https://github.com/farfarfun-skill) | 自研 AI Agent Skill（项目治理、服务规范、开发规范） |
| [farfarfun-skills](https://github.com/farfarfun-skills) | Skill 聚合镜像，每小时跟上游同步并镜像到 Gitee |
| [farfarfun-utools](https://github.com/farfarfun-utools) | 自研 uTools 插件 |

## 📞 联系

- 📧 **Email**: farfarfun@qq.com
- 📦 **PyPI**: [niuliangtao](https://pypi.org/user/niuliangtao/)

---

<div align="center">

**🎯 一套 API，打通所有网盘 🎯**

</div>
