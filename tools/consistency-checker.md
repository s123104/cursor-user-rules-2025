# 專案一致性檢查工具

**版本**: 2025.6.2  
**最後更新**: 2025-06-16T11:22:50+08:00  
**維護者**: Cursor User Rules 2025 Team

---

## 📋 目錄

- [工具概述](#-工具概述)
- [檢查項目](#-檢查項目)
- [使用方法](#-使用方法)
- [自動化腳本](#-自動化腳本)
- [CI/CD 整合](#-cicd-整合)
- [修復建議](#-修復建議)
- [配置選項](#-配置選項)

---

## 🔍 工具概述

專案一致性檢查工具用於確保 Cursor User Rules 2025 專案中所有文檔、配置文件和代碼的一致性。這包括版本號、連結、格式、命名規範等各個方面。

### 🎯 檢查目標

- **版本一致性**: 確保所有文檔使用相同的版本號
- **連結完整性**: 驗證所有內部和外部連結的有效性
- **格式一致性**: 檢查文檔格式、代碼風格的統一性
- **內容一致性**: 確保相關文檔間的資訊同步

---

## ✅ 檢查項目

### 1. 版本一致性檢查

```yaml
version_consistency:
  target_version: "2025.6.2"
  check_files:
    - README.md
    - CHANGELOG.md
    - cursor-user-rules-2025.md
    - docs/architecture.md
    - roles/*.md
    - templates/*.md
    - tools/*.md

  patterns:
    - "version.*2025\.6\.2"
    - "版本.*2025\.6\.2"
    - "v2025\.6\.2"
    - "2025-06-16T11:22:50\+08:00"
```

### 2. 文檔連結檢查

```yaml
link_validation:
  internal_links:
    - pattern: "\[.*\]\((?!http).*\.md\)"
    - pattern: "\[.*\]\(#.*\)"
    - pattern: "\[.*\]\(\.\.\/.*\)"

  external_links:
    - pattern: "\[.*\]\(https?:\/\/.*\)"
    - timeout: 5000ms
    - retry_count: 3

  anchor_links:
    - pattern: "#[a-z0-9-]+"
    - validate_existence: true
```

### 3. 格式一致性檢查

````yaml
format_consistency:
  markdown_style:
    - heading_style: "atx"  # # ## ### 格式
    - list_style: "dash"    # - 項目格式
    - code_fence: "```"     # 程式碼區塊格式
    - emphasis: "**bold**"  # 粗體格式

  yaml_frontmatter:
    - required_fields:
        - description
        - version
        - last_updated
    - date_format: "ISO8601"

  file_naming:
    - pattern: "^[a-z0-9-]+\.md$"
    - no_spaces: true
    - kebab_case: true
````

### 4. 內容一致性檢查

```yaml
content_consistency:
  role_configurations:
    - required_sections:
        - "技術棧配置"
        - "品質標準"
        - "效能指標"
        - "最佳實踐"
    - version_alignment: true

  template_completeness:
    - placeholder_check: "{{.*}}"
    - example_validation: true
    - instruction_clarity: true

  cross_references:
    - role_mentions: "roles/*.md"
    - tool_references: "tools/*.md"
    - doc_citations: "docs/*.md"
```

---

## 🚀 使用方法

### 命令列介面

```bash
# 執行完整檢查
./consistency-checker.sh --full

# 檢查特定類型
./consistency-checker.sh --check-versions
./consistency-checker.sh --check-links
./consistency-checker.sh --check-format

# 檢查特定文件
./consistency-checker.sh --file README.md
./consistency-checker.sh --directory roles/

# 自動修復（謹慎使用）
./consistency-checker.sh --fix --backup
```

### 配置文件

```yaml
# .consistency-config.yml
consistency_checker:
  version: "2025.6.2"
  base_directory: "."

  checks:
    version_consistency: true
    link_validation: true
    format_consistency: true
    content_consistency: true

  exclusions:
    - ".git/"
    - "node_modules/"
    - "*.tmp"
    - "*.backup"

  output:
    format: "json" # json, yaml, text
    file: "consistency-report.json"
    verbose: true
```

---

## 🤖 自動化腳本

### Bash 腳本版本

````bash
#!/bin/bash
# consistency-checker.sh

set -euo pipefail

# 配置變數
TARGET_VERSION="2025.6.2"
TARGET_DATE="2025-06-16T11:22:50+08:00"
BASE_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")/.." && pwd)"
REPORT_FILE="consistency-report.json"

# 顏色定義
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# 日誌函數
log_info() {
    echo -e "${BLUE}[INFO]${NC} $1"
}

log_success() {
    echo -e "${GREEN}[SUCCESS]${NC} $1"
}

log_warning() {
    echo -e "${YELLOW}[WARNING]${NC} $1"
}

log_error() {
    echo -e "${RED}[ERROR]${NC} $1"
}

# 檢查版本一致性
check_version_consistency() {
    log_info "檢查版本一致性..."

    local errors=0
    local files=(
        "README.md"
        "CHANGELOG.md"
        "cursor-user-rules-2025.md"
        "docs/architecture.md"
    )

    for file in "${files[@]}"; do
        if [[ -f "$BASE_DIR/$file" ]]; then
            if ! grep -q "$TARGET_VERSION" "$BASE_DIR/$file"; then
                log_error "版本不一致: $file 缺少版本 $TARGET_VERSION"
                ((errors++))
            else
                log_success "版本一致: $file"
            fi
        else
            log_warning "文件不存在: $file"
        fi
    done

    return $errors
}

# 檢查連結有效性
check_link_validity() {
    log_info "檢查連結有效性..."

    local errors=0

    # 檢查內部連結
    find "$BASE_DIR" -name "*.md" -type f | while read -r file; do
        # 提取內部連結
        grep -oP '\[.*?\]\(\K[^)]*(?=\))' "$file" 2>/dev/null | while read -r link; do
            if [[ "$link" =~ ^[^http] ]]; then
                # 內部連結檢查
                local target_file
                if [[ "$link" =~ ^\.\./ ]]; then
                    target_file="$(dirname "$file")/$link"
                elif [[ "$link" =~ ^\./ ]]; then
                    target_file="$(dirname "$file")/${link#./}"
                else
                    target_file="$(dirname "$file")/$link"
                fi

                if [[ ! -f "$target_file" ]]; then
                    log_error "無效連結: $file -> $link"
                    ((errors++))
                fi
            fi
        done
    done

    return $errors
}

# 檢查格式一致性
check_format_consistency() {
    log_info "檢查格式一致性..."

    local errors=0

    # 檢查 Markdown 格式
    find "$BASE_DIR" -name "*.md" -type f | while read -r file; do
        # 檢查標題格式（應使用 # 而非 ===）
        if grep -q "^===\|^---" "$file"; then
            log_warning "建議使用 ATX 標題格式: $file"
        fi

        # 檢查清單格式（應使用 - 而非 *）
        if grep -q "^\* " "$file"; then
            log_warning "建議使用 - 作為清單標記: $file"
        fi

        # 檢查程式碼區塊格式
        if grep -q "^    [a-zA-Z]" "$file"; then
            log_warning "建議使用 ``` 程式碼區塊: $file"
        fi
    done

    return $errors
}

# 檢查內容一致性
check_content_consistency() {
    log_info "檢查內容一致性..."

    local errors=0

    # 檢查角色配置完整性
    for role_file in "$BASE_DIR"/roles/*.md; do
        if [[ -f "$role_file" ]]; then
            local required_sections=(
                "技術棧配置"
                "品質標準"
                "效能指標"
            )

            for section in "${required_sections[@]}"; do
                if ! grep -q "$section" "$role_file"; then
                    log_error "缺少必要章節 '$section': $(basename "$role_file")"
                    ((errors++))
                fi
            done
        fi
    done

    return $errors
}

# 生成報告
generate_report() {
    local total_errors=$1

    cat > "$BASE_DIR/$REPORT_FILE" << EOF
{
  "timestamp": "$(date -Iseconds)",
  "version": "$TARGET_VERSION",
  "total_errors": $total_errors,
  "checks": {
    "version_consistency": $(check_version_consistency; echo $?),
    "link_validity": $(check_link_validity; echo $?),
    "format_consistency": $(check_format_consistency; echo $?),
    "content_consistency": $(check_content_consistency; echo $?)
  },
  "status": "$([ $total_errors -eq 0 ] && echo "PASS" || echo "FAIL")"
}
EOF

    log_info "報告已生成: $REPORT_FILE"
}

# 主函數
main() {
    log_info "開始專案一致性檢查..."
    log_info "目標版本: $TARGET_VERSION"
    log_info "基礎目錄: $BASE_DIR"

    local total_errors=0

    # 執行各項檢查
    check_version_consistency || ((total_errors += $?))
    check_link_validity || ((total_errors += $?))
    check_format_consistency || ((total_errors += $?))
    check_content_consistency || ((total_errors += $?))

    # 生成報告
    generate_report $total_errors

    # 輸出結果
    if [[ $total_errors -eq 0 ]]; then
        log_success "所有檢查通過！專案一致性良好。"
        exit 0
    else
        log_error "發現 $total_errors 個問題，請檢查並修復。"
        exit 1
    fi
}

# 執行主函數
main "$@"
````

### Node.js 腳本版本

```javascript
#!/usr/bin/env node
// consistency-checker.js

const fs = require("fs").promises;
const path = require("path");
const { execSync } = require("child_process");

class ConsistencyChecker {
  constructor(config = {}) {
    this.config = {
      targetVersion: "2025.6.2",
      targetDate: "2025-06-16T11:22:50+08:00",
      baseDir: process.cwd(),
      reportFile: "consistency-report.json",
      ...config,
    };

    this.errors = [];
    this.warnings = [];
  }

  log(level, message) {
    const colors = {
      info: "\x1b[34m",
      success: "\x1b[32m",
      warning: "\x1b[33m",
      error: "\x1b[31m",
      reset: "\x1b[0m",
    };

    console.log(
      `${colors[level]}[${level.toUpperCase()}]${colors.reset} ${message}`
    );
  }

  async checkVersionConsistency() {
    this.log("info", "檢查版本一致性...");

    const files = [
      "README.md",
      "CHANGELOG.md",
      "cursor-user-rules-2025.md",
      "docs/architecture.md",
    ];

    for (const file of files) {
      const filePath = path.join(this.config.baseDir, file);

      try {
        const content = await fs.readFile(filePath, "utf8");

        if (!content.includes(this.config.targetVersion)) {
          this.errors.push(
            `版本不一致: ${file} 缺少版本 ${this.config.targetVersion}`
          );
        } else {
          this.log("success", `版本一致: ${file}`);
        }
      } catch (error) {
        this.warnings.push(`文件不存在: ${file}`);
      }
    }
  }

  async checkLinkValidity() {
    this.log("info", "檢查連結有效性...");

    const markdownFiles = await this.findMarkdownFiles();

    for (const file of markdownFiles) {
      const content = await fs.readFile(file, "utf8");
      const links = this.extractLinks(content);

      for (const link of links) {
        if (this.isInternalLink(link)) {
          const targetPath = this.resolveInternalLink(file, link);

          try {
            await fs.access(targetPath);
            this.log("success", `有效連結: ${link}`);
          } catch {
            this.errors.push(
              `無效連結: ${path.relative(this.config.baseDir, file)} -> ${link}`
            );
          }
        }
      }
    }
  }

  async findMarkdownFiles() {
    const files = [];

    async function walk(dir) {
      const entries = await fs.readdir(dir, { withFileTypes: true });

      for (const entry of entries) {
        const fullPath = path.join(dir, entry.name);

        if (entry.isDirectory() && !entry.name.startsWith(".")) {
          await walk(fullPath);
        } else if (entry.isFile() && entry.name.endsWith(".md")) {
          files.push(fullPath);
        }
      }
    }

    await walk(this.config.baseDir);
    return files;
  }

  extractLinks(content) {
    const linkRegex = /\[.*?\]\(([^)]+)\)/g;
    const links = [];
    let match;

    while ((match = linkRegex.exec(content)) !== null) {
      links.push(match[1]);
    }

    return links;
  }

  isInternalLink(link) {
    return !link.startsWith("http") && !link.startsWith("mailto:");
  }

  resolveInternalLink(fromFile, link) {
    const fromDir = path.dirname(fromFile);

    if (link.startsWith("../")) {
      return path.resolve(fromDir, link);
    } else if (link.startsWith("./")) {
      return path.resolve(fromDir, link.substring(2));
    } else if (link.startsWith("#")) {
      return fromFile; // 錨點連結，指向同一文件
    } else {
      return path.resolve(fromDir, link);
    }
  }

  async checkFormatConsistency() {
    this.log("info", "檢查格式一致性...");

    const markdownFiles = await this.findMarkdownFiles();

    for (const file of markdownFiles) {
      const content = await fs.readFile(file, "utf8");
      const relativePath = path.relative(this.config.baseDir, file);

      // 檢查標題格式
      if (content.includes("===") || content.includes("---")) {
        this.warnings.push(`建議使用 ATX 標題格式: ${relativePath}`);
      }

      // 檢查清單格式
      if (/^\* /m.test(content)) {
        this.warnings.push(`建議使用 - 作為清單標記: ${relativePath}`);
      }

      // 檢查程式碼區塊格式
      if (/^    [a-zA-Z]/m.test(content)) {
        this.warnings.push(`建議使用 \`\`\` 程式碼區塊: ${relativePath}`);
      }
    }
  }

  async generateReport() {
    const report = {
      timestamp: new Date().toISOString(),
      version: this.config.targetVersion,
      totalErrors: this.errors.length,
      totalWarnings: this.warnings.length,
      errors: this.errors,
      warnings: this.warnings,
      status: this.errors.length === 0 ? "PASS" : "FAIL",
    };

    const reportPath = path.join(this.config.baseDir, this.config.reportFile);
    await fs.writeFile(reportPath, JSON.stringify(report, null, 2));

    this.log("info", `報告已生成: ${this.config.reportFile}`);
    return report;
  }

  async run() {
    this.log("info", "開始專案一致性檢查...");
    this.log("info", `目標版本: ${this.config.targetVersion}`);
    this.log("info", `基礎目錄: ${this.config.baseDir}`);

    await this.checkVersionConsistency();
    await this.checkLinkValidity();
    await this.checkFormatConsistency();

    const report = await this.generateReport();

    if (report.status === "PASS") {
      this.log("success", "所有檢查通過！專案一致性良好。");
      process.exit(0);
    } else {
      this.log(
        "error",
        `發現 ${report.totalErrors} 個錯誤，${report.totalWarnings} 個警告。`
      );
      process.exit(1);
    }
  }
}

// 如果直接執行此腳本
if (require.main === module) {
  const checker = new ConsistencyChecker();
  checker.run().catch(console.error);
}

module.exports = ConsistencyChecker;
```

---

## 🔄 CI/CD 整合

### GitHub Actions 工作流程

```yaml
# .github/workflows/consistency-check.yml
name: 專案一致性檢查

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  consistency-check:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout 程式碼
        uses: actions/checkout@v4

      - name: 設置 Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "18"

      - name: 執行一致性檢查
        run: |
          chmod +x tools/consistency-checker.sh
          ./tools/consistency-checker.sh --full

      - name: 上傳檢查報告
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: consistency-report
          path: consistency-report.json

      - name: 評論 PR（如果有錯誤）
        if: failure() && github.event_name == 'pull_request'
        uses: actions/github-script@v7
        with:
          script: |
            const fs = require('fs');
            const report = JSON.parse(fs.readFileSync('consistency-report.json', 'utf8'));

            const comment = `## 🔍 專案一致性檢查結果

            **狀態**: ${report.status === 'PASS' ? '✅ 通過' : '❌ 失敗'}
            **錯誤數量**: ${report.totalErrors}
            **警告數量**: ${report.totalWarnings}

            ${report.errors.length > 0 ? '### 錯誤\n' + report.errors.map(e => `- ${e}`).join('\n') : ''}
            ${report.warnings.length > 0 ? '### 警告\n' + report.warnings.map(w => `- ${w}`).join('\n') : ''}
            `;

            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: comment
            });
```

---

## 🛠️ 修復建議

### 自動修復功能

```bash
# 自動修復版本號
fix_version_numbers() {
    local target_version="2025.6.2"
    local target_date="2025-06-16T11:22:50+08:00"

    find . -name "*.md" -type f | while read -r file; do
        # 備份原文件
        cp "$file" "$file.backup"

        # 修復版本號
        sed -i "s/version.*[0-9]\+\.[0-9]\+\.[0-9]\+/version: $target_version/g" "$file"
        sed -i "s/版本.*[0-9]\+\.[0-9]\+\.[0-9]\+/版本: $target_version/g" "$file"

        # 修復日期
        sed -i "s/[0-9]\{4\}-[0-9]\{2\}-[0-9]\{2\}T[0-9]\{2\}:[0-9]\{2\}:[0-9]\{2\}+[0-9]\{2\}:[0-9]\{2\}/$target_date/g" "$file"

        echo "已修復: $file"
    done
}

# 修復連結格式
fix_link_format() {
    find . -name "*.md" -type f | while read -r file; do
        # 修復相對路徑連結
        sed -i 's|\[([^]]*)\](\([^)]*\)\.md)|\[\1\](\1.md)|g' "$file"

        # 修復錨點連結格式
        sed -i 's|#\([A-Z]\)|#\L\1|g' "$file"

        echo "已修復連結: $file"
    done
}
```

### 手動修復指南

````markdown
## 常見問題修復指南

### 1. 版本號不一致

- 檢查所有 .md 文件中的版本號
- 統一更新為目標版本 2025.6.2
- 確保日期格式為 ISO8601

### 2. 連結失效

- 檢查相對路徑是否正確
- 確認目標文件是否存在
- 修正錨點連結的大小寫

### 3. 格式不一致

- 使用 # ## ### 標題格式
- 使用 - 作為清單標記
- 使用 ``` 程式碼區塊

### 4. 內容缺失

- 確保角色配置包含必要章節
- 檢查模板的完整性
- 驗證交叉引用的準確性
````

---

## ⚙️ 配置選項

### 完整配置範例

```yaml
# .consistency-config.yml
consistency_checker:
  # 基本設定
  version: "2025.6.2"
  date: "2025-06-16T11:22:50+08:00"
  base_directory: "."

  # 檢查選項
  checks:
    version_consistency:
      enabled: true
      strict_mode: true
      auto_fix: false

    link_validation:
      enabled: true
      check_external: false
      timeout: 5000
      retry_count: 3

    format_consistency:
      enabled: true
      enforce_style: true
      auto_format: false

    content_consistency:
      enabled: true
      require_sections: true
      validate_examples: true

  # 文件過濾
  include_patterns:
    - "*.md"
    - "*.yml"
    - "*.yaml"

  exclude_patterns:
    - ".git/**"
    - "node_modules/**"
    - "*.tmp"
    - "*.backup"

  # 輸出設定
  output:
    format: "json" # json, yaml, text, html
    file: "consistency-report.json"
    verbose: true
    colors: true

  # 修復選項
  auto_fix:
    enabled: false
    backup: true
    confirm: true

  # 通知設定
  notifications:
    slack_webhook: ""
    email: ""
    github_comment: true
```

---

## 📊 報告格式

### JSON 報告範例

```json
{
  "timestamp": "2025-06-16T11:22:50+08:00",
  "version": "2025.6.2",
  "summary": {
    "total_files_checked": 25,
    "total_errors": 0,
    "total_warnings": 2,
    "status": "PASS"
  },
  "checks": {
    "version_consistency": {
      "status": "PASS",
      "errors": 0,
      "details": []
    },
    "link_validation": {
      "status": "PASS",
      "errors": 0,
      "checked_links": 45,
      "details": []
    },
    "format_consistency": {
      "status": "WARNING",
      "warnings": 2,
      "details": [
        {
          "file": "roles/frontend-engineer.md",
          "issue": "建議使用 - 作為清單標記",
          "line": 25
        }
      ]
    },
    "content_consistency": {
      "status": "PASS",
      "errors": 0,
      "details": []
    }
  },
  "recommendations": [
    "考慮設置 pre-commit hook 自動執行一致性檢查",
    "建議在 CI/CD 流程中加入自動修復功能"
  ]
}
```

---

## 🔧 定期維護

### 維護清單

```yaml
maintenance_schedule:
  daily:
    - 執行基本一致性檢查
    - 檢查新增文件的格式

  weekly:
    - 完整連結驗證
    - 內容一致性深度檢查
    - 更新檢查規則

  monthly:
    - 檢查工具本身的更新
    - 評估新的檢查項目
    - 優化檢查效能

  quarterly:
    - 全面檢查規則有效性
    - 更新最佳實踐標準
    - 檢討自動化流程
```

### 效能優化

```bash
# 並行檢查以提升效能
parallel_check() {
    local max_jobs=4

    find . -name "*.md" -type f | \
    xargs -n 1 -P $max_jobs -I {} \
    bash -c 'check_single_file "$@"' _ {}
}

# 增量檢查（只檢查變更的文件）
incremental_check() {
    local changed_files
    changed_files=$(git diff --name-only HEAD~1 HEAD | grep '\.md$')

    for file in $changed_files; do
        check_single_file "$file"
    done
}
```

---

<div align="center">

**專案一致性檢查工具** | **版本 2025.6.2** | **Cursor User Rules 2025**

[返回工具目錄](../tools/) • [查看專案檢查工具](project-checker.md) • [返回主文檔](../README.md)

</div>
