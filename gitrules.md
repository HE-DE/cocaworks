# Git 工作规范

## 1. 提交信息规范

### 1.1 提交信息格式

```
<类型>(<范围>): <描述>

[可选的正文]

[可选的脚注]
```

### 1.2 类型说明

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` / `feature` | 新功能 | `feat(auth): 添加登录功能` |
| `fix` / `bugfix` | Bug 修复 | `fix(api): 修复用户请求超时问题` |
| `refactor` | 代码重构 | `refactor(utils): 优化工具函数` |
| `docs` | 文档更新 | `docs(readme): 更新安装说明` |
| `chore` | 日常维护 | `chore(deps): 升级依赖版本` |
| `misc` | 其他更改 | `misc: 调整代码格式` |
| `style` | 代码格式 | `style: 格式化代码` |
| `test` | 测试相关 | `test(unit): 添加单元测试` |

### 1.3 提交信息规则

- **标题行**：使用中文或英文均可，保持简洁，不超过 50 个字符
- **正文**：描述「做什么」和「为什么」，每行不超过 72 个字符
- **脚注**：记录重大变更（BREAKING CHANGE）

### 1.4 示例

```
feat(user): 添加用户头像上传功能

- 支持 JPG、PNG 格式
- 最大文件大小 2MB
- 上传成功后自动裁剪为圆形

Closes #123
```

---

## 2. 分支命名规则

### 2.1 分支类型前缀

| 前缀 | 用途 | 示例 |
|------|------|------|
| `feature/` | 新功能开发 | `feature/user-profile` |
| `bugfix/` | Bug 修复 | `bugfix/login-error` |
| `refactor/` | 代码重构 | `refactor/api-handler` |
| `docs/` | 文档更新 | `docs/api-reference` |
| `hotfix/` | 紧急修复 | `hotfix/security-patch` |
| `release/` | 发布准备 | `release/v1.0.0` |

### 2.2 分支命名规范

- 使用小写字母、数字和连字符（`-`）
- 包含对应的任务或问题编号（如有）
- 名称简洁明了，不超过 30 个字符

### 2.3 示例

```
feature/add-payment-module
bugfix/fix-login-timeout-#456
release/v1.2.0
hotfix/critical-security-issue
```

---

## 3. 合并规则

### 3.1 分支策略

- **主分支**：`main` / `master` - 仅通过合并请求更新
- **开发分支**：`develop` - 开发主分支
- **功能分支**：从 `develop` 创建，开发完成后合并回 `develop`
- **发布分支**：从 `develop` 创建，发布完成后合并到 `main` 和 `develop`
- **修复分支**：从 `main` 创建，修复完成后合并到 `main` 和 `develop`

### 3.2 合并流程

1. **创建功能分支**
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/xxx
   ```

2. **开发并提交**
   ```bash
   git add .
   git commit -m "feat(xxx): 添加新功能"
   ```

3. **同步上游更改**
   ```bash
   git fetch origin
   git rebase origin/develop
   ```

4. **推送并创建合并请求**
   ```bash
   git push -u origin feature/xxx
   ```

### 3.3 合并要求

- 所有功能分支必须通过代码审查（Code Review）后才能合并
- 合并前确保本地测试通过
- 合并时使用 `Squash Merge` 或 `Rebase Merge` 保持历史清晰
- 合并信息应清晰描述本次合并的内容

### 3.4 冲突处理

- 优先使用 `rebase` 解决冲突，避免使用 `merge`
- 解决冲突后需要重新进行代码审查

---

## 4. 注意事项

- 保持提交粒度适中，每个提交应有明确的目的
- 提交信息应清晰描述更改内容，便于追溯
- 定期同步上游分支，避免长时间落后
- 禁止直接在主分支进行提交
