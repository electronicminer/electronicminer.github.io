# 邮件链接和联系方式修复指南

## 问题描述
- 🔴 点击邮件图标没有反应
- 🔴 也不显示联系方式

## 已完成的修复

### 1. 清理重复配置 ✅
已从 `_config.yml` 中删除重复的社交媒体配置，确保所有配置统一来自 `_data/socials.yml`。

## 当前配置检查

### 社交媒体配置 (_data/socials.yml)
```yaml
email: wangpan040930@163.com
github_username: electronicminer
cv_pdf: /assets/pdf/example_pdf.pdf
```

### 页面设置 (_pages/about.md)
```yaml
social: true  # ✅ 已启用
```

### 导航栏设置 (_config.yml)
```yaml
enable_navbar_social: true  # ✅ 已启用
```

## 接下来的步骤

### 方案 A：重新编译（推荐）
```bash
# 清空旧的编译缓存
docker compose down

# 重新编译项目
docker compose up --build

# 访问 http://localhost:8080 测试
```

**测试清单：**
- [ ] 关于页面显示社交媒体图标
- [ ] 导航栏右侧显示社交媒体图标  
- [ ] 邮件图标可点击，打开邮客户端或 mailto: 链接
- [ ] GitHub 链接可点击

### 方案 B：手动测试邮件链接

如果仍然无法显示，请检查浏览器开发者工具：

1. **打开浏览器开发者工具** (F12)
2. **切换到 Elements/Inspector 标签** 
3. **在关于页面搜索邮件元素：**
   - Ctrl+F 搜索 `wangpan040930@163.com`
   - 或搜索 `mailto:`
   - 或搜索 `contact-icons`

4. **查看生成的 HTML 是否如下所示：**
   ```html
   <a href="mailto:email@...">
     <i class="fas fa-envelope"></i>
   </a>
   ```

## 如果还是不显示

### 检查清单：
- [ ] `_data/socials.yml` 邮箱地址是否正确无空格
- [ ] `about.md` 中 `social: true` 是否存在
- [ ] CSS 是否正确加载（检查浏览器控制台警告）
- [ ] 浏览器缓存是否已清除 (Ctrl+Shift+Del)

### 备选方案：使用简化的邮件配置

如果 jekyll-socials 插件有问题，可以考虑在 about.md 中直接添加：

```markdown
## 联系方式

📧 **邮箱:** [wangpan040930@163.com](mailto:wangpan040930@163.com)  
🐙 **GitHub:** [@electronicminer](https://github.com/electronicminer)
```

## 常见错误日志

如果编译失败，查看以下可能的错误：

```
Error: Could not find jekyll-socials
Error: Email protect failed
```

**解决方法：**
```bash
# 更新 Gem 依赖
docker compose down
docker compose up --build
```

## 相关文件

- 社交媒体配置: `_data/socials.yml`
- 页面配置: `_pages/about.md`
- 整体配置: `_config.yml`
- 邮件样式: `_sass/_components.scss` (line 177)
- 导航栏样式: `_sass/_navbar.scss`
- 导航栏模板: `_includes/header.liquid`
- 关于页面模板: `_layouts/about.liquid`
