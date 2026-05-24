# Riot Games API 开发指南 - 中文翻译

---

## 一、API 申请说明

### 1.1 开发密钥 vs 生产密钥

| 类型 | 过期时间 | 申请方式 | 使用场景 |
|------|---------|---------|---------|
| **开发密钥** | 24小时 | 自动获得 | 测试、开发 |
| **生产密钥** | 永久 | 申请审核 | 正式项目 |
| **个人密钥** | 永久 | 申请（无需验证） | 个人项目 |

### 1.2 申请流程

#### 开发密钥
1. 注册 https://developer.riotgames.com/
2. 自动获得开发密钥
3. 每天需要刷新（过期后重新获取）

#### 生产密钥
1. 在开发者门户点击 "Register Project"
2. 填写项目信息
3. 上传 riot.txt 进行验证
4. 等待审核（约两周，10个工作日）
5. 审核通过后获得生产密钥

#### 个人密钥
- 仅用于标准 API，不支持锦标赛 API
- 需要详细的项目描述
- 无需验证流程

### 1.3 注意事项

- **不要在测试阶段申请生产密钥**
- 生产密钥需要有**可工作的原型**
- 申请期间修改项目会重新排队
- 超过两周未收到回复，可在 Discord 咨询 Guru

### 1.4 获取 App ID

访问 https://developer.riotgames.com/apps，选择项目，URL中的数字即为 App ID。

---

## 二、Data Dragon 使用指南

### 2.1 什么是 Data Dragon？

Data Dragon（ddragon）是 Riot 提供的**静态数据文件集合**：

- 英雄图片和数据
- 物品图片和数据
- 符文图片和数据
- 将 ID 转换为名称的映射表

### 2.2 数据获取方式

#### 下载完整数据包

```
https://ddragon.leagueoflegends.com/cdn/dragontail-{版本}.tgz
```

文件大小约 1GB，包含所有图片和数据。

#### 单文件访问

```
https://ddragon.leagueoflegends.com/cdn/{版本}/data/{语言}/champion.json
```

示例：
```
https://ddragon.leagueoflegends.com/cdn/12.6.1/data/zh_CN/champion.json
```

### 2.3 获取最新版本

```
https://ddragon.leagueoflegends.com/api/versions.json
```

返回版本列表，第一个为最新版本。

### 2.4 区域版本

不同区域可能使用不同版本，检查区域版本：

```
https://ddragon.leagueoflegends.com/realms/{区域}.json
```

如北美：`https://ddragon.leagueoflegends.com/realms/na.json`

### 2.5 支持的语言

完整语言列表：https://ddragon.leagueoflegends.com/cdn/languages.json

常用语言：
- `zh_CN` - 简体中文（中国）
- `zh_TW` - 繁体中文（台湾）
- `ja_JP` - 日语（日本）
- `en_US` - 英语（美国）
- `ko_KR` - 韩语（韩国）

### 2.6 缓存建议

- Data Dragon 数据只在新版本发布时更新
- 建议缓存到本地，减少网络请求
- 可显著提升应用性能

### 2.7 Community Dragon

如果 Data Dragon 没有你需要的数据，查看 **Community Dragon**：

```
http://raw.communitydragon.org/
```

这是社区生成的补充数据，包含更多内容。

### 2.8 常见问题

#### 英雄内部名称

Wukong 的内部名称是 `monkeyking`。查看 `champion.json` 中的 `key` 属性获取所有英雄的内部名称。

#### 数据不准确

Data Dragon 的部分数据（特别是技能数据）可能不准确。建议使用 [League Wikia](https://leagueoflegends.fandom.com/wiki/League_of_Legends_Wiki) 查找准确数据。

#### 新版本未更新

新补丁发布后，Data Dragon 可能需要 1-2 天才更新。

---

## 三、LCU API 使用指南

### 3.1 什么是 LCU？

LCU (League Client Update) = 英雄联盟客户端

LCU API 允许你访问客户端的内部功能：
- 创建/管理游戏房间
- 获取当前比赛信息
- 查看好友列表
- 修改客户端设置

### 3.2 使用条件

- **客户端必须在本地运行**
- **必须已登录**
- 需要在开发者门户创建应用说明你的使用方式

### 3.3 可用端点

官方允许使用的端点列表：
https://developer.riotgames.com/league-client-apis.html

### 3.4 探索工具

#### Rift Explorer
https://github.com/Pupix/rift-explorer

可视化探索 LCU 端点的工具。

#### LCU Explorer
https://github.com/HextechDocs/lcu-explorer

由 Hi-Ray 和 MingweiSamuel 创建的替代工具。

#### Vivi 的 Swagger 网站
http://lcu.vivide.re/

在线查看 LCU 端点的 Swagger 文档。

### 3.5 常用技巧

#### 无登录模式

启动客户端时添加参数：
```
--mode unattended
```

允许在无头服务器上使用部分 LCU 端点。

#### 创建游戏房间

**普通游戏房间**：
```json
POST /lol-lobby/v2/lobby
{
  "queueId": 430
}
```

**自定义游戏房间**：
```json
POST /lol-lobby/v2/lobby
{
  "customGameLobby": {
    "configuration": {
      "gameMode": "PRACTICETOOL",
      "gameMutator": "",
      "gameServerRegion": "",
      "mapId": 11,
      "mutators": {"id": 1},
      "spectatorPolicy": "AllAllowed",
      "teamSize": 5
    },
    "lobbyName": "房间名",
    "lobbyPassword": null
  },
  "isCustom": true
}
```

将 `PRACTICETOOL` 改为 `CLASSIC` 可创建普通自定义房间。

#### Linux Wine 运行

- 设置 Wine prefix 为 Windows XP
- 需要 wine-staging 版本
- 用于兼容反作弊系统

#### 有用的启动参数

```
--app-port=1337 --headless --allow-multiple-clients
```

---

## 四、ID 转换指南

### 4.1 英雄 ID

使用 Data Dragon 的 `champion.json` 将英雄 ID 转换为名称：

```
https://ddragon.leagueoflegends.com/cdn/{版本}/data/zh_CN/champion.json
```

### 4.2 物品 ID

使用 Data Dragon 的 `item.json`：

```
https://ddragon.leagueoflegends.com/cdn/{版本}/data/zh_CN/item.json
```

### 4.3 符文 ID

使用 Data Dragon 的 `runesReforged.json`：

```
https://ddragon.leagueoflegends.com/cdn/{版本}/data/zh_CN/runesReforged.json
```

### 4.4 队列 ID

常见队列 ID：

| ID | 类型 |
|-----|------|
| 400 | 5v5 Draft Pick |
| 420 | 5v5 Ranked Solo |
| 430 | 5v5 Blind Pick |
| 440 | 5v5 Ranked Flex |
| 450 | ARAM |

完整列表参考官方文档。

---

## 五、速率限制

### 5.1 Riot API 速率限制

Riot API 有严格的速率限制：

- **应用限制**: 每个应用的全局限制
- **方法限制**: 每个端点的限制

### 5.2 响应头

API 响应包含速率限制信息：

```
X-RateLimit-Type: application
X-RateLimit-Limit: 100:120,20:1
X-ateLimit-Count: 1:120,1:1
X-RateLimit-Remaining: 99:120,19:1
```

### 5.3 处理建议

- 使用带有 `rate-limiting` 标签的库
- 库会自动处理速率限制和重试
- 避免手动处理，容易出错

---

## 六、推荐库详解

### 6.1 Python 库

#### Cassiopeia (☆ 471)

**特点**：
- 最受欢迎的 Python 库
- 自动处理所有细节
- 内置速率限制和缓存
- 让你专注于应用开发

**安装**：
```bash
pip install cassiopeia
```

**链接**：
- PyPI: https://pypi.org/project/cassiopeia/
- 文档: http://cassiopeia.readthedocs.org/en/latest/

#### Riot-Watcher (☆ 468)

**特点**：
- 简单易用
- 轻量级设计
- 内置速率限制

**安装**：
```bash
pip install riotwatcher
```

**链接**：
- 文档: http://riot-watcher.readthedocs.io/en/latest/
- PyPI: https://pypi.python.org/pypi/riotwatcher

#### Pyot (☆ 83)

**特点**：
- 基于 AsyncIO
- 现代化设计
- 支持 Django 集成
- 多游戏支持

**安装**：
```bash
pip install pyot
```

**链接**：
- PyPI: https://pypi.org/project/pyot/
- 文档: https://pyot.paaksing.com/

### 6.2 JavaScript/TypeScript 库

#### Twisted (☆ 81)

**特点**：
- 全功能支持
- 支持 LoL 和 TFT
- 内置速率限制和缓存

**安装**：
```bash
npm install twisted
```

#### Shieldbow (☆ 15)

**特点**：
- TypeScript 类型支持
- 易于使用
- 多版本支持（v4, v5）

**安装**：
```bash
npm install shieldbow
```

#### Galeforce (☆ 31)

**特点**：
- 多游戏支持（LoL, LOR, VAL, TFT）
- TypeScript fluent interface
- Promise-based

**安装**：
```bash
npm install galeforce
```

### 6.3 Java 库

#### Orianna (☆ 160)

**特点**：
- 高度可配置
- 易用性优先
- 内置速率限制和缓存

**Maven**：
```xml
<dependency>
  <groupId>com.merakianalytics.orianna</groupId>
  <artifactId>orianna</artifactId>
  <version>最新版本</version>
</dependency>
```

**链接**：
- Maven: https://search.maven.org/search?q=g:com.merakianalytics.orianna
- 文档: http://orianna.readthedocs.org/en/latest/

### 6.4 C# 库

#### Camille (☆ 77)

**特点**：
- 完全速率限制
- 自动重试
- 线程安全
- 每晚自动发布

**NuGet**：
```
Install-Package MingweiSamuel.Camille
```

#### RiotSharp (☆ 288)

**特点**：
- ASP.NET Core 支持
- 内置速率限制

**注意**：NuGet 版本可能过旧，建议直接使用源码。

---

## 七、常见错误排查

### 7.1 403 Forbidden

**原因**：API Key 过期

**解决**：刷新开发密钥或检查生产密钥状态

### 7.2 404 Not Found

**原因**：
- URL 路径错误
- 数据不存在（如玩家未玩过某英雄）

**解决**：检查 API 端点拼写和参数

### 7.3 429 Too Many Requests

**原因**：超出速率限制

**解决**：
- 使用带速率限制的库
- 检查响应头的限制信息
- 等待后重试

### 7.4 数据不准确

**原因**：Data Dragon 数据可能不完整或过时

**解决**：
- 使用 Community Dragon
- 参考 League Wikia
- 在 Discord 咨询

---

## 八、社区资源

### 8.1 Discord 社区

https://discord.gg/riotgamesdevrel

频道：
- `#lol-dev` - 英雄联盟开发
- `#tft-dev` - 云顶之弈开发
- `#lor-dev` - 符文之地传奇开发
- `#val-dev` - 无畏契约开发
- `#lcu-api` - LCU API 讨论
- `#ingame-api` - 游戏内 API
- `#rso-dev` - RSO 认证讨论

### 8.2 GitHub Issues

https://github.com/RiotGames/developer-relations/issues

官方开发者关系的 GitHub 问题追踪。

### 8.3 官方文档

https://developer.riotgames.com/docs/lol

Riot 官方 API 文档。

---

*翻译完成日期: 2026-05-25*