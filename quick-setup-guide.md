# Cursor User Rules 2025 - 快速設置指南

## 🚀 5分鐘快速開始

### 步驟1：複製主配置文件（30秒）
1. 開啟 `cursor-user-rules-2025.md`
2. 複製全部內容
3. 前往 Cursor → Settings → User Rules
4. 貼上配置內容

### 步驟2：個人化設定（1分鐘）
```yaml
# 修改這些設定
USER_ROLE: "your-name"              # ← 改成您的帳號名稱
project_context: "personal"         # personal | enterprise | startup | research
development_style: "progressive"    # minimal | standard | comprehensive | enterprise
team_size: "solo"                  # solo | small | medium | large
deployment_target: "cloud"         # local | cloud | hybrid | edge
```

### 步驟3：選擇您的主要角色（1分鐘）
根據您的主要工作選擇對應的角色配置：

**前端開發者**：
```bash
# 在專案目錄執行
cursor-init --role=frontend --style=progressive
```

**後端開發者**：
```bash
cursor-init --role=backend --style=progressive
```

**全端開發者**：
```bash
cursor-init --role=fullstack --style=progressive
```

**其他角色**：請參考對應的角色配置文件

### 步驟4：初始化您的專案（2分鐘）
```bash
# 獲取當前時間（系統會自動選擇對應指令）
get-current-time

# 初始化專案
init-project

# 檢查專案狀態
check-status

# 開始第一個功能開發
mvp first-feature
```

### 步驟5：驗證設置（30秒）
```bash
# 執行品質檢查
check-quality

# 查看TODO清單
show-todos

# 檢查版本資訊
show-version
```

## 🎯 依據專案類型的快速設置

### 個人Side Project
```yaml
USER_ROLE: "your-name"
project_context: "personal"
development_style: "minimal"
team_size: "solo"
deployment_target: "cloud"
```

**推薦旗標**：
- `mvp_stage`: 基礎功能優先
- `simple_deployment`: 簡化部署
- `basic_testing`: 基本測試

### 新創公司MVP
```yaml
USER_ROLE: "your-name"
project_context: "startup"
development_style: "standard"
team_size: "small"
deployment_target: "cloud"
```

**推薦旗標**：
- `standard_stage`: 平衡功能與速度
- `automated_deployment`: 自動化部署
- `user_analytics`: 用戶分析

### 企業級專案
```yaml
USER_ROLE: "your-name"
project_context: "enterprise"
development_style: "enterprise"
team_size: "large"
deployment_target: "hybrid"
```

**推薦旗標**：
- `enterprise_stage`: 完整企業功能
- `compliance_checking`: 合規檢查
- `disaster_recovery`: 災害恢復

## 🔧 常用指令速查

### 專案管理
```bash
init                    # 初始化專案
status                  # 查看專案狀態
roadmap                 # 顯示開發路線圖
update-todos           # 更新TODO清單
```

### 開發流程
```bash
mvp [feature]          # 開始MVP功能
enhance [feature]      # 增強功能
fix [issue]            # 修復問題
optimize [aspect]      # 優化特定方面
```

### 品質控制
```bash
check-quality          # 品質檢查
security-audit         # 安全稽核
performance-test       # 效能測試
lint-fix              # 自動修復Lint問題
```

### 部署相關
```bash
deploy-mvp            # 部署MVP
deploy-staging        # 部署測試環境
deploy-production     # 部署生產環境
rollback [version]    # 版本回滾
```

## 🎨 UI界面說明

安裝完成後，您會在Cursor中看到：

1. **智能提示**：根據您的角色和專案階段提供相關建議
2. **TODO面板**：顯示當前待辦事項和進度
3. **品質儀表板**：實時顯示代碼品質指標
4. **快速動作**：常用指令的快捷按鈕

## 🆘 故障排除

### 配置沒有生效
1. 確認Cursor版本 ≥ 0.40
2. 重新啟動Cursor
3. 檢查配置格式是否正確

### 時間獲取失敗
```bash
# 手動設置時間格式
export CURSOR_TIME_FORMAT="Asia/Taipei"
```

### TODO文件無法創建
```bash
# 手動創建必要目錄
mkdir -p docs
touch docs/TODO.md docs/PROGRESS.md docs/BACKLOG.md
```

### 權限問題
```bash
# 確保有足夠權限
chmod +x cursor-init
```

## 📚 進階設置

### 團隊協作設置
如果您在團隊中工作，建議額外配置：

1. **共享配置**：將基本配置存放在專案根目錄的`.cursor/`資料夾
2. **角色矩陣**：定義團隊成員的角色分工
3. **品質標準**：統一團隊的品質門檻設定

### 多專案管理
如果您管理多個專案：

1. **專案模板**：為不同類型的專案建立模板
2. **環境變數**：使用環境變數管理不同專案的設定
3. **工作區設定**：利用Cursor的工作區功能切換專案配置

## 🎉 恭喜！

您已成功設置Cursor User Rules 2025！現在您可以：

- ✅ 享受智能化的開發體驗
- ✅ 獲得針對您角色的專業指導
- ✅ 自動化的品質控制和部署
- ✅ 漸進式的技能提升建議

開始您的高效開發旅程吧！🚀