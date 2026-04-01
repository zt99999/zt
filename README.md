# M3U 文件自动同步到 Gitee

自动从 GitHub 下载 M3U 直播源文件，去掉第二行后推送到 Gitee。

## 配置步骤

### 1. 在 GitHub 上创建仓库
```bash
# 创建新仓库（私有或公开均可）
gh repo create m3u-auto-sync --public
```

### 2. 配置 GitHub Secrets 和 Variables

#### Secrets（设置 → Secrets and variables → Actions → New repository secret）
- **GITEE_TOKEN**: 你的 Gitee 个人访问令牌

#### Variables（设置 → Secrets and variables → Actions → Variables → New repository variable）
- **GITEE_OWNER**: 你的 Gitee 用户名
- **GITEE_REPO**: 目标 Gitee 仓库名

### 3. 获取 Gitee Token
1. 访问 https://gitee.com/profile/personal_access_tokens
2. 创建新令牌，勾选 `projects` 权限
3. 复制令牌并填入 GitHub Secrets

### 4. 在 Gitee 创建仓库
在你的 Gitee 账号下创建一个空仓库（名称与 `GITEE_REPO` 一致）

### 5. 推送到 GitHub
```bash
git init
git add .
git commit -m "init: m3u auto sync workflow"
git branch -M main
git remote add origin https://github.com/你的用户名/m3u-auto-sync.git
git push -u origin main
```

## 运行方式

### 自动运行
每天北京时间 08:00 自动执行

### 手动触发
1. 进入 GitHub 仓库
2. 点击 Actions 标签
3. 选择 "Sync M3U to Gitee"
4. 点击 "Run workflow"

## 文件说明
- `.github/workflows/sync.yml` - GitHub Actions 工作流配置
- `Jsnzkpg1.m3u` - 处理后生成的文件（在 Gitee 仓库中）

## 修改同步频率
编辑 `sync.yml` 中的 cron 表达式：
```yaml
on:
  schedule:
    - cron: '0 0 * * *'  # 每天 00:00 UTC
```

常用 cron 表达式：
- `0 */6 * * *` - 每 6 小时
- `0 0 */2 * *` - 每 2 天
- `0 0 * * 1` - 每周一
