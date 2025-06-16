# 前端工程師專用 Cursor User Rules 配置

## 🎨 前端工程師角色配置

```yaml
# 前端工程師專用設定
USER_ROLE: "frontend-dev"
specialization: "frontend"
primary_technologies: ["React", "TypeScript", "CSS", "HTML"]
focus_areas: ["UI/UX", "Performance", "Accessibility", "User Experience"]
```

---

## § 1 前端特化核心設定

### 1.1 技術棧優先配置 (2025年標準)

```yaml
FRONTEND_TECH_STACK:
  languages:
    primary: ["TypeScript", "JavaScript"]
    styling: ["CSS3", "SCSS", "PostCSS"]
    markup: ["HTML5", "JSX", "TSX"]
    
  frameworks:
    react_ecosystem: ["React 18", "Next.js 14", "Remix"]
    vue_ecosystem: ["Vue 3", "Nuxt 3", "Quasar"]
    angular_ecosystem: ["Angular 17", "Ionic"]
    meta_frameworks: ["Astro", "SvelteKit"]
    
  build_tools:
    bundlers: ["Vite", "Webpack 5", "esbuild", "Rollup"]
    task_runners: ["npm scripts", "Turborepo"]
    package_managers: ["npm", "yarn", "pnpm"]
    
  development_tools:
    dev_servers: ["Vite dev", "Webpack dev server"]
    hot_reload: ["React Fast Refresh", "Vue HMR"]
    browser_tools: ["React DevTools", "Vue DevTools"]
    
  styling_solutions:
    css_frameworks: ["Tailwind CSS", "Bootstrap 5", "Bulma"]
    css_in_js: ["Styled-components", "Emotion", "Vanilla Extract"]
    component_libraries: ["Material-UI", "Ant Design", "Chakra UI"]
    
  state_management:
    client_state: ["Zustand", "Redux Toolkit", "Jotai", "Valtio"]
    server_state: ["React Query", "SWR", "Apollo Client"]
    form_state: ["React Hook Form", "Formik", "Zod"]
    
  testing_framework:
    unit_testing: ["Vitest", "Jest", "@testing-library/react"]
    integration: ["Testing Library", "Enzyme (legacy)"]
    e2e_testing: ["Playwright", "Cypress", "Puppeteer"]
    visual_testing: ["Storybook", "Chromatic", "Percy"]
```

### 1.2 前端專用開發流程

**MVP階段 (個人專案)**：
```yaml
mvp_frontend_workflow:
  setup:
    - "建立React/Vue專案骨架"
    - "設定基本路由"
    - "實作核心UI組件"
    
  development:
    - "使用組件化開發方式"
    - "實作基本響應式設計"
    - "整合狀態管理"
    
  quality:
    - "基本Lighthouse檢查"
    - "跨瀏覽器測試"
    - "基礎無障礙性檢查"
```

**標準階段 (小團隊)**：
```yaml
standard_frontend_workflow:
  setup:
    - "TypeScript嚴格模式"
    - "ESLint + Prettier配置"
    - "Storybook組件文檔"
    
  development:
    - "設計系統建立"
    - "組件測試覆蓋"
    - "效能監控整合"
    
  quality:
    - "自動化視覺回歸測試"
    - "Bundle分析和優化"
    - "Core Web Vitals監控"
```

**企業階段 (大型團隊)**：
```yaml
enterprise_frontend_workflow:
  setup:
    - "微前端架構考量"
    - "完整CI/CD管道"
    - "多環境配置管理"
    
  development:
    - "代碼分割策略"
    - "國際化(i18n)支援"
    - "PWA功能實作"
    
  quality:
    - "完整E2E測試套件"
    - "效能預算控制"
    - "安全性檢查整合"
```

---

## § 2 前端品質門檻標準

### 2.1 效能指標要求

```yaml
FRONTEND_PERFORMANCE_GATES:
  core_web_vitals:
    LCP: "≤ 2.5s"        # Largest Contentful Paint
    FID: "≤ 100ms"       # First Input Delay
    CLS: "≤ 0.1"         # Cumulative Layout Shift
    
  lighthouse_scores:
    performance: "≥ 90"
    accessibility: "≥ 95"
    best_practices: "≥ 90"
    seo: "≥ 85"
    
  bundle_optimization:
    initial_js: "≤ 150KB gzipped"
    initial_css: "≤ 50KB gzipped"
    total_bundle: "≤ 500KB gzipped"
    
  runtime_performance:
    first_paint: "≤ 1.5s"
    time_to_interactive: "≤ 3.5s"
    total_blocking_time: "≤ 200ms"
```

### 2.2 程式碼品質標準

```yaml
FRONTEND_CODE_QUALITY:
  linting:
    eslint_errors: "0"
    eslint_warnings: "≤ 5"
    typescript_errors: "0"
    
  testing:
    unit_coverage: "≥ 80%"
    component_coverage: "≥ 85%"
    integration_coverage: "≥ 70%"
    
  accessibility:
    wcag_level: "AA"
    color_contrast: "≥ 4.5:1"
    keyboard_navigation: "100%"
    screen_reader_support: "完整"
    
  browser_support:
    modern_browsers: "最新2個版本"
    ie_support: "可選，依專案需求"
    mobile_browsers: "iOS Safari, Chrome Mobile"
```

---

## § 3 前端專用工具配置

### 3.1 開發環境設定

```json
// package.json scripts 建議
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "test": "vitest",
    "test:ui": "vitest --ui",
    "test:e2e": "playwright test",
    "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "lint:fix": "eslint . --ext ts,tsx --fix",
    "format": "prettier --write \"src/**/*.{ts,tsx,css,md}\"",
    "storybook": "storybook dev -p 6006",
    "build-storybook": "storybook build",
    "lighthouse": "lhci autorun",
    "bundle-analyzer": "npm run build && npx vite-bundle-analyzer dist"
  }
}
```

### 3.2 VSCode/Cursor 推薦擴展

```json
// .vscode/extensions.json
{
  "recommendations": [
    "bradlc.vscode-tailwindcss",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "ms-vscode.vscode-typescript-next",
    "formulahendry.auto-rename-tag",
    "christian-kohler.path-intellisense",
    "ms-playwright.playwright",
    "ms-vscode.vscode-css-peek",
    "csstools.postcss"
  ]
}
```

---

## § 4 前端專用自然語言指令

### 4.1 組件開發指令

```bash
# 組件相關
create-component [ComponentName]     # 建立新組件（含測試和故事）
refactor-component [ComponentName]   # 重構現有組件
test-component [ComponentName]       # 執行組件測試
story-component [ComponentName]      # 建立Storybook故事

# 頁面相關
create-page [PageName]              # 建立新頁面
optimize-page [PageName]            # 優化頁面效能
audit-page [PageName]               # 頁面品質稽核

# 樣式相關
create-theme                        # 建立設計系統主題
optimize-css                        # CSS優化和清理
check-a11y                         # 無障礙性檢查
```

### 4.2 效能優化指令

```bash
# 效能分析
analyze-bundle                      # 分析Bundle大小
measure-performance                 # 效能指標測量
optimize-images                     # 圖片優化
lazy-load [ComponentName]          # 實作懶載入

# 建置優化
code-split [RouteName]             # 實作代碼分割
tree-shake                         # 移除死代碼
compress-assets                    # 資產壓縮
```

---

## § 5 前端專用TODO模板

### 5.1 功能開發TODO

```markdown
## TODO-P1-FEAT-FRONTEND-用戶界面改善

**建立時間**: 2025-06-16T10:49:55+08:00
**負責人**: @{{USER_ROLE}}
**預計完成**: 2025-06-23T23:59:59+08:00
**狀態**: 待開始
**專案階段**: 標準

### 前端特定需求
- **組件**: 需要建立的新組件清單
- **頁面**: 需要更新的頁面
- **路由**: 路由變更需求
- **狀態**: 狀態管理更新

### 設計規格
- **設計稿**: Figma連結
- **互動規格**: 使用者互動流程
- **響應式**: 斷點和適配需求
- **動畫**: 動畫效果規格

### 技術實作
- [ ] 建立基礎組件結構
- [ ] 實作響應式佈局
- [ ] 整合狀態管理
- [ ] 撰寫組件測試
- [ ] 建立Storybook故事
- [ ] 效能優化檢查

### 品質檢查
- [ ] 跨瀏覽器測試完成
- [ ] 無障礙性檢查通過
- [ ] Lighthouse分數達標
- [ ] 視覺回歸測試通過
```

---

## § 6 前端學習成長路徑

### 6.1 技能發展階梯

**初級前端工程師**：
- HTML5語義化標籤熟練運用
- CSS3現代特性和Flexbox/Grid
- JavaScript ES6+語法和DOM操作
- 基礎React或Vue框架使用

**中級前端工程師**：
- TypeScript型別系統掌握
- 狀態管理最佳實踐
- 建置工具配置和優化
- 測試驅動開發實踐

**高級前端工程師**：
- 前端架構設計能力
- 效能優化深度技能
- 跨瀏覽器相容性處理
- 團隊技術領導能力

**前端架構師**：
- 大型前端系統設計
- 微前端架構實作
- 技術選型決策能力
- 團隊技能培養規劃

### 6.2 2025年重點學習領域

```yaml
learning_priorities_2025:
  core_technologies:
    - "React Server Components深度應用"
    - "Vue 3 Composition API進階模式"
    - "CSS Container Queries實用技巧"
    - "Web Components標準化開發"
    
  performance_optimization:
    - "Core Web Vitals深度優化"
    - "Runtime Performance分析"
    - "Critical Resource Optimization"
    - "Progressive Enhancement策略"
    
  developer_experience:
    - "Vite進階配置和插件開發"
    - "TypeScript進階型別技巧"
    - "Testing Library最佳實踐"
    - "Storybook進階應用"
    
  emerging_trends:
    - "AI輔助前端開發工具"
    - "WebAssembly前端應用"
    - "Edge-side Rendering"
    - "Micro Frontend架構模式"
```

---

## § 7 前端項目檢查清單

### 7.1 專案啟動檢查

- [ ] **技術棧選擇**：確認框架、建置工具、樣式解決方案
- [ ] **開發環境**：Cursor/VSCode擴展、linting規則、格式化設定
- [ ] **專案結構**：資料夾組織、命名規範、檔案模板
- [ ] **設計系統**：顏色、字體、間距、組件規範

### 7.2 開發中檢查

- [ ] **組件設計**：可重用性、props interface、預設值
- [ ] **狀態管理**：狀態結構、資料流、副作用處理
- [ ] **效能考量**：懶載入、記憶化、bundle splitting
- [ ] **測試覆蓋**：單元測試、整合測試、快照測試

### 7.3 發布前檢查

- [ ] **跨瀏覽器測試**：主要瀏覽器兼容性驗證
- [ ] **響應式測試**：各種螢幕尺寸適配檢查
- [ ] **無障礙性檢查**：鍵盤導航、螢幕閱讀器支援
- [ ] **效能驗證**：Lighthouse分數、Core Web Vitals
- [ ] **SEO優化**：meta標籤、結構化資料、sitemap

---

## § 8 前端緊急問題處理

### 8.1 常見問題快速修復

**效能問題**：
```bash
# 快速效能診斷
npm run lighthouse
npm run bundle-analyzer
npm run performance-audit
```

**建置問題**：
```bash
# 清理和重建
rm -rf node_modules package-lock.json
npm install
npm run build
```

**樣式問題**：
```bash
# CSS清理和重建
npm run clean-css
npm run build-css
npm run lint:css
```

### 8.2 緊急部署檢查

- [ ] **建置成功**：所有資產正確產生
- [ ] **功能驗證**：核心功能正常運作
- [ ] **樣式確認**：UI顯示正確
- [ ] **響應速度**：頁面載入時間可接受
- [ ] **錯誤監控**：沒有JavaScript錯誤

---

**前端工程師專用配置完成！** 🎨

此配置專為前端開發優化，提供：
- ✅ 前端特化的技術棧和工具
- ✅ 效能和品質門檻標準
- ✅ 組件化開發流程指導
- ✅ 現代前端最佳實踐
- ✅ 學習成長路徑規劃

立即開始您的高效前端開發之旅！