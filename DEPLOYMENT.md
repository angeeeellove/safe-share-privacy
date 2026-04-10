# 隐私政策和服务条款部署指南

## 文件结构

```
docs/
├── index.html            # 主入口（导航页面）
├── legal/                # 法律文档文件夹
│   ├── privacy.html       # 隐私政策（英文）
│   ├── privacy-zh.html    # 隐私政策（中文）
│   ├── terms.html         # 服务条款（英文）
│   └── terms-zh.html      # 服务条款（中文）
├── DEPLOYMENT.md          # 本部署指南
└── README.md             # 项目说明
```

## 文件说明

| 文件 | 语言 | 说明 |
|------|------|------|
| `index.html` | - | **主入口**，导航到各法律文档 |
| `legal/privacy.html` | 英文 | 隐私政策 |
| `legal/privacy-zh.html` | 中文 | 隐私政策（简体中文） |
| `legal/terms.html` | 英文 | 服务条款 |
| `legal/terms-zh.html` | 中文 | 服务条款（简体中文） |

## GitHub Pages 部署步骤

### 方案 1: 使用项目的 `/docs` 文件夹（推荐）

1. **将文件推送到 GitHub**
   ```bash
   git add docs/
   git commit -m "Add privacy policy and terms of service"
   git push
   ```

2. **启用 GitHub Pages**
   - 进入仓库 Settings → Pages
   - Source → Deploy from a branch
   - Branch → `main` (或 `master`)
   - Folder → `/docs`
   - 点击 Save

3. **获取 URL**

   访问 `https://your-username.github.io/SecureCard/` 会自动显示 `docs/index.html`

   各文档的直接链接：
   ```
   https://your-username.github.io/SecureCard/                       # 导航页
   https://your-username.github.io/SecureCard/legal/privacy.html      # 英文隐私政策
   https://your-username.github.io/SecureCard/legal/privacy-zh.html   # 中文隐私政策
   https://your-username.github.io/SecureCard/legal/terms.html        # 英文服务条款
   https://your-username.github.io/SecureCard/legal/terms-zh.html     # 中文服务条款
   ```

### 方案 2: 使用独立仓库

1. **创建新仓库** (例如: `securecard-legal`)

2. **将文件移至根目录并推送**
   ```bash
   cp docs/*.html ../securecard-legal/
   cd ../securecard-legal
   git add .
   git commit -m "Add legal documents"
   git push
   ```

3. **启用 GitHub Pages**
   - 进入仓库 Settings → Pages
   - Source → Deploy from a branch
   - Branch → `main`
   - Folder → `/ (root)`

4. **获取 URL**
   ```
   https://your-username.github.io/securecard-legal/privacy.html
   https://your-username.github.io/securecard-legal/terms.html
   ```

## 更新移动端配置

编辑 `mobile/lib/core/constants/app_constants.dart`:

```dart
// 更新为你的实际 GitHub Pages URL
static const String _legalBaseUrl = 'https://your-username.github.io/SecureCard';
```

## 多语言支持

当前支持的语言：

| 语言代码 | 隐私政策 | 服务条款 |
|---------|---------|---------|
| `en` (英语) | `legal/privacy.html` | `legal/terms.html` |
| `zh` (中文) | `legal/privacy-zh.html` | `legal/terms-zh.html` |
| 其他语言 | 回退到英语版本 | 回退到英语版本 |

App 会根据用户的语言设置自动跳转到对应的文档版本。

## 添加更多语言

如需添加其他语言版本：

1. **创建 HTML 文件**
   - 复制 `legal/privacy.html` → `legal/privacy-es.html` (西班牙语)
   - 复制 `legal/terms.html` → `legal/terms-es.html`

2. **翻译内容**
   - 翻译所有文本内容
   - 更新 `<html lang="es">` 属性

3. **更新 `app_constants.dart`**
   ```dart
   const langMap = {
     'zh': 'legal/privacy-zh.html',
     'es': 'legal/privacy-es.html',  // 添加这行
     'en': 'legal/privacy.html',
   };
   ```

4. **更新 `index.html`**
   - 在中文部分下添加新的语言部分
   - 添加对应文档链接

3. **更新 `app_constants.dart`**
   ```dart
   const langMap = {
     'zh': 'privacy-zh.html',
     'es': 'privacy-es.html',  // 添加这行
     'en': 'privacy.html',
   };
   ```

## 应用商店配置

### Apple App Store
- App Store Connect → App → App Privacy → Privacy Policy URL
- 填入: `https://your-username.github.io/.../privacy.html`

### Google Play
- Play Console → Setup → Policy → Privacy policy URL
- 填入: `https://your-username.github.io/.../privacy.html`

## 测试清单

部署后请测试以下内容：

- [ ] 链接可以在移动端浏览器中正常打开
- [ ] 中文用户跳转到中文版本
- [ ] 英文用户跳转到英文版本
- [ ] 页面在手机上显示正常（响应式设计）
- [ ] 所有内部链接有效（如有）
- [ ] 联系邮箱准确

## 维护

### 定期更新
- 每年至少审查一次法律文档
- 法律变更时及时更新
- 更新 HTML 中的"最后更新"日期

### 更新流程
1. 修改 `docs/*.html` 文件
2. 提交并推送到 GitHub
3. GitHub Pages 会自动重新部署
4. 无需更新 App（因为链接指向外部）

## 自定义域名（可选）

如果使用自定义域名（如 `legal.securecard.app`）：

1. **创建 CNAME 文件**
   ```bash
   echo "legal.securecard.app" > docs/CNAME
   git add docs/CNAME
   git commit -m "Add custom domain"
   git push
   ```

2. **配置 DNS**
   - 在域名提供商处添加 CNAME 记录
   - 指向: `your-username.github.io`

3. **更新 App 配置**
   ```dart
   static const String _legalBaseUrl = 'https://legal.securecard.app';
   ```

## 常见问题

### Q: 页面更新后用户看到的还是旧版本？
A: 清除浏览器缓存或硬刷新（Ctrl+Shift+R）

### Q: GitHub Pages 显示 404？
A: 检查文件名大小写是否匹配，等待 1-2 分钟让 GitHub 部署完成

### Q: 如何确认 URL 正确？
A: 在浏览器中直接访问 URL，确认页面可正常显示

### Q: 需要购买域名吗？
A: 不需要。GitHub Pages 提供免费的 `github.io` 域名
