<p align="center">
  <img src="https://raw.githubusercontent.com/farfarfun/.github/master/brand/png/mark/drive-128.png"
       width="80" alt="farfarfun-drive">
</p>

## ☁️ farfarfun-drive

[farfarfun](https://github.com/farfarfun) 的**网盘 / 云存储产品线**，由主组织孵化成熟后独立为子组织。核心是一套统一的
`BaseDrive` 接口：以同一份代码操作 Google Drive、阿里云盘、百度网盘、S3、WebDAV 等
20+ 种服务，切换网盘仅需更换驱动。

```python
from fundrive.drives import get_drive

drive = get_drive("lanzou")      # 替换为 "alipan" / "baidu" / "webdav" 等，其余代码不变
drive.login()                     # 凭据由 funsecret 统一管理
for f in drive.get_file_list("0"):
    print(f.name, f.size)
```

---

## 📦 仓库总览

### 核心框架

| 仓库 | 说明 | PyPI |
|------|------|------|
| [fundrive](https://github.com/farfarfun-drive/fundrive) | 统一的网盘操作接口框架，内置 20 个驱动，提供 `get_drive()` 工厂、`DriveFile` 模型与统一异常体系 | [![PyPI](https://img.shields.io/pypi/v/fundrive?style=flat-square)](https://pypi.org/project/fundrive/) |

### 独立驱动包

由主框架拆分、独立发版的驱动，统一使用 `fundrives.*` 命名空间，可按需安装并各自迭代：

| 仓库 | 网盘 | 导入路径 | PyPI |
|------|------|----------|------|
| [fundrive-alipan](https://github.com/farfarfun-drive/fundrive-alipan) | 阿里云盘 | `fundrives.alipan` | [![PyPI](https://img.shields.io/pypi/v/fundrive-alipan?style=flat-square)](https://pypi.org/project/fundrive-alipan/) |
| [fundrive-baidu](https://github.com/farfarfun-drive/fundrive-baidu) | 百度网盘 | `fundrives.baidu` | [![PyPI](https://img.shields.io/pypi/v/fundrive-baidu?style=flat-square)](https://pypi.org/project/fundrive-baidu/) |
| [fundrive-lanzou](https://github.com/farfarfun-drive/fundrive-lanzou) | 蓝奏云 | `fundrives.lanzou` | [![PyPI](https://img.shields.io/pypi/v/fundrive-lanzou?style=flat-square)](https://pypi.org/project/fundrive-lanzou/) |
| [fundrive-quark](https://github.com/farfarfun-drive/fundrive-quark) | 夸克网盘 | `fundrives.quark` | [![PyPI](https://img.shields.io/pypi/v/fundrive-quark?style=flat-square)](https://pypi.org/project/fundrive-quark/) |

### 蓝奏云专项

| 仓库 | 说明 |
|------|------|
| [funlanzou](https://github.com/farfarfun-drive/funlanzou) | 蓝奏云 Python SDK 与 PyQt6 桌面客户端，支持登录、上传下载、分享提取与回收站管理，并可突破上传格式与体积限制 |
| [lanzou-gui](https://github.com/farfarfun-drive/lanzou-gui) | 蓝奏云 GUI 的 fork 开发版本，上游已停止维护 |

### 开发与编排

| 仓库 | 说明 |
|------|------|
| [fundrive-dev](https://github.com/farfarfun-drive/fundrive-dev) | 以子模块方式聚合上述 5 个包，单次 clone 即可获取完整产品线，用于跨包联调 |
| [fundrive-api](https://github.com/farfarfun-drive/fundrive-api) | 占位仓库，规划中的 HTTP API 形态，尚未启动开发 |
| [fundrive-web](https://github.com/farfarfun-drive/fundrive-web) | 占位仓库，规划中的 Web 界面形态，尚未启动开发 |

---

## 🚀 快速开始

```bash
# 仅安装框架（含本地文件系统、MediaFire、OpenXLab、天池等无额外依赖的驱动）
pip install fundrive

# 按需安装内置驱动的可选依赖
pip install "fundrive[google]" "fundrive[onedrive]" "fundrive[webdav]"

# 安装独立驱动包
pip install fundrive-alipan fundrive-quark
```

两类驱动的区别：**内置驱动**随 `fundrive` 统一发版，通过 `fundrive[<extra>]`
安装可选依赖，导入路径为 `fundrive.drives.<name>`；**独立驱动包**单独发版，
导入路径为 `fundrives.<name>`。二者均可通过 `get_drive("<name>")` 获取。

## 🧰 支持的网盘

以下 20 个驱动均已通过「核心能力、高级能力、示例、规范」四项验收：

**国际**：Google Drive、OneDrive、Dropbox、Amazon S3、pCloud、MediaFire、WebDAV
**国内**：百度网盘、阿里云盘（Aligo / Open 双实现）、阿里云 OSS、蓝奏云、文叔叔
**代码托管**：GitHub、Gitee
**学术 / 数据集**：Zenodo、清华云盘、OpenXLab、天池
**本地**：本地文件系统（用于测试并统一代码路径）

此外还提供以独立包形式发布的夸克网盘驱动（`fundrive-quark`）。完整的驱动实现状态矩阵见
[fundrive README](https://github.com/farfarfun-drive/fundrive#支持的云存储服务)；
仓库中另有 `pan115`、`ossutil` 等在研驱动，尚未纳入验收矩阵。

## 🗂️ 其他 farfarfun 组织

farfarfun 的新项目默认在主组织孵化，当某一方向的仓库数量与功能完整度达到一定规模后，即毕业并独立为子组织；规划阶段已确定为独立产品线的，则直接建立子组织。

| 组织 | 产物 |
|------|------|
| [farfarfun](https://github.com/farfarfun) | 通用 Python 工具链，含 `far*` 基础库与 `fun*` 领域库 |
| [farfarfun-skill](https://github.com/farfarfun-skill) | 自研 AI Agent Skill，覆盖项目治理、服务规范与开发规范 |
| [farfarfun-skills](https://github.com/farfarfun-skills) | Skill 聚合镜像，每小时与上游同步并镜像至 Gitee |
| [farfarfun-utools](https://github.com/farfarfun-utools) | 自研 uTools 插件 |

## 📞 联系

- 📧 **Email**: farfarfun@qq.com
- 📦 **PyPI**: [niuliangtao](https://pypi.org/user/niuliangtao/)

---

<div align="center">

**🎯 一套 API，打通所有网盘 🎯**

</div>
