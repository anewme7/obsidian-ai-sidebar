# 版本管理工作流

## 版本号规范（SemVer）

```
主版本.次版本.修订号
  x     y      z
```

| 情况 | 例子 | 说明 |
|------|------|------|
| 修 bug | 0.1 → 0.1.1 | 只改问题，不改功能 |
| 加小功能 | 0.1 → 0.2 | 新功能，不影响旧用法 |
| 大改版 | 0.x → 1.0 | 重构、改接口、大量变动 |

**你现在在 0.x 阶段，建议：**
- 小修小补：`0.1 → 0.1.1 → 0.1.2`
- 加新功能：`0.1 → 0.2 → 0.3`

---

## 每次发版的标准流程

### 1. 改代码 + 构建

```bash
cd "/Users/kk233/Library/Mobile Documents/iCloud~md~obsidian/Documents/手动脑子/.obsidian/plugins/ai-sidebar"
# 改 main.ts
npm run build
```

### 2. 测试

在 Obsidian 里刷新插件（设置 → 社区插件 → 关闭再打开 AI Sidebar），确认功能正常。

### 3. 改版本号

改两个文件：

**manifest.json**
```json
{
  "version": "0.2"
}
```

**package.json**
```json
{
  "version": "0.2"
}
```

### 4. 复制到 GitHub 仓库

```bash
cp main.ts main.js styles.css manifest.json package.json \
  "/Users/kk233/Documents/GitHub/obsidian-ai-sidebar/"
```

### 5. Commit + Push

GitHub Desktop：
- 填写 commit message，比如 `fix: 修复标签页丢失问题` 或 `feat: 添加搜索历史`
- Push origin

### 6. 发 GitHub Release

1. 打开 `https://github.com/anewme7/obsidian-ai-sidebar/releases`
2. 点 **Create a new release**
3. **Choose a tag**：输入 `0.2` → **Create new tag**
4. **Release title**：`0.2`
5. Description 写这次改了什么（简洁几条）
6. 上传 `main.js`、`manifest.json`、`styles.css`
7. 点 **Publish release**

---

## 重要：Obsidian 社区插件自动更新

你的插件一旦被收录到 `community-plugins.json`，**后续更新不需要再提 PR**。

Obsidian 会：
1. 定期检查你的 GitHub repo
2. 读取 latest release 的 `manifest.json`
3. 对比用户本地版本
4. 有新版本就提示用户更新

所以你只要做好两件事：
- ✅ manifest.json 里的 `version` 正确递增
- ✅ GitHub Release 的 tag 和 version 一致

---

## Commit 信息规范（建议）

```
fix: 修复标签页重启丢失
feat: 添加拖拽排序功能
docs: 更新 README
chore: 删除不需要的文件
```

这样以后看 commit 历史很清楚。
