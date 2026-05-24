# Riot Games API 文档 - 完整中文翻译

---

## 一、API 申请说明 (Applications)

### 1.1 开发密钥 vs 生产密钥

你可以在开发者门户主页点击 "Register Project" 申请个人或生产应用。

**重要提示**：
- 开发密钥每 24 小时过期，除非你申请并获得个人或生产应用密钥
- 如果收到 403 响应，通常只需要刷新密钥

### 1.2 申请流程

- 应用审核大约需要 **两周**（10 个工作日，不含节假日）
- 确保应用已验证（riot.txt）
- 如果超过两周且期间未修改应用，可在 Discord 向 Guru 寻求帮助

### 1.3 密钥类型

#### 生产密钥 (Production App)
- 注册项目申请生产 API 密钥
- 访问标准 API 和/或锦标赛 API
- 需要**可工作的原型**
- 不用于测试目的
- 可在项目规划阶段提交申请，但只有在项目准备好公开发布时才会批准

#### 个人密钥 (Personal App)
- 注册项目申请个人 API 密钥
- 无需验证流程
- 仅用于标准 API，不包括锦标赛 API
- 需要详细的项目描述

### 1.4 获取 App ID

访问 https://developer.riotgames.com/apps，从左侧列表选择项目，URL 中的数字即为 App ID。

---

## 二、数据收集指南 (Collecting Data)

### 2.1 比赛数据收集

收集大量比赛数据的最佳方法并不简单。通常需要以下步骤：

#### 步骤流程

1. **手动收集一些召唤师**
   - 你自己的召唤师就足够了
   - 或者使用所有挑战者玩家

2. **获取这些召唤师的账号 ID**

3. **获取他们指定队列类型的比赛历史**
   - 根据需要分页
   - 按补丁版本过滤

4. **成功！** 你获得了大量比赛 ID
   - 可以获取时间线数据
   - 或按需要解析比赛

#### 替代方案

Discord 的 Canisback 目前托管了比赛 ID 列表：
- 地址: http://canisback.com/matchId/
- 可用于从 `matches/{matchId}` 端点获取召唤师
- 免费提供给社区使用
- 可能随时停止服务或停止更新

### 2.2 召唤师数据收集

召唤师数据收集方法与比赛数据类似。

#### 使用联赛端点

联赛端点提供排名召唤师的分页列表：
- 位置联赛端点按段位 + 分段 + 位置分页
- 例如：所有钻石 II 上单玩家

#### 替代方案

Discord 的 Canisback 目前托管了联赛 ID 列表：
- 地址: http://canisback.com/leagueId/
- 可用于从 `leagues/{leagueId}` 端点获取召唤师
- 免费提供给社区使用

---

## 三、Data Dragon 使用指南 (Data Dragon)

### 3.1 什么是 Data Dragon？

Data Dragon（简称 ddragon）是 Riot 提供的静态数据文件集合：
- 英雄图片和信息
- 物品图片和信息
- 符文图片和信息
- 将 ID 转换为名称的数据

### 3.2 数据获取

#### 下载完整数据包

```
https://ddragon.leagueoflegends.com/cdn/dragontail-{版本}.tgz
```

- 文件大小约 1 GB
- 包含所有图片和数据

#### 单文件访问

```
https://ddragon.leagueoflegends.com/cdn/{版本}/data/{语言}/champion.json
```

示例：
```
https://ddragon.leagueoflegends.com/cdn/12.6.1/data/en_US/champion.json
```

### 3.3 缓存建议

- Data Dragon 数据只在新补丁发布时更新
- 建议缓存到本地，减少网络请求
- 可显著提升应用性能

### 3.4 Community Dragon

如果 Data Dragon 没有你需要的数据，查看 Community Dragon：

```
http://raw.communitydragon.org/
```

这是社区生成的补充数据。

### 3.5 版本信息

- 最新版本列表: https://ddragon.leagueoflegends.com/api/versions.json
- 区域版本检查: https://ddragon.leagueoflegends.com/realms/{区域}.json

### 3.6 支持的语言

完整语言列表: https://ddragon.leagueoflegends.com/cdn/languages.json

| 代码 | 语言 |
|------|------|
| zh_CN | 简体中文（中国） |
| zh_TW | 繁体中文（台湾） |
| ja_JP | 日语（日本） |
| en_US | 英语（美国） |
| ko_KR | 韩语（韩国） |

### 3.7 常见问题

#### 英雄内部名称

Wukong 的内部名称是 `monkeyking`。查看 `champion.json` 的 `key` 属性获取所有英雄的内部名称。

#### 数据不准确

Data Dragon 的部分数据（特别是技能数据）可能不准确。
建议使用 [League Wikia](https://leagueoflegends.fandom.com/wiki/League_of_Legends_Wiki)。

#### 新版本未更新

新补丁发布后，Data Dragon 可能需要 1-2 天才更新。

---

## 四、ID 说明 (PUUIDs and Other IDs)

### 4.1 三种 ID 类型

Riot API 使用三种 ID：

| ID 类型 | 说明 | 唯一性 |
|--------|------|--------|
| **Summoner ID** | 召唤师 ID | 区域唯一 |
| **Account ID** | 账号 ID | 区域唯一 |
| **PUUID** | 玩家唯一 ID | 全球唯一 |

### 4.2 使用建议

- 不同 API 使用不同的 ID
- 使用 API 要求的 ID 类型

### 4.3 PUUID 的特点

- **全球唯一**
- 转区时不会改变
- 可以追踪转区的玩家

### 4.4 转区影响

当玩家转区时：
- PUUID **不会改变**
- Summoner ID 和 Account ID **会改变**

### 4.5 ID 加密

- 所有 ID 使用项目唯一的加密密钥加密
- 开发密钥获取的 ID 不能用于生产密钥（反之亦然）
- 刷新密钥时，加密 ID 不会改变

---

## 五、LCU API 使用指南 (LCU)

### 5.1 什么是 LCU？

LCU (League Client Update) = 英雄联盟客户端

LCU API 允许访问客户端内部功能：
- 创建/管理游戏房间
- 获取当前比赛信息
- 查看好友列表

### 5.2 使用条件

- 客户端必须在本地运行
- 必须已登录
- 在开发者门户创建应用说明使用方式

### 5.3 可用端点

官方允许使用的端点列表：
https://developer.riotgames.com/league-client-apis.html

### 5.4 探索工具

#### Rift Explorer
https://github.com/Pupix/rift-explorer

#### LCU Explorer
https://github.com/HextechDocs/lcu-explorer

#### Vivi 的 Swagger 网站
http://lcu.vivide.re/

### 5.5 常用技巧

#### 无登录模式

启动参数：
```
--mode unattended
```

允许在无头服务器使用部分端点。

#### 创建游戏房间

普通房间：
```json
POST /lol-lobby/v2/lobby
{"queueId": 430}
```

自定义房间：
```json
POST /lol-lobby/v2/lobby
{
  "customGameLobby": {
    "configuration": {
      "gameMode": "PRACTICETOOL",
      "mapId": 11,
      "teamSize": 5
    },
    "lobbyName": "房间名"
  },
  "isCustom": true
}
```

#### 有用的启动参数

```
--app-port=1337 --headless --allow-multiple-clients
```

---

## 六、移动应用开发 (Mobile Apps)

### 6.1 CORS 问题

客户端调用 Riot API 被**阻止**：
- 无法在不暴露 API Key 的情况下调用
- 需要设置后端服务器安全存储 API Key

### 6.2 解决方案

#### 快速代理服务器

- 使用 AWS Lambda 创建函数
- 或使用 [Kernel](https://github.com/meraki-analytics/kernel)

#### 个人项目

修改浏览器设置禁用 CORS：
- 仅用于个人测试
- 不能发布公开网站

### 6.3 移动应用要求

- 创建网页说明应用
- 设置服务器代理 API 调用
- 网页应包含足够信息让 Rioter 评估项目
- 无法安全存储 API Key，必须通过服务器通信

---

## 七、Replay API 使用指南 (Replay API)

### 7.1 简介

Replay API 是新的游戏客户端 API，允许在回放中调整游戏镜头。

### 7.2 League Director

Riot 发布了 [League Director](https://github.com/riotgames/leaguedirector)，使用这些 API，可作为开发起点。

### 7.3 文档

- Replay API 文档: https://developer.riotgames.com/replay-apis.html
- League Director: https://github.com/riotgames/leaguedirector

---

## 八、英雄位置识别 (Role ID)

### 8.1 问题说明

想要知道每个英雄在召唤师峡谷的位置。

Riot API 提供的角色和分路数据**经常不准确**。

### 8.2 数据定义

| 类型 | 值 |
|------|-----|
| **Role** | DUO, DUO_CARRY, DUO_SUPPORT, NONE, SOLO |
| **Lane** | TOP_LANE, MID_LANE, BOT_LANE, JUNGLE |
| **Position** | TOP, MIDDLE, JUNGLE, BOTTOM, UTILITY, APEX, NONE |

### 8.3 修正方法

#### 方法一：简单映射

准确率约 87.5%

```json
{
    (MID_LANE, SOLO): MIDDLE,
    (TOP_LANE, SOLO): TOP,
    (JUNGLE, NONE): JUNGLE,
    (BOT_LANE, DUO_CARRY): BOTTOM,
    (BOT_LANE, DUO_SUPPORT): UTILITY
}
```

#### 方法二：使用出场率

使用英雄出场率数据判断位置：
- 不使用 Lane 或 Role 数据
- 纯依赖出场率统计
- 准确率约 95%
- 可用于当前游戏端点

实现示例: https://github.com/meraki-analytics/role-identification

#### 方法三：使用时间线数据

使用比赛时间线对象中的数据：
- 查看英雄在地图上的位置
- 分析物品、符文、召唤师技能
- 使用机器学习方法

训练数据: https://github.com/Canisback/roleML/blob/master/data/verification_results.csv

实现示例: https://github.com/meraki-analytics/role-identification/blob/timeline/

#### 其他有用数据

查看召唤师最近游戏历史：
- 如 80% 玩中路
- 可推断其他游戏位置

---

## 九、特定数据信息 (Specifics)

### 9.1 召唤师数据

参见 ID 说明章节。

### 9.2 比赛数据

| 项目 | 说明 |
|------|------|
| **保存时间** | 比赛 2 年，时间线 1 年 |
| **创建时间** | 毫秒级时间戳（非秒） |
| **选择顺序** | 0-5-1-6-2-7-3-8-4-9 |
| **totalGame 字段** | 多数情况不准确，建议忽略 |
| **赛季 ID** | 仅用于超过一年的数据，建议使用时间戳 |

赛季开始时间: https://github.com/CommunityDragon/Data/blob/master/patches.json

种子数据: https://s3-us-west-1.amazonaws.com/riot-developer-portal/seed-data/matches1.json ... matches10.json

### 9.3 自定义游戏数据

- 目前无法从 API 获取自定义游戏数据（隐私政策）
- Riot 正在开发外部 RSO 解决方案
- 允许玩家授权网站使用其自定义游戏数据

### 9.4 验证

RSO (Riot Sign-On) = Riot 登录系统。

网站验证流程：
1. 生成随机字符串
2. 用户输入到客户端
3. 使用验证端点

**注意**：验证端点可能有问题，用户可能需要重启客户端多次。

### 9.5 当前游戏

- 观战时间不准确且不一致
- 参考 GitHub issue #81

### 9.6 回放文件

- 反工程回放文件 (.rofl) **不可能** 且违反条款
- 加密方式每补丁变化
- 用于防止作弊

---

## 十、电竞 API (eSports API)

### 10.1 简介

官方 API **不支持** 电竞。

lolesports.com 使用的 API：
- 官方不支持
- 可能随时无预警变更

### 10.2 非官方文档

- https://gist.github.com/levi/e7e5e808ac0119e154ce
- https://gist.github.com/brcooley/8429583561c47b248f80

### 10.3 示例代码

https://github.com/Canisback/LoLWorlds2018/blob/master/gatherGames.ipynb

### 10.4 个人比赛数据

https://github.com/PandaXcentric/game_apis

---

## 十一、库列表 (Libraries)

详见 `LIBRARIES_CN.md` 文档。

---

## 十二、搜索 (Search)

欢迎使用 Riot API Libraries 文档！

---

## 附录：快速参考

### 常用端点

| 端点 | 说明 |
|------|------|
| `/lol/summoner/v4/summoners/by-name/{name}` | 按名称获取召唤师 |
| `/lol/match/v4/matchlists/by-account/{accountId}` | 获取比赛列表 |
| `/lol/match/v4/matches/{matchId}` | 获取比赛详情 |
| `/lol/league/v4/entries/by-summoner/{summonerId}` | 获取段位信息 |

### 常用区域

| 代码 | 区域 |
|------|------|
| `jp1` | 日本 |
| `kr` | 韩国 |
| `na1` | 北美 |
| `euw1` | 欧洲西部 |
| `eun1` | 欧洲北部/东部 |

### 常用队列 ID

| ID | 类型 |
|-----|------|
| 420 | 单排 |
| 440 | 灵活组排 |
| 430 | 匹配 |
| 450 | ARAM |
| 400 | 征召模式 |

---

*翻译完成日期: 2026-05-25*
*翻译者: OpenClaw Assistant*