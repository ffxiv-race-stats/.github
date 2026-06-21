# FFXIV 高难首杀竞速网站

FFXIV 高难副本世界首杀竞速数据聚合平台。追踪队伍进度、赛事新闻、转播方信息——一切尽在实时排名表。

→ **[ffxiv-race-stats.pages.dev](https://ffxiv-race-stats.pages.dev)**

---

## 团队

| Team | 成员 | 职责 |
|------|------|------|
| **`dev-team`** | 开发者 | 页面代码、CSS 样式、JS 逻辑、CI 配置 |
| **`ops-agent`** | PI Agent（自动化） | `data.js` 数据值（队伍进度、新闻、转播方信息） |

### 为什么 `ops-agent` 只有一个人？

运营者**不需要 GitHub 账号**。运营者通过自然语言（"队伍1 P5 了，血量 12%"）描述变更，由 **PI Agent** 自动完成 git 操作（创建 `content/*` 分支、修改 `data.js`、校验、创建 PR、合并）。`ops-agent` team 中的账号只是 Agent 的执行身份——当前由项目持有者兼任，将来会替换为独立的机器账号。

简单说：
```
运营者说 "队伍1 通关了"
      ↓
PI Agent 自动执行全部 git 操作
      ↓
data.js 更新上线
```

---

## 开发规范

### Clone

```bash
git clone git@github.com:ffxiv-race-stats/ffxiv-race-stats.git
```

### 分支

| 轨道 | 前缀 | 示例 |
|------|------|------|
| 开发 | `feature/*`、`fix/*` | `feature/add-guide-page`、`fix/mobile-table` |
| 运营 | `content/*` | `content/update-t1-p5` |

### 你能改什么

✅ HTML、CSS、JS 模块、`.github/`、`docs/`、`schema/`、`.pi/`
❌ `data.js` 的数据值（运营侧地盘）。改结构可以，改值不行。

### 提交流程

```
1. git checkout main && git pull
2. git checkout -b feature/<描述>
3. 写代码 → 本地用浏览器打开 index.html 测试
4. commit（英文，格式: feat: / fix: / refactor: / docs: + 描述）
5. git push → 去 github.com 创建 PR
6. CI（validate）自动运行，绿色 ✓ 后才能合并
7. Squash and merge 合入 main
```

### Commit 格式

```
feat: add guide page navigation
fix: table overflow on mobile breakpoint
refactor: extract rank calculation utility
docs: update responsive breakpoint documentation
```

---

## 项目特点

- **零依赖**：无 npm、无构建、无框架。浏览器直接打开 `index.html`
- **双轨模型**：开发侧改页面代码，运营侧改数据值。CI + CODEOWNERS 确保不越界
- **OKLCH 设计系统**：CSS 变量控制全局主题，系统字体栈
- **Squash Merge**：main 分支保持干净，一个 PR = 一个 commit
- **运营免 Git**：运营者不碰 GitHub，全程由 PI Agent 执行

---

## 链接

- [仓库](https://github.com/ffxiv-race-stats/ffxiv-race-stats)
- [生产站](https://ffxiv-race-stats.pages.dev)
