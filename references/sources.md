# 公开来源与适用边界

核验日期：2026-11-13。以下是公开网页的简短归纳及本项目的应用建议，不是授权转载的完整规范，也不是任何公司的私有设计文档。后续实施若依赖具体版本或数字，重新检查原文。

| ID | 官方/一手来源 | 可借鉴内容 | 应用边界 |
|---|---|---|---|
| S1 | [Riot — Clarity in League](https://www.leagueoflegends.com/en-us/news/dev/clarity-in-league/) | 信息重要性与视觉注意力匹配；轮廓辨识；减少噪声 | 原文针对竞技游戏；小镇中的角色/入口/目标优先级是本项目迁移，不是Riot小镇规范 |
| S2 | [Microsoft XAG 101 — Text display](https://learn.microsoft.com/en-us/xbox/accessibility/xbox-accessibility-guidelines/101) | 文本可读、字体选择、缩放及语言覆盖 | 文本大小随设备条件变化；不要把主机1080p的像素值直接套到手机CSS尺寸 |
| S3 | [Microsoft XAG 102 — Contrast](https://learn.microsoft.com/en-us/xbox/accessibility/xbox-accessibility-guidelines/102) | 普通关键文本/视觉元素参考4.5:1，大型元素有3:1等条件；复杂背景取最弱对比处 | 不是全部美术纹理的对比度要求；只采用其中一条不能声称整个游戏符合全部XAG |
| S4 | [Microsoft XAG 103 — Additional channels for visual and audio cues](https://learn.microsoft.com/en-us/xbox/accessibility/xbox-accessibility-guidelines/103) | 关键信息使用额外的感知渠道，不依赖单一颜色或声音 | 可迁移到事件提示、收集状态；具体替代方式需结合玩法验证 |
| S5 | [Unity — Pixel Perfect Camera reference, 6000.6 URP](https://docs.unity.com/en-us/engine/6000.6/manual/unity2d/2d-urp/2d-pixelperfect/ref) | 像素密度、参考分辨率、像素对齐与缩放取舍 | 本项目是HTML，借鉴概念即可；不要安装Unity包或照抄API；最近邻不自动消除所有缩放闪烁 |
| S6 | [MDN — image-rendering](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/image-rendering) | CSS缩放算法及pixelated选项 | 仅处理相应CSS缩放环节，不代表Canvas内部采样已关闭 |
| S7 | [MDN — requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame) | 按时间推进动画；回调跟随刷新率且后台通常暂停 | 游戏固定步长、碰撞及恢复策略是项目工程选择 |
| S8 | [MDN — Page Visibility API](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API) | 监测页面可见性变化 | 背景暂停或离线结算由玩法决定，API不替项目做决定 |
| S9 | [MDN — IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) | 同源结构化数据、索引及事务 | 不自动提供云备份、永久保存或跨设备同步 |

## 引用方式

每条外部要求注明来源ID、实际采用条目及适用平台；公开建议、项目硬约束和待验证参数分别列出。例：“本项目采用XAG 102普通关键文本4.5:1作为验收目标”，而非“大厂要求所有像素都达到4.5:1”。

本技能中的32px地块、角色画布、600秒一天、层级命名、JSON字段、事件事务流程、性能预算方法和编辑器验收项，是项目建议或工程实践整理，不归属于上述公司的统一标准。
