# 完整交接示例：晚间拾取灯笼

这是数据合同说明，无引擎依赖，不是可直接运行的完整游戏。数值全部为示例建议。

## 统一约定

- 世界单位=1个原生像素；地块32×32。世界原点为地图左上，x向右、y向下。
- 精灵坐标也从原始画布左上开始，单位像素；pivot是原始画布上的点，不是归一化比例。
- worldAnchor是pivot映射到的世界点。图片左上=worldAnchor−pivot；裁切图绘制左上再加trimOffset。
- collision与interaction均是相对worldAnchor的本地矩形，数组为[x,y,width,height]。
- footprintCells的offset原点为明确的placementCell；它不从图片尺寸自动推导。
- 此例为网格模式，worldAnchor=placementCell×32+[16,32]；placementCell为权威字段，导入校验冗余worldAnchor是否一致。
- collectionId标识灯笼种类，instanceId标识地图上的这一盏，eventId标识此次拾取事件。显示名称可本地化，不作为关联键。

```json
{
  "schemaVersion": 1,
  "contentVersion": "demo-1",
  "tileSizePx": 32,
  "assets": [
    {
      "assetId": "prop.lantern.red",
      "revision": 1,
      "styleVersion": "town-warm-1",
      "runtimeFile": "assets/lantern-red.png",
      "canvasPx": [32, 48],
      "pivotPx": [16, 44],
      "trimOffsetPx": [0, 0],
      "directions": ["south"],
      "animation": null,
      "sortAnchorLocalPx": [0, 0],
      "collisionLocalRectPx": [-8, -8, 16, 8],
      "interactionLocalRectPx": [-24, -24, 48, 48],
      "footprintCells": {"offset": [0, 0], "size": [1, 1]},
      "layers": ["body", "emissive"],
      "licenseRecord": "licenses/lantern-red.json"
    }
  ],
  "instances": [
    {
      "instanceId": "village.lantern.001",
      "assetId": "prop.lantern.red",
      "placementCell": [10, 6],
      "anchorOffsetPx": [16, 32],
      "worldAnchorPx": [336, 224]
    }
  ],
  "collections": [
    {
      "collectionId": "collection.red-lantern",
      "titleKey": "collection.redLantern.title",
      "category": "festival",
      "iconAssetId": "prop.lantern.red",
      "criterion": "pickup"
    }
  ],
  "clock": {
    "source": "simulation",
    "dayLengthSeconds": 600,
    "hiddenPolicy": "pause",
    "phases": [
      {"id": "morning", "start": 0, "end": 200},
      {"id": "noon", "start": 200, "end": 400},
      {"id": "evening", "start": 400, "end": 600}
    ]
  },
  "events": [
    {
      "eventId": "pickup.village.lantern.001",
      "trigger": {"type": "interact", "instanceId": "village.lantern.001"},
      "conditions": [{"type": "phaseEquals", "value": "evening"}],
      "repeatPolicy": "once-per-save",
      "reentryPolicy": "ignore-while-running",
      "transactionalActions": [
        {"type": "unlockCollection", "collectionId": "collection.red-lantern"},
        {"type": "removeInstance", "instanceId": "village.lantern.001"}
      ],
      "completionKey": "pickup.village.lantern.001",
      "afterCommit": [{"type": "showToast", "textKey": "collection.newEntry"}]
    }
  ]
}
```

此示例中渲染左上是(320,180)，放置格(10,6)覆盖世界矩形[320,192,32,32]。图片高48px、占地1格、碰撞16×8px、交互48×48px，四者不同。PNG和授权文件路径用于说明交接，不表示本Skill附带这些素材。

约定：此例criterion为pickup，因此unlockCollection幂等地把条目标为已发现且已收集，保留首次收集时间；它不是只解锁一个未知轮廓。removeInstance写入存档的已移除实例集合；完成键与这两个状态变化一起提交。afterCommit仅显示反馈，不能额外发奖励。存储失败保留原状态并允许重试，不先标记已领取。真正异步持久化期间阻止同一事件重入。

本例在提交前重验晚间条件、实例存在和完成键，多个事件经同一状态队列提交。实际SaveGame须保存收藏记录、已移除实例集合和完成键集合；加载后由内容定义加这些记录重建世界，而不是重新生成已拾取物。此处未提供完整SaveGame序列化实现。

执行轨迹：中午交互不满足条件 → 到400秒切晚间 → 交互一次 → 收藏解锁、实例移除、完成键写入 → 提示新条目 → 刷新读档仍然已收集，物件不重生。不支持的条件或动作必须在导入校验时报错。

这只是一个小资产的坐标及事件示范；正式交付还需按[美术合同](art-direction.md)补源文件、完整授权、发光层文件、导入设置与实际图标。
