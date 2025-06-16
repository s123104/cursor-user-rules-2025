# MCP 安裝與使用指引

> **版本**: 2025.6.2  
> **最後更新**: 2025-06-16T11:22:50+08:00  
> **適用範圍**: Cursor IDE + MCP Interactive Feedback + Context7

本指引將協助您完整設置 MCP (Model Context Protocol) 環境，包含 `mcp-feedback-enhanced` 和 `context7` 兩個核心組件。

---

## 📋 目錄

- [系統需求](#-系統需求)
- [MCP Feedback Enhanced 安裝](#-mcp-feedback-enhanced-安裝)
- [Context7 安裝](#-context7-安裝)
- [Cursor IDE 配置](#-cursor-ide-配置)
- [快速驗證](#-快速驗證)
- [進階配置](#-進階配置)
- [疑難排解](#-疑難排解)

---

## 🔧 系統需求

### 基礎環境

- **Cursor IDE**: v0.40+
- **Node.js**: 18+ (推薦 20+)
- **Python**: 3.8+ (推薦 3.11+)
- **uv**: Python 套件管理器 (推薦)
- **作業系統**: Windows 10+, macOS 12+, Linux (Ubuntu 20.04+)

### 檢查現有環境

```bash
# 檢查 Node.js 版本
node --version

# 檢查 Python 版本
python --version

# 檢查 uv 是否已安裝
uv --version

# 如果 uv 未安裝，請執行：
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

## 🔄 MCP Feedback Enhanced 安裝

### 1. 快速安裝

```bash
# 使用 uvx 安裝最新版本
uvx mcp-feedback-enhanced@latest

# 或指定版本安裝
uvx mcp-feedback-enhanced@2.5.4
```

### 2. 功能測試

```bash
# 檢查版本
uvx mcp-feedback-enhanced@latest version

# 測試 Web UI 介面
uvx mcp-feedback-enhanced@latest test --web

# 測試桌面應用程式 (v2.5.0+)
uvx mcp-feedback-enhanced@latest test --desktop

# 啟用除錯模式測試
MCP_DEBUG=true uvx mcp-feedback-enhanced@latest test
```

### 3. 環境變數配置

```bash
# 設置環境變數 (可選)
export MCP_DEBUG=false                    # 除錯模式 (生產環境建議關閉)
export MCP_WEB_PORT=8765                  # Web UI 埠號
export MCP_DESKTOP_MODE=false             # 桌面應用程式模式
```

### 4. 進階安裝 (開發者)

```bash
# 從原始碼安裝
git clone https://github.com/Minidoracat/mcp-feedback-enhanced.git
cd mcp-feedback-enhanced
uv sync

# 本地測試
make test-func                            # 功能測試
make test-web                             # Web UI 測試
make test-desktop-func                    # 桌面應用程式測試

# 建置桌面應用程式
make build-desktop                        # 除錯版本
make build-desktop-release                # 發布版本
```

---

## 📚 Context7 安裝

### 1. 簡化安裝流程

**Context7 已更新為更簡單的配置方式，無需額外註冊或設置！**

Context7 MCP 伺服器會在 Cursor IDE 配置時自動安裝，無需手動安裝或註冊 Upstash 帳戶。

### 2. 配置說明

Context7 使用以下簡化配置：

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"],
      "timeout": 300
    }
  }
}
```

**配置說明**：

- `npx -y @upstash/context7-mcp`: 自動安裝並執行 Context7 MCP 伺服器
- 無需環境變數或額外的認證設定
- 首次執行會自動下載所需組件

### 3. 功能測試

在 Cursor IDE 中測試 Context7 功能：

```
請使用 Context7 獲取 React 的最新文檔
```

**預期結果**：Context7 會自動解析並提供 React 的最新技術文檔。

---

## ⚙️ Cursor IDE 配置

### 1. 基礎 MCP 配置

在 Cursor IDE 中配置 MCP 伺服器：

1. **開啟設置**

   - `Ctrl/Cmd + ,` → 搜尋 "MCP"
   - 或直接編輯 `~/.cursor/mcp_servers.json`

2. **添加 MCP 伺服器配置**

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced": {
      "command": "uvx",
      "args": ["mcp-feedback-enhanced@latest"],
      "timeout": 600,
      "env": {
        "MCP_DEBUG": "false",
        "MCP_WEB_PORT": "8765",
        "MCP_DESKTOP_MODE": "false"
      },
      "autoApprove": ["interactive_feedback"]
    },
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"],
      "timeout": 300
    }
  }
}
```

### 2. 桌面應用程式模式配置

如果您偏好使用桌面應用程式介面：

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced": {
      "command": "uvx",
      "args": ["mcp-feedback-enhanced@latest"],
      "timeout": 600,
      "env": {
        "MCP_DESKTOP_MODE": "true",
        "MCP_WEB_PORT": "8765"
      },
      "autoApprove": ["interactive_feedback"]
    }
  }
}
```

### 3. 開發環境配置

針對開發者的進階配置：

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced-dev": {
      "command": "uv",
      "args": ["run", "python", "-m", "mcp_feedback_enhanced"],
      "cwd": "/path/to/mcp-feedback-enhanced",
      "timeout": 600,
      "env": {
        "MCP_DEBUG": "true",
        "MCP_WEB_PORT": "8765"
      },
      "autoApprove": ["interactive_feedback", "get_system_info"]
    }
  }
}
```

---

## ✅ 快速驗證

### 1. 驗證 MCP Feedback Enhanced

1. **重新啟動 Cursor IDE**
2. **開啟任意專案**
3. **在聊天中輸入**：
   ```
   請使用 MCP Interactive Feedback 測試連接
   ```
4. **預期結果**：應該會彈出互動回饋視窗

### 2. 驗證 Context7

1. **在聊天中輸入**：
   ```
   請使用 Context7 獲取 React 的最新文檔
   ```
2. **預期結果**：應該會顯示 React 的最新文檔資訊

### 3. 整合測試

```
請初始化一個新的 React 專案，並使用 MCP Interactive Feedback 收集我的回饋，同時使用 Context7 獲取最新的 React 最佳實踐。
```

---

## 🔧 進階配置

### 1. 自訂埠號與網路設定

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced": {
      "env": {
        "MCP_WEB_PORT": "9000",
        "MCP_HOST": "0.0.0.0"
      }
    }
  }
}
```

### 2. 效能優化設定

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced": {
      "timeout": 300,
      "env": {
        "MCP_CACHE_SIZE": "1000",
        "MCP_SESSION_TIMEOUT": "3600"
      }
    }
  }
}
```

### 3. 安全性設定

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"],
      "timeout": 300,
      "env": {
        "CONTEXT7_RATE_LIMIT": "100"
      }
    }
  }
}
```

### 4. 多環境配置

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced-prod": {
      "command": "uvx",
      "args": ["mcp-feedback-enhanced@latest"],
      "env": {
        "NODE_ENV": "production",
        "MCP_DEBUG": "false"
      }
    },
    "mcp-feedback-enhanced-dev": {
      "command": "uvx",
      "args": ["mcp-feedback-enhanced@latest"],
      "env": {
        "NODE_ENV": "development",
        "MCP_DEBUG": "true"
      }
    }
  }
}
```

---

## 🔍 疑難排解

### 常見問題與解決方案

#### 1. MCP Feedback Enhanced 無法啟動

**問題**: `uvx mcp-feedback-enhanced@latest` 失敗

**解決方案**:

```bash
# 清除 uv 快取
uv cache clean

# 重新安裝
uvx --force mcp-feedback-enhanced@latest

# 檢查 Python 環境
python --version
uv --version
```

#### 2. Web UI 無法開啟

**問題**: 瀏覽器無法連接到 `http://localhost:8765`

**解決方案**:

```bash
# 檢查埠號是否被佔用
netstat -an | grep 8765

# 嘗試不同埠號
MCP_WEB_PORT=9000 uvx mcp-feedback-enhanced@latest test --web

# 檢查防火牆設定
```

#### 3. Context7 連接失敗

**問題**: Context7 MCP 伺服器無法正常運作

**解決方案**:

```bash
# 清除 npm 快取
npm cache clean --force

# 手動測試安裝
npx -y @upstash/context7-mcp

# 檢查網路連接
ping github.com
```

#### 4. Cursor IDE 無法識別 MCP 伺服器

**問題**: MCP 伺服器在 Cursor IDE 中顯示為離線

**解決方案**:

1. **檢查配置檔案格式**

   ```bash
   # 驗證 JSON 格式
   cat ~/.cursor/mcp_servers.json | python -m json.tool
   ```

2. **重新啟動 Cursor IDE**

   ```bash
   # 完全關閉 Cursor IDE
   # 重新開啟
   ```

3. **檢查日誌**
   ```bash
   # 查看 Cursor IDE 日誌
   # Windows: %APPDATA%\Cursor\logs
   # macOS: ~/Library/Logs/Cursor
   # Linux: ~/.config/Cursor/logs
   ```

#### 5. SSH Remote 環境問題

**問題**: 在 SSH Remote 環境中無法開啟瀏覽器

**解決方案**:

```bash
# 使用埠轉發
ssh -L 8765:localhost:8765 user@remote-server

# 在本地瀏覽器開啟
open http://localhost:8765
```

#### 6. 快取問題

**問題**: 更新後功能異常

**解決方案**:

```bash
# 清除所有快取
uv cache clean
npm cache clean --force

# 重新安裝
uvx --force mcp-feedback-enhanced@latest
npm install -g @upstash/context7 --force
```

### 效能調優

#### 1. 記憶體使用優化

```json
{
  "mcpServers": {
    "mcp-feedback-enhanced": {
      "env": {
        "NODE_OPTIONS": "--max-old-space-size=2048",
        "MCP_MEMORY_LIMIT": "1GB"
      }
    }
  }
}
```

#### 2. 網路超時設定

```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"],
      "timeout": 600,
      "env": {
        "CONTEXT7_TIMEOUT": "30000",
        "CONTEXT7_RETRY_COUNT": "3"
      }
    }
  }
}
```

### 除錯模式

#### 1. 啟用詳細日誌

```bash
# MCP Feedback Enhanced 除錯
MCP_DEBUG=true uvx mcp-feedback-enhanced@latest

# Context7 除錯
DEBUG=context7:* npx -y @upstash/context7-mcp
```

#### 2. 日誌分析

```bash
# 查看 MCP 日誌
tail -f ~/.cursor/logs/mcp-feedback-enhanced.log

# 查看系統資訊
uvx mcp-feedback-enhanced@latest get_system_info
```

---

## 📚 參考資源

### 官方文檔

- **MCP Feedback Enhanced**: [GitHub Repository](https://github.com/Minidoracat/mcp-feedback-enhanced)
- **Context7**: [GitHub Repository](https://github.com/upstash/context7)
- **Cursor IDE**: [https://cursor.sh/](https://cursor.sh/)

### 社群支援

- **Discord**: [MCP Community](https://discord.gg/Gur2V67)
- **GitHub Issues**:
  - [MCP Feedback Enhanced Issues](https://github.com/Minidoracat/mcp-feedback-enhanced/issues)
  - [Context7 Issues](https://github.com/upstash/context7/issues)

### 疑難排解與支援

如遇到任何安裝或配置問題，請依序查看：

1. **本文檔的疑難排解章節** - 包含最常見問題的解決方案
2. **[MCP Feedback Enhanced GitHub](https://github.com/Minidoracat/mcp-feedback-enhanced)** - 互動回饋機制相關問題
3. **[Context7 GitHub](https://github.com/upstash/context7)** - 技術文檔獲取相關問題
4. **社群討論區** - Discord 或 GitHub Discussions

### 相關工具

- **uv**: [Python 套件管理器](https://github.com/astral-sh/uv)
- **Model Context Protocol**: [官方規範](https://modelcontextprotocol.io/)

---

## 🔄 版本更新

### 更新 MCP Feedback Enhanced

```bash
# 檢查最新版本
uvx mcp-feedback-enhanced@latest version

# 強制更新到最新版本
uvx --force mcp-feedback-enhanced@latest

# 更新到特定版本
uvx --force mcp-feedback-enhanced@2.5.4
```

### 更新 Context7

```bash
# Context7 MCP 伺服器會自動使用最新版本
# 如需強制更新，可清除 npm 快取

# 清除快取
npm cache clean --force

# 重新執行會自動下載最新版本
npx -y @upstash/context7-mcp
```

---

## 📝 最佳實踐

### 1. 開發環境建議

- 使用 `MCP_DEBUG=true` 進行開發
- 定期清除快取避免問題累積
- 使用版本鎖定避免意外更新

### 2. 生產環境建議

- 設定 `MCP_DEBUG=false` 提升效能
- 配置適當的超時時間
- 監控記憶體和 CPU 使用率

### 3. 安全性建議

- 定期更新所有組件到最新版本
- 使用環境變數管理敏感資訊
- 限制網路存取權限

---

**🎯 完成設置後，您就可以開始使用 Cursor User Rules 2025 的完整功能了！**

如有任何問題，請參考 [疑難排解](#-疑難排解) 章節或聯繫社群支援。
