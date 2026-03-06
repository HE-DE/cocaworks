## Branch Rules
- base branches: main, develop, release
- purposes:
  - feature: feature/{scope}-{slug}
  - fix: fix/{scope}-{slug}
  - hotfix: hotfix/{scope}-{slug}
  - chore: chore/{scope}-{slug}

## Commit Rules
- commit types: feat, fix, chore, docs, refactor, test, misc, style
- commit template: {type}({scope}): {summary}
- merge template: merge({base}<-{work}): {purpose}

---

## 分支规则
- 基础分支: main, develop, release
- 分支目的:
  - feature: feature/{scope}-{slug}
  - fix: fix/{scope}-{slug}
  - hotfix: hotfix/{scope}-{slug}
  - chore: chore/{scope}-{slug}

## 提交规则
- 提交类型: feat, fix, chore, docs, refactor, test, misc, style
- 提交模板: {type}({scope}): {summary}
- 合并模板: merge({base}<-{work}): {purpose}

---

<!-- GITRULES:BEGIN -->
BASE_BRANCHES=main,develop,release
BRANCH_PURPOSES=feature:feature/{scope}-{slug};fix:fix/{scope}-{slug};hotfix:hotfix/{scope}-{slug};chore:chore/{scope}-{slug}
COMMIT_TYPES=feat,fix,chore,docs,refactor,test,misc,style
COMMIT_TEMPLATE={type}({scope}): {summary}
MERGE_TEMPLATE=merge({base}<-{work}): {purpose}
<!-- GITRULES:END -->
BASE_BRANCHES=main,develop,release
BRANCH_PURPOSES=feature:feature/{scope}-{slug};fix:fix/{scope}-{slug};hotfix:hotfix/{scope}-{slug};chore:chore/{scope}-{slug}
COMMIT_TYPES=feat,fix,chore,docs,refactor,test,misc,style
COMMIT_TEMPLATE={type}({scope}): {summary}
MERGE_TEMPLATE=merge({base}<-{work}): {purpose}