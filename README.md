# GitHub Pages 部署指南

本指南说明如何将隐私政策和服务条款部署到 GitHub Pages。

## 步骤 1: 创建 GitHub Pages 仓库

1. 在 GitHub 上创建一个新仓库（例如：`securecard-docs`）
2. 或者使用现有的 `SecureCard` 仓库

## 步骤 2: 启用 GitHub Pages

### 方案 A: 使用专用文档仓库

1. 进入仓库 Settings → Pages
2. Source 选择: Deploy from a branch
3. Branch 选择: `main` 或 `master`，文件夹: `/ (root)`
4. 点击 Save

### 方案 B: 使用现有仓库的 docs 文件夹

1. 进入仓库 Settings → Pages
2. Source 选择: Deploy from a branch
3. Branch 选择: `main` 或 `master`，文件夹: `/docs`
4. 点击 Save

## 步骤 3: 部署文件

### 如果使用 docs 文件夹（推荐）

```bash
# 在项目根目录
git add docs/
git commit -m "Add privacy policy and terms of service"
git push
```

### 如果使用独立仓库

```bash
# 复制文件到独立仓库
cp docs/privacy.html ../securecard-docs/
cp docs/terms.html ../securecard-docs/
cd ../securecard-docs
git add .
git commit -m "Add legal documents"
git push
```

## 步骤 4: 获取 URL

GitHub Pages URL 格式：

| 仓库类型 | URL 格式 | 示例 |
|---------|---------|------|
| 用户/组织页面 | `https://username.github.io/` | `https://john.github.io/` |
| 项目页面 | `https://username.github.io/repository-name/` | `https://john.github.io/securecard-docs/` |
| 使用 docs/ 文件夹 | `https://username.github.io/repository-name/docs/` | `https://john.github.io/SecureCard/docs/` |

## 步骤 5: 更新移动端 URL

编辑 `mobile/lib/core/constants/app_constants.dart`:

```dart
// 替换为你的实际 GitHub Pages URL
static const String privacyPolicyUrl = 'https://your-username.github.io/securecard-docs/privacy.html';
static const String termsOfServiceUrl = 'https://your-username.github.io/securecard-docs/terms.html';

// 或者如果使用 docs 文件夹
static const String privacyPolicyUrl = 'https://your-username.github.io/SecureCard/docs/privacy.html';
static const String termsOfServiceUrl = 'https://your-username.github.io/SecureCard/docs/terms.html';
```

## 步骤 6: 强制刷新（如果页面未更新）

在浏览器中打开隐私政策页面时，如果看不到更新：

1. **硬刷新**: Ctrl + Shift + R (Windows) 或 Cmd + Shift + R (Mac)
2. **清除缓存**: 浏览器设置 → 清除缓存
3. **GitHub Pages 延迟**: 部署通常需要 1-2 分钟

## 自定义域名（可选）

如果使用自定义域名：

1. 在 `docs/` 文件夹创建 `CNAME` 文件
2. 文件内容只需写你的域名（例如：`legal.securecard.app`）
3. 在域名 DNS 设置中添加 CNAME 记录指向 `your-username.github.io`

## 多语言支持

如需添加其他语言版本，创建对应文件：

- `privacy-zh.html` (中文)
- `privacy-es.html` (西班牙语)
- `privacy-fr.html` (法语)

然后在 `app_constants.dart` 中根据语言设置不同 URL。

## 安全检查清单

- [ ] 隐私政策包含所有必要条款（GDPR、CCPA 等）
- [ ] 服务条款明确定义用户责任和限制
- [ ] 联系邮箱已更新为实际邮箱
- [ ] GitHub Pages URL 在移动端应用中正确配置
- [ ] 文档可公开访问（无登录要求）
- [ ] URL 链接在移动端测试可正常打开
