# Riot Games API 公共库集合 - 中文介绍

## 目录
1. [项目简介](#项目简介)
2. [项目结构](#项目结构)
3. [支持的编程语言](#支持的编程语言)
4. [如何使用](#如何使用)
5. [如何添加你的库](#如何添加你的库)
6. [配置文件格式](#配置文件格式)
7. [标签说明](#标签说明)
8. [常见问题](#常见问题)

---

## 项目简介

本项目是 **Riot Games API 开发者社区** 的第三方库配置文件集合。这些配置文件用于驱动 Riot Games API 开发者社区 Discord 服务器中 BottyMcBotFace 机器人的 `!libs` 命令。

### 主要目的

- 为第三方库开发者提供一个**半自动化、集中化**的方式来管理其库的曝光
- 帮助其他开发者快速找到适合自己项目的 Riot API 库
- 维护一个活跃的社区库列表

### 项目来源

- **Discord 社区**: https://discord.gg/riotgamesdevrel
- **GitHub**: https://github.com/WxWatch/riot-api-libraries

---

## 项目结构

### 目录结构

```
riot-api-libraries/
├── README.md           # 英文说明文档
├── README_CN.md        # 中文说明文档（本文件）
├── schema.json         # JSON 配置文件的验证模式
├── package.json        # Node.js 项目配置
├── docs/               # 文档目录
│   ├── index.rst       # 文档首页
│   ├── libraries.rst   # 库列表文档
│   ├── applications.rst # API 申请说明
│   ├── ddragon.rst     # Data Dragon 说明
│   ├── lcu.rst         # LCU API 说明
│   └── ...             # 其他文档
├── libraries/          # 库配置文件目录
│   ├── python/         # Python 库配置
│   ├── javascript/     # JavaScript 库配置
│   ├── java/           # Java 库配置
│   ├── c-sharp/        # C# 库配置
│   ├── rust/           # Rust 库配置
│   └── ...             # 其他语言
├── docs.js             # 文档生成脚本
├── utilities.js        # 工具函数
└── validate.js         # 配置验证脚本
```

### 配置文件命名规则

- 配置文件名 = 仓库名（小写，去除所有非字母数字字符）
- 如果文件名已存在，在末尾添加数字（如 `lolfakejavalib1.json`）

---

## 支持的编程语言

本项目支持以下编程语言的 Riot API 库：

| 语言 | 目录 | 库数量 |
|------|------|--------|
| **Python** | `libraries/python/` | 多个热门库 |
| **JavaScript** | `libraries/javascript/` | 多个热门库 |
| **TypeScript** | `libraries/typescript/` | 类型安全库 |
| **Java** | `libraries/java/` | 多个库 |
| **C#** | `libraries/c-sharp/` | .NET 库 |
| **Rust** | `libraries/rust/` | 高性能库 |
| **Go** | `libraries/go/` | Go 语言库 |
| **PHP** | `libraries/php/` | PHP 库 |
| **Swift** | `libraries/swift/` | iOS/macOS 库 |
| **Kotlin** | `libraries/kotlin/` | Kotlin 库 |
| **Ruby** | `libraries/ruby/` | Ruby 库 |
| **Julia** | `libraries/julia/` | Julia 库 |
| **Elixir** | `libraries/elixir/` | Elixir 库 |
| **Perl** | `libraries/perl/` | Perl 库 |
| **C++** | `libraries/cpp/` | C++ 库 |
| **Objective-C** | `libraries/objective-c/` | Objective-C 库 |

---

## 如何使用

### 查找库

1. 浏览 `libraries/` 目录下的各语言文件夹
2. 查看对应语言的 JSON 配置文件
3. 每个配置文件包含库的基本信息、链接、标签等

### 推荐库

#### Python
- **Cassiopeia** (☆ 471) - 最受欢迎，功能完整
- **Riot-Watcher** (☆ 468) - 简单易用
- **Pyot** (☆ 83) - 异步支持，现代化设计

#### JavaScript/TypeScript
- **Twisted** (☆ 81) - 全功能，支持 LoL/TFT
- **Shieldbow** (☆ 15) - TypeScript 支持，类型安全
- **Galeforce** (☆ 31) - 多游戏支持（LoL/LOR/VAL/TFT）
- **Kayn** (☆ 134) - 老牌库，稳定可靠

#### Java
- **Orianna** (☆ 160) - 高度可配置，功能完整
- **R4J** (☆ 65) - 支持所有 Riot 游戏

#### C#
- **Camille** (☆ 77) - 自动限速，线程安全
- **RiotSharp** (☆ 288) - ASP.NET Core 支持

#### Rust
- **Riven** (☆ 76) - 高性能，自动限速

---

## 如何添加你的库

### 步骤 1：创建配置文件

在对应语言目录下创建 JSON 配置文件：

```json
{
    "owner": "你的GitHub用户名",
    "repo": "你的仓库名",
    "description": "库的描述（可选，不填会使用仓库描述）",
    "language": "编程语言",
    "links": [
        {
            "name": "文档",
            "url": "https://文档链接"
        }
    ],
    "metadata": {
        "version": "版本号"
    },
    "tags": [
        "v4",
        "rate-limiting"
    ]
}
```

### 步骤 2：提交 Pull Request

- 创建 PR 添加你的配置文件
- 如果你的语言目录不存在，可以创建
- 等待审核合并

---

## 配置文件格式

### RepoObject 属性

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `owner` | string | ✓ | GitHub 仓库拥有者 |
| `repo` | string | ✓ | 仓库名称 |
| `description` | string | 可选 | 库描述 |
| `language` | string | ✓ | 编程语言 |
| `links` | array | ✓ | 链接数组 |
| `metadata` | object | ✓ | 元数据对象 |
| `tags` | array | ✓ | 标签数组 |

### RepoLink 属性

| 属性 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | ✓ | 链接显示名称 |
| `url` | string | ✓ | 链接 URL |

---

## 标签说明

### 官方标签

| 标签 | 说明 |
|------|------|
| `v4` | 支持 Riot API v4 版本 |
| `v5` | 支持 Riot API v5 版本 |
| `lol` | 支持英雄联盟 API |
| `tft` | 支持云顶之弈 API |
| `lor` | 支符文之地传奇 API |
| `val` | 支持无畏契约 API |
| `lcu` | 支持 LCU（League Client）API |
| `ingame` | 支持游戏内 API |
| `replay` | 支持回放 API |
| `rso` | 支持 RSO（Riot Sign-On）认证 |
| `rate-limiting` | 内置速率限制处理 |
| `caching` | 内置缓存功能 |

---

## 常见问题

### Q: 如何获取 API Key？

1. 访问 https://developer.riotgames.com/
2. 注册账号后自动获得开发密钥（24小时过期）
3. 如需生产密钥，需要申请项目并等待审核（约两周）

### Q: API Key 过期怎么办？

开发密钥每 24 小时过期，需要重新获取。如果收到 403 响应，通常是密钥过期。

### Q: 如何申请生产密钥？

1. 在开发者门户点击 "Register Project"
2. 提交项目信息
3. 等待约两周审核
4. 确保项目已验证（riot.txt）

### Q: Data Dragon 是什么？

Data Dragon 是 Riot 提供的静态数据文件集合，包含：
- 英雄图片和信息
- 物品图片和信息
- 符文图片和信息
- 用于将 ID 转换为名称的数据

访问地址：
- 版本信息: https://ddragon.leagueoflegends.com/api/versions.json
- 英雄数据: https://ddragon.leagueoflegends.com/cdn/{版本}/data/zh_CN/champion.json

### Q: LCU API 是什么？

LCU (League Client Update) 是英雄联盟客户端。LCU API 允许你：
- 访问客户端内部数据
- 创建游戏房间
- 获取比赛信息
- 等等

使用要求：
- 客户端必须在本地运行
- 必须已登录

推荐工具：
- **Rift Explorer**: https://github.com/Pupix/rift-explorer
- **LCU Explorer**: https://github.com/HextechDocs/lcu-explorer

---

## 相关链接

- **Riot Games 开发者门户**: https://developer.riotgames.com/
- **社区 Discord**: https://discord.gg/riotgamesdevrel
- **官方文档**: https://developer.riotgames.com/docs/lol
- **Data Dragon**: https://ddragon.leagueoflegends.com/
- **Community Dragon**: http://raw.communitydragon.org/

---

## 免责声明

Riot API 库集合项目未得到 Riot Games 认可，不代表 Riot Games 或任何官方参与制作或管理英雄联盟的人员的观点或意见。英雄联盟和 Riot Games 是 Riot Games, Inc. 的商标或注册商标。英雄联盟 © Riot Games, Inc。

---

*翻译日期: 2026-05-25*
*翻译者: OpenClaw Assistant*