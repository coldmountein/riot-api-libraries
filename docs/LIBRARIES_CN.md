# Riot API 库详细介绍 - 中文版

---

## 一、Python 库

---

### 1. Cassiopeia (☆ 471)

**最受欢迎的 Python Riot API 库**

#### 简介
Cassiopeia 是一个功能完整的 Riot API 库，专注于易用性。它会自动处理所有技术细节（速率限制、缓存、数据转换等），让你专注于构建应用。

#### 特点
- ✅ 自动速率限制处理
- ✅ 内置缓存系统
- ✅ 简洁的 API 设计
- ✅ 完整的类型支持
- ✅ 支持 Riot API v4

#### 安装
```bash
pip install cassiopeia
```

#### 快速示例
```python
import cassiopeia as cass

# 设置 API Key
cass.set_api_key("YOUR_API_KEY")

# 获取召唤师信息
summoner = cass.get_summoner(name="ColdMountain", region="JP")

print(f"名称: {summoner.name}")
print(f"等级: {summoner.level}")
print(f"段位: {summoner.league_entries[0].tier} {summoner.league_entries[0].division}")
```

#### 链接
- PyPI: https://pypi.org/project/cassiopeia/
- 文档: http://cassiopeia.readthedocs.org/en/latest/
- GitHub: https://github.com/meraki-analytics/cassiopeia

---

### 2. Riot-Watcher (☆ 468)

**简单轻量的 Riot API 包装器**

#### 简介
Riot-Watcher 是一个简单易用的 Riot API 包装器，专注于提供直接、简洁的 API 接口。

#### 特点
- ✅ 简单易用
- ✅ 内置速率限制
- ✅ 轻量设计
- ✅ 支持 Riot API v4

#### 安装
```bash
pip install riotwatcher
```

#### 快速示例
```python
from riotwatcher import LolWatcher, ApiError

lol_watcher = LolWatcher('YOUR_API_KEY')

# 获取召唤师信息
my_region = 'jp1'
me = lol_watcher.summoner.by_name(my_region, 'ColdMountain')

print(f"名称: {me['name']}")
print(f"等级: {me['summonerLevel']}")
print(f"ID: {me['id']}")

# 获取段位信息
my_ranked_stats = lol_watcher.league.by_summoner(my_region, me['id'])
print(my_ranked_stats)
```

#### 链接
- 文档: http://riot-watcher.readthedocs.io/en/latest/
- PyPI: https://pypi.python.org/pypi/riotwatcher
- GitHub: https://github.com/pseudonym117/Riot-Watcher

---

### 3. Pyot (☆ 83)

**现代化异步 Riot API 框架**

#### 简介
Pyot 是一个基于 AsyncIO 的现代化 Riot API 框架，支持 Django 集成，鼓励快速开发和简洁设计。

#### 特点
- ✅ AsyncIO 支持
- ✅ Django 集成
- ✅ 多游戏支持（LoL, LOR, TFT, VAL）
- ✅ 内置速率限制
- ✅ TypeScript 式的静态配置

#### 安装
```bash
pip install pyot
```

#### 快速示例
```python
import asyncio
from pyot.core import PyotCore
from pyot.models.lol.summoner import Summoner

async def main():
    async with PyotCore(api_key="YOUR_API_KEY") as pyot:
        summoner = await Summoner(name="ColdMountain", platform="JP1").get()
        print(f"名称: {summoner.name}")
        print(f"等级: {summoner.level}")

asyncio.run(main())
```

#### 链接
- PyPI: https://pypi.org/project/pyot/
- 文档: https://pyot.paaksing.com/
- GitHub: https://github.com/paaksing/Pyot

---

## 二、JavaScript/TypeScript 库

---

### 1. Twisted (☆ 81)

**全功能 JavaScript/TypeScript 库**

#### 简介
Twisted 是一个功能完整的 Riot API 库，支持 LoL 和 TFT，提供完整的 TypeScript 类型定义。

#### 特点
- ✅ 内置速率限制
- ✅ 内置缓存
- ✅ 支持 LoL 和 TFT
- ✅ TypeScript 类型支持
- ✅ 多平台（Node.js, Browser）

#### 安装
```bash
npm install twisted
```

#### 快速示例
```typescript
import { RiotAPI, RiotAPITypes, PlatformModels } from 'twisted';

const api = new RiotAPI('YOUR_API_KEY');

// 获取召唤师信息
const summoner = await api.Summoner.getByName('ColdMountain', RiotAPITypes.Region.JP);
console.log(summoner.response);

// 获取段位信息
const entries = await api.League.getEntriesBySummonerId(summoner.response.id, RiotAPITypes.Region.JP);
console.log(entries.response);
```

#### 链接
- npm: https://www.npmjs.com/package/twisted
- GitHub: https://github.com/Sansossio/twisted
- 示例: https://github.com/Sansossio/twisted/tree/master/example

---

### 2. Shieldbow (☆ 15)

**易于使用的 TypeScript Riot API 包装器**

#### 简介
Shieldbow 是一个超易用的 Riot API 包装器，提供完整的 TypeScript 类型支持。

#### 特点
- ✅ 超易用设计
- ✅ 完整 TypeScript 支持
- ✅ 内置速率限制
- ✅ 内置缓存
- ✅ 支持 v4 和 v5

#### 安装
```bash
npm install shieldbow
```

#### 快速示例
```typescript
import { Client } from 'shieldbow';

const client = new Client('YOUR_API_KEY');

// 获取召唤师信息
const summoner = await client.summoners.fetch('ColdMountain', 'jp');
console.log(summoner.name);
console.log(summoner.level);

// 获取段位信息
const entries = await summoner.fetchLeagueEntries();
console.log(entries);
```

#### 链接
- npm: https://www.npmjs.com/package/shieldbow
- GitHub: https://github.com/TheDrone7/shieldbow
- 文档: https://thedrone7.github.io/shieldbow/

---

### 3. Galeforce (☆ 31)

**多游戏支持的 TypeScript Fluent Interface**

#### 简介
Galeforce 是一个可定制、Promise-based、Command-oriented 的 TypeScript Riot API 库，支持多个 Riot 游戏。

#### 特点
- ✅ 多游戏支持（LoL, LOR, VAL, TFT）
- ✅ Fluent interface 设计
- ✅ Promise-based
- ✅ 内置速率限制和缓存
- ✅ 支持 v4 和 v5

#### 安装
```bash
npm install galeforce
```

#### 快速示例
```typescript
import Galeforce from 'galeforce';

const galeforce = Galeforce.withKey('YOUR_API_KEY');

// 获取召唤师信息
const summoner = await galeforce.lol.summoner.region('jp').name('ColdMountain').get();
console.log(summoner);

// 获取段位信息
const entries = await galeforce.lol.league.entries.region('jp').summonerId(summoner.id).get();
console.log(entries);
```

#### 链接
- npm: https://www.npmjs.com/package/galeforce
- GitHub: https://github.com/bcho04/galeforce
- 文档: https://bcho04.github.io/galeforce/

---

### 4. Kayn (☆ 134)

**老牌 Node.js Riot API 库**

#### 简介
Kayn 是一个经典的 Riot API 库，受到 superagent 启发，设计简洁高效。

#### 特点
- ✅ 内置速率限制
- ✅ 内置缓存
- ✅ 简洁的 API 设计
- ✅ 部分 TypeScript 支持

#### 安装
```bash
npm install kayn
```

#### 快速示例
```javascript
const Kayn = require('kayn');
const kayn = Kayn('YOUR_API_KEY');

// 获取召唤师信息
kayn.Summoner.by.name('ColdMountain')
  .region('jp')
  .then(summoner => {
    console.log(summoner);
  });

// 获取段位信息
kayn.LeaguePositions.by.summonerID('SUMMONER_ID')
  .region('jp')
  .then(entries => {
    console.log(entries);
  });
```

#### 链接
- npm: https://www.npmjs.com/package/kayn
- GitHub: https://github.com/cnguy/kayn

---

## 三、Java 库

---

### 1. Orianna (☆ 160)

**高度可配置的 Java Riot API 框架**

#### 简介
Orianna 是一个高度可配置、易用性优先的 Java Riot API 框架，自动处理所有细节。

#### 特点
- ✅ 高度可配置
- ✅ 易用性优先
- ✅ 内置速率限制
- ✅ 内置缓存
- ✅ 支持 Riot API v4

#### Maven 安装
```xml
<dependency>
  <groupId>com.merakianalytics.orianna</groupId>
  <artifactId>orianna</artifactId>
  <version>4.0.0</version>
</dependency>
```

#### 快速示例
```java
import com.merakianalytics.orianna.types.core.summoner.Summoner;
import com.merakianalytics.orianna.Orianna;

// 配置 API Key
Orianna.setRiotAPIKey("YOUR_API_KEY");

// 获取召唤师信息
Summoner summoner = Summoner.named("ColdMountain").withRegion(Region.JAPAN).get();

System.out.println("名称: " + summoner.getName());
System.out.println("等级: " + summoner.getLevel());

// 获取段位信息
LeagueEntry entry = summoner.getLeagueEntries().get(0);
System.out.println("段位: " + entry.getTier() + " " + entry.getDivision());
```

#### 链接
- Maven: https://search.maven.org/search?q=g:com.merakianalytics.orianna
- 文档: http://orianna.readthedocs.org/en/latest/
- JavaDoc: http://javadoc.io/doc/com.merakianalytics.orianna/orianna
- GitHub: https://github.com/meraki-analytics/orianna

---

### 2. R4J (☆ 65)

**支持所有 Riot 游戏的 Java 库**

#### 简介
R4J 是一个包含所有 Riot 游戏 API 的 Java 库，支持 LoL, TFT, LOR, VAL 等。

#### 特点
- ✅ 支持所有 Riot 游戏
- ✅ Riot API v4
- ✅ Apache 2.0 许可

#### 链接
- GitHub: https://github.com/stelar7/R4J

---

## 四、C# 库

---

### 1. Camille (☆ 77)

**高性能 C# Riot API 库**

#### 简介
Camille 是一个完全速率限制、自动重试、线程安全的 C# Riot API 库。

#### 特点
- ✅ 完全速率限制
- ✅ 自动重试
- ✅ 线程安全
- ✅ 每晚自动发布
- ✅ 支持 v3 和 v4

#### NuGet 安装
```
Install-Package MingweiSamuel.Camille
```

#### 快速示例
```csharp
using MingweiSamuel.Camille.RiotGames;
using MingweiSamuel.Camille.RiotGames.SummonerV4;

var riotApi = RiotGamesApi.NewInstance("YOUR_API_KEY");

// 获取召唤师信息
var summoner = await riotApi.SummonerV4.GetBySummonerName(Region.JP, "ColdMountain");

Console.WriteLine($"名称: {summoner.Name}");
Console.WriteLine($"等级: {summoner.SummonerLevel}");

// 获取段位信息
var entries = await riotApi.LeagueV4.GetLeagueEntriesForSummoner(Region.JP, summoner.Id);
foreach (var entry in entries)
{
    Console.WriteLine($"段位: {entry.Tier} {entry.Rank}");
}
```

#### 链接
- NuGet: https://www.nuget.org/packages/MingweiSamuel.Camille/
- GitHub: https://github.com/MingweiSamuel/Camille

---

### 2. RiotSharp (☆ 288)

**经典 C# Riot API 库**

#### 简介
RiotSharp 是一个经典的 C# Riot API 库，支持 ASP.NET Core 集成。

#### 特点
- ✅ ASP.NET Core 支持
- ✅ 内置速率限制
- ✅ MIT 许可

#### 注意
**NuGet 版本可能严重过时，建议直接使用源码！**

#### 链接
- GitHub: https://github.com/BenFradet/RiotSharp

---

## 五、Rust 库

---

### 1. Riven (☆ 76)

**高性能 Rust Riot API 库**

#### 简介
Riven 是一个经过严格测试的 Rust Riot API 库，设计高效可靠。

#### 特点
- ✅ 高性能
- ✅ 自动速率限制
- ✅ 支持 v3 和 v4
- ✅ 支持 TFT

#### Cargo 安装
```toml
[dependencies]
riven = "2"
```

#### 快速示例
```rust
use riven::RiotApi;
use riven::models::summoner_v4::Summoner;
use riven::consts::Region;

let api = RiotApi::new("YOUR_API_KEY");

// 获取召唤师信息
let summoner = api.summoner_v4().get_by_summoner_name(Region::JP, "ColdMountain");
match summoner {
    Some(s) => println!("名称: {}", s.name),
    None => println!("未找到"),
}
```

#### 链接
- Docs.rs: https://docs.rs/riven/
- Crates.io: https://crates.io/crates/riven
- GitHub: https://github.com/MingweiSamuel/Riven

---

## 六、Go 库

---

### 1. Golio (☆ 45)

**Go 语言 Riot API 客户端**

#### 简介
Golio 是一个用 Go 编写的英雄联盟 API 客户端。

#### 特点
- ✅ 内置速率限制
- ✅ 内置缓存
- ✅ MIT 许可

#### 链接
- GitHub: https://github.com/KnutZuidema/golio
- GoDoc: https://godoc.org/github.com/KnutZuidema/golio

---

## 七、PHP 库

---

### 1. Riot-API (☆ 110)

**PHP7 Riot API 包装器**

#### 简介
Riot-API 是一个 PHP7 的 Riot API 包装器，支持 LoL 和 DataDragon。

#### 特点
- ✅ PSR-7/PSR-18 兼容
- ✅ 内置速率限制
- ✅ CLI 工具

#### 链接
- Packagist: https://packagist.org/packages/dolejska-daniel/riot-api
- GitHub: https://github.com/dolejska-daniel/riot-api
- Wiki: https://github.com/dolejska-daniel/riot-api/wiki

---

## 八、Swift 库

---

### 1. LeagueAPI (☆ 51)

**iOS/macOS Swift Riot API 库**

#### 简介
LeagueAPI 是一个 Swift 框架，提供所有英雄联盟数据，支持 Carthage 和 CocoaPods。

#### 特点
- ✅ 内置缓存
- ✅ 自动速率限制和重试
- ✅ MIT 许可

#### 链接
- GitHub: https://github.com/Kelmatou/LeagueAPI
- 文档: https://github.com/Kelmatou/LeagueAPI/wiki

---

## 九、库对比总结

### Python 库对比

| 库名 | Stars | 异步支持 | 缓存 | 多游戏 |
|------|-------|---------|------|--------|
| Cassiopeia | 471 | ❌ | ✅ | ❌ |
| Riot-Watcher | 468 | ❌ | ❌ | ❌ |
| Pyot | 83 | ✅ | ✅ | ✅ |

### JavaScript/TypeScript 库对比

| 库名 | Stars | TypeScript | 缓存 | 多游戏 |
|------|-------|-----------|------|--------|
| Kayn | 134 | 部分 | ✅ | ❌ |
| Twisted | 81 | ✅ | ✅ | TFT |
| Galeforce | 31 | ✅ | ✅ | ✅ |
| Shieldbow | 15 | ✅ | ✅ | ❌ |

---

## 十、选择建议

### 根据语言选择

- **Python**: Cassiopeia（最完整）或 Pyot（异步）
- **JavaScript**: Twisted（全功能）或 Kayn（经典）
- **TypeScript**: Shieldbow 或 Galeforce
- **Java**: Orianna
- **C#**: Camille
- **Rust**: Riven

### 根据需求选择

- **简单易用**: Cassiopeia, Riot-Watcher, Shieldbow
- **高性能异步**: Pyot, Riven
- **多游戏支持**: Pyot, Galeforce, R4J
- **生产环境**: 所有推荐库都适合生产环境

---

*翻译完成日期: 2026-05-25*