# HTML 像素小镇设计 Skill

面向 HTML 浏览器中的像素小镇：统一美术、地图编辑器、事件、早中晚昼夜、人物移动、收集册与存档。它是一套给AI和开发团队使用的规范，不包含游戏实现或素材图片。

## 使用

将整个 `html-pixel-town-design` 文件夹复制到支持 Agent Skills 的工具所扫描的技能目录，保留 `SKILL.md` 和 `references/` 的相对结构。

Codex 常见用户级目录为 `~/.agents/skills/`；Windows通常对应 `%USERPROFILE%\.agents\skills\`。也可放在项目 `.agents/skills/` 下，具体发现规则以所用客户端为准。重新打开会话后检查是否被发现；没有自动发现时可直接要求AI阅读主文件。

从 GitHub 安装到当前项目（在项目根目录执行，目标目录应不存在）：

```bash
git clone https://github.com/1047406067-alt/html-pixel-town-design-skill.git .agents/skills/html-pixel-town-design
```

若使用 GitHub 的 Download ZIP，请解压并将目录改名为 `html-pixel-town-design`，再放入技能目录。

示例指令：

> 使用 html-pixel-town-design，检查这个HTML小镇项目的素材一致性、编辑器数据、事件触发、早中晚切换、角色移动和收集册。沿用已有技术栈，先列实际问题与证据，再处理本次授权范围内的修改。

> 使用 html-pixel-town-design，为下一批建筑和角色写美术交付规格；把建议参数和已确认要求分开。

## 内容

- [SKILL.md](SKILL.md)：触发条件、工作流程和输出约定。
- [美术规范](references/art-direction.md)：风格、素材拆层、交付字段与避坑。
- [系统规范](references/web-systems.md)：HTML、编辑器、事件、时间、移动、收藏与存档。
- [验收清单](references/acceptance.md)：分项通过条件和证据记录。
- [交接示例](references/example.md)：一盏晚间灯笼的完整坐标与事件合同。
- [公开来源](references/sources.md)：Riot、微软、Unity与MDN，注明采用范围。

所有建议值可由项目已有规范替换。素材本身必须统一风格；公开行业经验不等于对特定厂商规范的全面认证。
