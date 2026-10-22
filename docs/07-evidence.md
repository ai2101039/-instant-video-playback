# 来源、版本与证据等级

整理日期：2026-10-22。源项目是原生 Android 短剧应用。本包按主题重写、使用虚构示例，不导出原项目资源、媒体、配置和完整业务源码。

## 证据等级

| 标记 | 含义 | 不能推导出的结论 |
|---|---|---|
| source_verified | 整理时已读取源项目当前代码 | 目标项目已实现；任意设备已通过 |
| documented_backend | 源项目保存的后端说明中有记录 | 本次已核验后端源码、DDL 或线上状态 |
| historical_measurement | 已有验收报告及样本 | 本次新测试；目标项目性能承诺 |
| recommendation | 为迁移总结的建议 | 源项目已落地该建议 |

## 代码核对范围

按相对模块定位，包名前缀已省略；这些文件未附在本包，接入不依赖它们存在。

| 来源模块 | 核对内容 |
|---|---|
| data/ApiClient、Models、CatalogRepository | 目录窗口、首页/详情选集差异、锁定过滤、解析来源 |
| data/PlaybackUrlCache | 7 项 LRU、TTL、签名边界、在途合并、取消与代次 |
| data/EpisodePreloadPolicy | 方向、距离、缺集/锁定、预加载时长 |
| data/LocalUserStore | DataStore 账号/模式隔离的毫秒位置 |
| ui/player/MediaCache、MediaHttpDataSource | 共享缓存、索引、URI 键、HTTP 关闭 |
| ui/player/PlaybackEngine、PlaybackEnginePool | 五槽、独立 Builder、所有权、预创建与归还 |
| ui/player/EpisodePlaybackSession | 当前首帧优先、输出匹配、晋升、预热调度 |
| ui/player/PlayerLoadingIndicator | 1 秒显示门槛 |

依赖清单与代码中使用 Media3 1.11.1 的相关 API；这是源项目版本记录，不表示所有接入方可直接调用这些 API，也不表示它是阅读时最新版本。

## 文档与历史记录

后端来源为 `v5-drama-client-guide.md` 与 `v5-drama-api.md`，内容涉及 V5 接口、数据对象与 Redis；缺少真实 DDL/索引/执行计划。原文包含重复变更和时间差异，本包只提取可定位条目，未把描述中的耗时作为新复测。

性能来源为 2026-10-20 首帧对照报告和 2026-10-21 独立播放线程报告，并核对后者的 comparison-summary.json。公开样本保留数值、日期、场景和条件；移除真实剧名、内容 ID、地址、设备序列号及安装身份。原始私有日志未提供，因此这是可复算的摘录，不是独立可审计的原始实验数据集。

旧文档中的两播放器、三播放器、首页三路加详情五路、八对象等是演进阶段；本包当前描述以全局五槽、独立播放队列和现行首页目录策略为准。历史性能也不能代表整理当日尚有其他改动的工作区。

## 公开参考

- [Media3 预加载管理器](https://developer.android.com/media/media3/exoplayer/preloading-media/preloadmanager)
- [Media3 HLS](https://developer.android.com/media/media3/exoplayer/hls)
- [Media3 输出类型](https://developer.android.com/media/media3/ui/surface)

官方文档用于解释基础能力，不能作为本项目具体性能提升的证据。
