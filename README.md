# Cursor User Rules 2025 - 完整工程師最佳實踐配置

> 🚀 **全面、智能、循序漸進的開發配置系統**  
> 支援12種工程師角色，從個人Side Project到企業級系統的完整解決方案

![Version](https://img.shields.io/badge/version-2025.6.0-blue)
![Compatibility](https://img.shields.io/badge/cursor-v0.40%2B-green)
![License](https://img.shields.io/badge/license-MIT-green)
![Engineers](https://img.shields.io/badge/engineers-12%20roles-orange)

---

## ✨ 核心特色

### 🎯 智能專案檢測
- 自動識別專案類型（個人/新創/企業）
- 動態調整複雜度等級（MVP→標準→進階→企業）
- 避免過早優化和過度工程化

### 👥 全角色支援
支援12種工程師角色的專業化配置：
- 🎨 前端工程師 - React/Vue/Angular最佳實踐
- ⚙️ 後端工程師 - API設計與效能優化
- 🔄 全端工程師 - 端到端開發流程
- 📱 行動應用工程師 - iOS/Android/跨平台
- 🎮 遊戲開發工程師 - Unity/Unreal最佳實踐
- 🔌 嵌入式系統工程師 - 硬體軟體整合
- 📊 資料工程師 - 資料管道與品質管理
- 🤖 機器學習工程師 - MLOps與模型部署
- 🚀 DevOps工程師 - CI/CD與基礎設施
- 🔒 安全工程師 - 安全左移與合規
- ✅ QA工程師 - 測試策略與自動化
- 🏗️ 軟體架構師 - 系統設計與治理

### 🔄 循序漸進開發
- **MVP優先**：先實現核心功能，再逐步擴展
- **智能旗標**：根據專案階段自動啟用適當工具
- **品質門檻**：分階段的品質標準，確保可持續發展

### 📋 強制TODO管理
- 結構化的任務追蹤系統
- 自動進度更新與提醒
- 團隊協作與責任分工

---

## 🚀 快速開始

### 1. 立即設置（5分鐘）

```bash
# 1. 複製主配置文件到Cursor
# 前往：Cursor → Settings → User Rules
# 複製：cursor-user-rules-2025.md 的全部內容

# 2. 個人化設定
USER_ROLE: "your-name"              # ← 改成您的帳號
project_context: "personal"         # personal | enterprise | startup
development_style: "progressive"    # 循序漸進開發
```

### 2. 初始化專案

```bash
# 獲取當前時間（自動選擇系統對應指令）
get-current-time

# 初始化專案（自動檢測類型）
init-project

# 查看專案狀態
status
```

### 3. 開始第一個功能

```bash
# 建立MVP功能
mvp user-authentication

# 檢查品質
check-quality

# 查看下一步建議
roadmap
```

---

## 📁 專案結構

```
projects/UserRules/
├── cursor-user-rules-2025.md          # 主配置文件 ⭐
├── quick-setup-guide.md               # 5分鐘快速設置指南
├── README.md                          # 本文件
├── templates/
│   └── TODO-template.md               # TODO清單模板
├── roles/
│   ├── frontend-engineer.md           # 前端工程師專用配置
│   ├── backend-engineer.md            # 後端工程師專用配置
│   ├── fullstack-engineer.md          # 全端工程師專用配置
│   ├── mobile-engineer.md             # 行動應用工程師配置
│   ├── game-developer.md              # 遊戲開發工程師配置
│   ├── embedded-engineer.md           # 嵌入式系統工程師配置
│   ├── data-engineer.md               # 資料工程師配置
│   ├── ml-engineer.md                 # 機器學習工程師配置
│   ├── devops-engineer.md             # DevOps工程師配置
│   ├── security-engineer.md           # 安全工程師配置
│   ├── qa-engineer.md                 # QA工程師配置
│   └── software-architect.md          # 軟體架構師配置
└── tools/
    └── project-checker.md             # 專案檢查工具
```

---

## 🎯 根據角色選擇配置

### 👨‍💻 我是前端工程師
```bash
# 使用前端專用配置
cp roles/frontend-engineer.md my-frontend-config.md

# 或直接在主配置中設定
specialization: "frontend"
primary_technologies: ["React", "TypeScript", "CSS"]
```

**包含特色**：
- React 18+、Vue 3+、Angular 17+最新實踐
- Core Web Vitals效能優化
- 無障礙性(A11y)自動檢查
- Storybook元件文檔
- 視覺回歸測試

### 🔧 我是後端工程師
```bash
# 使用後端專用配置
specialization: "backend"
primary_technologies: ["Node.js", "Python", "Go"]
```

**包含特色**：
- FastAPI、Django、Express最佳實踐
- OpenAPI自動文檔生成
- 資料庫效能優化
- 微服務架構指導
- 安全性最佳實踐

### 📱 我是行動應用工程師
```bash
# 使用行動應用專用配置
specialization: "mobile"
primary_technologies: ["React Native", "Flutter", "Swift"]
```

**包含特色**：
- React Native 0.73+、Flutter 3.16+
- 原生iOS/Android開發支援
- 跨平台最佳實踐
- App Store部署自動化
- 效能與電池優化

### 🎮 我是遊戲開發工程師
```bash
# 使用遊戲開發專用配置
specialization: "game"
primary_technologies: ["Unity", "Unreal", "C#"]
```

**包含特色**：
- Unity 2023.3、Unreal Engine 5.3
- 大型資產版本控制
- 多平台建置自動化
- 效能分析與優化
- 遊戲測試框架

---

## 🛠️ 進階功能

### 🔄 智能旗標系統

根據專案階段自動啟用功能：

```yaml
# MVP階段（個人專案）
mvp_flags:
  - basic_linting      # 基礎代碼檢查
  - unit_testing       # 單元測試
  - simple_deployment  # 簡單部署

# 標準階段（小團隊）
standard_flags:
  - integration_testing  # 整合測試
  - automated_deployment # 自動化部署
  - security_scanning    # 安全掃描

# 企業階段（大型組織）
enterprise_flags:
  - compliance_checking  # 合規檢查
  - disaster_recovery   # 災害恢復
  - advanced_monitoring # 進階監控
```

### 📊 專案健康度檢查

使用內建的專案檢查工具：

```bash
# 執行完整檢查
cursor-check --full

# 生成HTML報告
cursor-check --report=html

# CI/CD整合
cursor-check --ci --fail-on-score=80
```

### 📝 智能TODO管理

自動管理和追蹤專案進度：

```markdown
## TODO-P1-FEAT-frontend-2025-06-23

**負責人**: @your-name
**狀態**: 進行中
**預估工時**: 8小時

### 接受條件
- [ ] 功能實作完成
- [ ] 單元測試覆蓋率 ≥ 80%
- [ ] 文檔更新完成
- [ ] 代碼審查通過
```

---

## 🎨 自然語言指令

使用簡單的中文指令完成複雜任務：

```bash
# 專案管理
init                    # 初始化專案
status                  # 查看專案狀態
roadmap                 # 顯示開發路線圖

# 功能開發
mvp 用戶登入            # 建立MVP版本功能
enhance 搜尋功能        # 增強現有功能
fix 效能問題           # 修復特定問題

# 品質控制
check-quality          # 執行品質檢查
security-audit         # 安全稽核
performance-test       # 效能測試

# 部署相關
deploy-mvp            # 部署MVP版本
deploy-production     # 部署到生產環境
rollback v1.2.0       # 回滾到特定版本
```

---

## 🔧 技術棧支援

### 前端技術 (2025年最新)
- **框架**: React 18+, Vue 3+, Angular 17+, Svelte 5+
- **建置工具**: Vite, Webpack 5, esbuild, Rollup
- **測試**: Vitest, Jest, Playwright, Cypress
- **樣式**: Tailwind CSS, Styled-components, CSS Modules

### 後端技術
- **語言**: Node.js 20+, Python 3.11+, Go 1.21+, Rust
- **框架**: FastAPI, Django 5, Express.js, Spring Boot 3
- **資料庫**: PostgreSQL 16, MongoDB 6, Redis 7
- **容器化**: Docker, Kubernetes, Helm

### 行動應用
- **跨平台**: React Native 0.73+, Flutter 3.16+, Expo 50+
- **原生iOS**: Swift 5.9, SwiftUI, Combine
- **原生Android**: Kotlin, Jetpack Compose, Coroutines

### DevOps & 雲端
- **CI/CD**: GitHub Actions, GitLab CI, Jenkins
- **雲端平台**: AWS, GCP, Azure, Cloudflare
- **監控**: Prometheus, Grafana, Datadog

---

## 📈 效能與品質標準

### 前端品質門檻
- **Lighthouse分數**: ≥ 90（所有類別）
- **Core Web Vitals**: LCP ≤ 2.5s, FID ≤ 100ms, CLS ≤ 0.1
- **Bundle大小**: ≤ 500KB gzipped
- **測試覆蓋率**: ≥ 80%

### 後端品質門檻
- **API回應時間**: ≤ 200ms (P95)
- **資料庫查詢**: ≤ 100ms (P95)
- **系統可用性**: ≥ 99.9%
- **安全漏洞**: 0個高危漏洞

### 通用品質標準
- **程式碼品質**: 0個ESLint錯誤
- **安全性**: OWASP Top 10防護
- **文檔完整性**: 100% API文檔覆蓋
- **版本控制**: Conventional Commits格式

---

## 🚀 成功案例

### 個人Side Project → 獨角獸公司
```yaml
階段演進:
  MVP (1個月):
    - 核心功能實作
    - 基礎UI介面
    - 簡單部署
    
  成長期 (6個月):
    - 功能擴展
    - 效能優化
    - 用戶分析
    
  規模化 (2年):
    - 微服務架構
    - 國際化支援
    - 企業級安全性
```

### 企業數位轉型
```yaml
轉型成果:
  開發效率: +300%
  代碼品質: +250%
  部署頻率: 每日10次
  系統可用性: 99.99%
```

---

## 🤝 社群與支援

### 🙋‍♂️ 獲得幫助
- 📖 **文檔**: 查看對應角色的配置文件
- 🔧 **工具**: 使用專案檢查工具診斷問題
- 💬 **社群**: 加入開發者社群討論

### 🐛 問題報告
如果您遇到問題：
1. 檢查是否為已知問題
2. 使用`cursor-check`診斷專案
3. 提供詳細的錯誤描述
4. 附上專案配置資訊

### 💡 功能建議
我們歡迎您的建議：
- 新的工程師角色支援
- 額外的技術棧整合
- 工作流程改善建議
- 工具與整合需求

---

## 📅 版本與更新

### 當前版本: 2025.6.0
- ✅ 支援12種工程師角色
- ✅ 智能專案檢測系統
- ✅ 循序漸進開發指導
- ✅ 強制TODO管理機制
- ✅ 專案健康度檢查工具

### 即將推出的功能
- 🔄 AI輔助代碼生成整合
- 📊 更智能的效能監控
- 🌐 多語言國際化支援
- 🔗 更多第三方工具整合

### 更新頻率
- **主要版本**: 每季更新（增加新功能）
- **次要版本**: 每月更新（改善與修復）
- **補丁版本**: 即時更新（緊急修復）

---

## 📜 授權條款

本專案採用 MIT 授權條款，您可以自由：
- ✅ 商業使用
- ✅ 修改和分發
- ✅ 私人使用
- ✅ 專利使用

---

## 🎉 立即開始

準備好提升您的開發效率了嗎？

1. **複製主配置**: 將`cursor-user-rules-2025.md`貼到Cursor User Rules
2. **選擇角色**: 找到適合您的角色配置文件
3. **初始化專案**: 使用`init`指令開始
4. **享受開發**: 體驗智能化的開發流程

---

<div align="center">

**🚀 開始您的高效開發之旅 🚀**

[快速設置](quick-setup-guide.md) • [角色配置](roles/) • [工具文檔](tools/) • [模板文件](templates/)

</div>

---

<div align="center">
<small>

**Cursor User Rules 2025** - 讓每一行代碼都有意義  
Made with ❤️ for developers worldwide

</small>
</div>