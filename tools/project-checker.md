# 專案最佳實踐檢查工具

## 🔍 專案健康度檢查清單

### 使用方式
```bash
# 執行完整專案檢查
cursor-check --full

# 執行特定類型檢查
cursor-check --type=frontend
cursor-check --type=backend
cursor-check --type=fullstack

# 執行特定階段檢查
cursor-check --stage=mvp
cursor-check --stage=enterprise

# 生成檢查報告
cursor-check --report=html
cursor-check --report=json
```

---

## § 1 通用專案檢查項目

### 1.1 專案結構檢查

```yaml
PROJECT_STRUCTURE_CHECK:
  required_files:
    - path: "README.md"
      description: "專案說明文檔"
      critical: true
      
    - path: "package.json"
      description: "Node.js專案配置"
      condition: "if nodejs project"
      
    - path: ".gitignore"
      description: "Git忽略檔案"
      critical: true
      
    - path: "docs/TODO.md"
      description: "TODO清單"
      critical: true
      
  recommended_files:
    - path: "CHANGELOG.md"
      description: "變更記錄"
      stage: "standard+"
      
    - path: "CONTRIBUTING.md"
      description: "貢獻指南"
      stage: "comprehensive+"
      
    - path: "LICENSE"
      description: "授權條款"
      stage: "standard+"
      
  directory_structure:
    - path: "src/"
      description: "原始碼目錄"
      
    - path: "tests/"
      description: "測試檔案目錄"
      alternative: ["__tests__", "test"]
      
    - path: "docs/"
      description: "文檔目錄"
      
    - path: ".github/workflows/"
      description: "GitHub Actions"
      condition: "if using github"
```

### 1.2 Git提交品質檢查

```yaml
GIT_COMMIT_QUALITY:
  commit_message_format:
    pattern: "^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}"
    description: "使用Conventional Commits格式"
    
  branch_naming:
    patterns:
      - "feature/.*"
      - "bugfix/.*"
      - "hotfix/.*"
      - "release/.*"
    description: "使用標準分支命名"
    
  commit_frequency:
    max_files_per_commit: 20
    max_lines_per_commit: 500
    description: "避免過大的提交"
```

### 1.3 文檔完整性檢查

```yaml
DOCUMENTATION_CHECK:
  readme_sections:
    required:
      - "專案描述"
      - "安裝說明"
      - "使用方式"
      - "貢獻指南"
      
    recommended:
      - "API文檔"
      - "架構說明"
      - "部署指南"
      - "故障排除"
      
  todo_management:
    required_files:
      - "docs/TODO.md"
      - "docs/PROGRESS.md"
      
    content_check:
      - "至少一個活躍TODO項目"
      - "清楚的優先級標記"
      - "明確的完成期限"
      - "負責人指定"
```

---

## § 2 前端專案檢查

### 2.1 前端技術棧檢查

```yaml
FRONTEND_TECH_CHECK:
  package_json_dependencies:
    required_dev_dependencies:
      - name: "eslint"
        description: "代碼品質檢查"
        
      - name: "prettier"
        description: "代碼格式化"
        
      - name: "@typescript-eslint/parser"
        description: "TypeScript ESLint支援"
        condition: "if typescript"
        
    modern_dependencies:
      - name: "vite"
        description: "現代建置工具"
        alternatives: ["webpack", "rollup"]
        
      - name: "vitest"
        description: "現代測試框架"
        alternatives: ["jest", "@jest/core"]
        
  configuration_files:
    - name: "tsconfig.json"
      description: "TypeScript配置"
      condition: "if typescript"
      
    - name: "vite.config.ts"
      description: "Vite配置"
      condition: "if vite"
      
    - name: ".eslintrc.js"
      description: "ESLint配置"
      alternatives: [".eslintrc.json", "eslint.config.js"]
```

### 2.2 前端品質檢查

```yaml
FRONTEND_QUALITY_CHECK:
  performance_budget:
    bundle_size:
      max_initial_js: "150KB"
      max_initial_css: "50KB"
      max_total_size: "500KB"
      
    lighthouse_scores:
      performance: 90
      accessibility: 95
      best_practices: 90
      seo: 85
      
  code_quality:
    typescript_strict: true
    eslint_errors: 0
    eslint_warnings_max: 5
    
  testing:
    unit_test_coverage: 80
    component_test_coverage: 85
    e2e_test_exists: true
```

---

## § 3 後端專案檢查

### 3.1 後端技術棧檢查

```yaml
BACKEND_TECH_CHECK:
  api_documentation:
    - name: "OpenAPI/Swagger規格"
      files: ["openapi.json", "swagger.yaml", "api-docs.yaml"]
      
    - name: "API文檔"
      files: ["docs/api.md", "API.md"]
      
  security_configuration:
    - name: "環境變數範例"
      files: [".env.example", ".env.template"]
      
    - name: "安全性header設定"
      check: "helmet middleware configured"
      
    - name: "速率限制設定"
      check: "rate limiting configured"
      
  database_management:
    - name: "資料庫遷移檔案"
      directories: ["migrations/", "db/migrations/"]
      
    - name: "種子資料"
      directories: ["seeds/", "db/seeds/"]
```

### 3.2 後端品質檢查

```yaml
BACKEND_QUALITY_CHECK:
  performance_metrics:
    api_response_time_p95: "200ms"
    database_query_time_p95: "100ms"
    concurrent_requests: "1000 RPS"
    
  security_checks:
    dependency_vulnerabilities: 0
    secrets_in_code: false
    https_enforced: true
    cors_configured: true
    
  monitoring:
    health_check_endpoint: true
    logging_configured: true
    error_tracking: true
    metrics_collection: true
```

---

## § 4 DevOps和部署檢查

### 4.1 CI/CD管道檢查

```yaml
CICD_PIPELINE_CHECK:
  github_actions:
    required_workflows:
      - name: "測試工作流程"
        file: ".github/workflows/test.yml"
        
      - name: "建置工作流程"
        file: ".github/workflows/build.yml"
        
    workflow_stages:
      - "代碼品質檢查"
      - "安全性掃描"
      - "測試執行"
      - "建置驗證"
      
  deployment_configuration:
    - name: "Dockerfile"
      description: "容器化配置"
      
    - name: "docker-compose.yml"
      description: "本地開發環境"
      
    - name: "k8s manifests"
      directory: "k8s/"
      stage: "enterprise"
```

### 4.2 安全性檢查

```yaml
SECURITY_CHECK:
  dependency_scanning:
    tools: ["npm audit", "snyk", "dependabot"]
    critical_vulnerabilities: 0
    high_vulnerabilities: 0
    
  code_scanning:
    sast_tools: ["eslint-security", "semgrep", "codeql"]
    secrets_detection: ["git-secrets", "trufflehog"]
    
  container_security:
    base_image_scanning: true
    non_root_user: true
    minimal_dependencies: true
```

---

## § 5 檢查報告生成

### 5.1 HTML報告模板

```html
<!DOCTYPE html>
<html>
<head>
    <title>專案健康度檢查報告</title>
    <style>
        .pass { color: green; }
        .fail { color: red; }
        .warning { color: orange; }
        .info { color: blue; }
    </style>
</head>
<body>
    <h1>專案健康度檢查報告</h1>
    
    <section>
        <h2>專案概要</h2>
        <ul>
            <li><strong>專案名稱</strong>: {{project_name}}</li>
            <li><strong>檢查時間</strong>: {{check_time}}</li>
            <li><strong>專案類型</strong>: {{project_type}}</li>
            <li><strong>當前階段</strong>: {{current_stage}}</li>
        </ul>
    </section>
    
    <section>
        <h2>整體評分</h2>
        <div class="score-circle">
            <span class="score">{{overall_score}}/100</span>
        </div>
    </section>
    
    <section>
        <h2>檢查結果</h2>
        {{#each categories}}
        <h3>{{name}} ({{score}}/{{max_score}})</h3>
        <ul>
            {{#each checks}}
            <li class="{{status}}">
                {{description}} - {{status_text}}
            </li>
            {{/each}}
        </ul>
        {{/each}}
    </section>
    
    <section>
        <h2>改善建議</h2>
        <ol>
            {{#each recommendations}}
            <li class="{{priority}}">
                <strong>{{title}}</strong>: {{description}}
            </li>
            {{/each}}
        </ol>
    </section>
</body>
</html>
```

### 5.2 JSON報告格式

```json
{
  "project_info": {
    "name": "{{project_name}}",
    "type": "{{project_type}}",
    "stage": "{{current_stage}}",
    "check_time": "{{iso_timestamp}}"
  },
  "overall_score": {
    "total": 85,
    "max": 100,
    "grade": "B+"
  },
  "categories": [
    {
      "name": "專案結構",
      "score": 90,
      "max_score": 100,
      "checks": [
        {
          "name": "README.md存在",
          "status": "pass",
          "description": "專案根目錄包含README.md",
          "critical": true
        }
      ]
    }
  ],
  "failed_checks": [
    {
      "category": "安全性",
      "name": "依賴漏洞檢查",
      "status": "fail",
      "description": "發現3個高危漏洞",
      "recommendation": "執行 npm audit fix 修復漏洞"
    }
  ],
  "recommendations": [
    {
      "priority": "high",
      "title": "修復安全漏洞",
      "description": "立即修復已發現的高危安全漏洞",
      "action": "npm audit fix"
    }
  ]
}
```

---

## § 6 自動化檢查腳本

### 6.1 Node.js檢查腳本

```javascript
#!/usr/bin/env node

const fs = require('fs');
const path = require('path');
const { execSync } = require('child_process');

class ProjectChecker {
    constructor(projectPath = '.') {
        this.projectPath = projectPath;
        this.results = {
            overall_score: 0,
            categories: [],
            failed_checks: [],
            recommendations: []
        };
    }
    
    async runAllChecks() {
        console.log('🔍 開始專案健康度檢查...\n');
        
        await this.checkProjectStructure();
        await this.checkPackageJson();
        await this.checkGitConfiguration();
        await this.checkDocumentation();
        await this.checkSecurity();
        
        this.calculateOverallScore();
        this.generateRecommendations();
        
        return this.results;
    }
    
    checkProjectStructure() {
        const category = {
            name: '專案結構',
            score: 0,
            max_score: 100,
            checks: []
        };
        
        const requiredFiles = [
            { file: 'README.md', weight: 20, critical: true },
            { file: 'package.json', weight: 15, critical: true },
            { file: '.gitignore', weight: 10, critical: true },
            { file: 'docs/TODO.md', weight: 15, critical: false }
        ];
        
        requiredFiles.forEach(({ file, weight, critical }) => {
            const exists = fs.existsSync(path.join(this.projectPath, file));
            const check = {
                name: `${file}存在`,
                status: exists ? 'pass' : 'fail',
                description: `檢查${file}是否存在`,
                critical,
                weight
            };
            
            category.checks.push(check);
            if (exists) {
                category.score += weight;
            } else if (critical) {
                this.failed_checks.push({
                    ...check,
                    category: category.name
                });
            }
        });
        
        this.results.categories.push(category);
    }
    
    checkPackageJson() {
        const packageJsonPath = path.join(this.projectPath, 'package.json');
        if (!fs.existsSync(packageJsonPath)) return;
        
        const category = {
            name: 'Package.json配置',
            score: 0,
            max_score: 100,
            checks: []
        };
        
        try {
            const packageJson = JSON.parse(fs.readFileSync(packageJsonPath, 'utf8'));
            
            // 檢查必要欄位
            const requiredFields = ['name', 'version', 'description'];
            requiredFields.forEach(field => {
                const exists = packageJson[field];
                const check = {
                    name: `${field}欄位`,
                    status: exists ? 'pass' : 'fail',
                    description: `package.json包含${field}欄位`
                };
                category.checks.push(check);
                if (exists) category.score += 20;
            });
            
            // 檢查開發依賴
            const devDeps = packageJson.devDependencies || {};
            const recommendedDevDeps = ['eslint', 'prettier'];
            recommendedDevDeps.forEach(dep => {
                const exists = devDeps[dep];
                const check = {
                    name: `${dep}開發依賴`,
                    status: exists ? 'pass' : 'warning',
                    description: `建議安裝${dep}`
                };
                category.checks.push(check);
                if (exists) category.score += 10;
            });
            
        } catch (error) {
            this.failed_checks.push({
                category: category.name,
                name: 'package.json解析',
                status: 'fail',
                description: 'package.json格式錯誤'
            });
        }
        
        this.results.categories.push(category);
    }
    
    async checkSecurity() {
        const category = {
            name: '安全性',
            score: 0,
            max_score: 100,
            checks: []
        };
        
        try {
            // 檢查npm audit
            execSync('npm audit --audit-level=high', { 
                cwd: this.projectPath,
                stdio: 'pipe'
            });
            
            category.checks.push({
                name: 'npm audit檢查',
                status: 'pass',
                description: '沒有發現高危漏洞'
            });
            category.score += 50;
            
        } catch (error) {
            const check = {
                name: 'npm audit檢查',
                status: 'fail',
                description: '發現安全漏洞'
            };
            category.checks.push(check);
            this.failed_checks.push({
                ...check,
                category: category.name
            });
        }
        
        // 檢查.env檔案是否在.gitignore中
        const gitignorePath = path.join(this.projectPath, '.gitignore');
        if (fs.existsSync(gitignorePath)) {
            const gitignoreContent = fs.readFileSync(gitignorePath, 'utf8');
            const envIgnored = gitignoreContent.includes('.env');
            
            const check = {
                name: '.env檔案忽略',
                status: envIgnored ? 'pass' : 'warning',
                description: '.env檔案應該被git忽略'
            };
            category.checks.push(check);
            if (envIgnored) category.score += 25;
        }
        
        this.results.categories.push(category);
    }
    
    calculateOverallScore() {
        const totalScore = this.results.categories.reduce((sum, cat) => sum + cat.score, 0);
        const maxScore = this.results.categories.reduce((sum, cat) => sum + cat.max_score, 0);
        this.results.overall_score = Math.round((totalScore / maxScore) * 100);
    }
    
    generateRecommendations() {
        // 基於失敗的檢查生成建議
        this.failed_checks.forEach(check => {
            if (check.name.includes('README.md')) {
                this.results.recommendations.push({
                    priority: 'high',
                    title: '建立README.md',
                    description: '建立專案說明文檔，包含安裝和使用說明',
                    action: 'touch README.md'
                });
            }
            
            if (check.name.includes('npm audit')) {
                this.results.recommendations.push({
                    priority: 'critical',
                    title: '修復安全漏洞',
                    description: '立即修復已發現的安全漏洞',
                    action: 'npm audit fix'
                });
            }
        });
    }
    
    printResults() {
        console.log('\n📊 檢查結果摘要');
        console.log('='.repeat(50));
        console.log(`整體評分: ${this.results.overall_score}/100`);
        
        this.results.categories.forEach(category => {
            console.log(`\n📁 ${category.name}: ${category.score}/${category.max_score}`);
            category.checks.forEach(check => {
                const icon = check.status === 'pass' ? '✅' : 
                           check.status === 'fail' ? '❌' : '⚠️';
                console.log(`  ${icon} ${check.description}`);
            });
        });
        
        if (this.results.recommendations.length > 0) {
            console.log('\n💡 改善建議:');
            this.results.recommendations.forEach((rec, index) => {
                console.log(`${index + 1}. [${rec.priority.toUpperCase()}] ${rec.title}`);
                console.log(`   ${rec.description}`);
                if (rec.action) {
                    console.log(`   執行: ${rec.action}`);
                }
                console.log();
            });
        }
    }
}

// 如果直接執行此腳本
if (require.main === module) {
    const checker = new ProjectChecker();
    checker.runAllChecks().then(() => {
        checker.printResults();
        
        // 根據評分設定退出碼
        process.exit(checker.results.overall_score >= 80 ? 0 : 1);
    });
}

module.exports = ProjectChecker;
```

---

## § 7 使用說明

### 7.1 快速開始

1. **安裝檢查工具**：
```bash
npm install -g cursor-project-checker
```

2. **執行基本檢查**：
```bash
cd your-project
cursor-check
```

3. **查看詳細報告**：
```bash
cursor-check --detailed --output=report.html
```

### 7.2 CI/CD整合

將檢查工具整合到GitHub Actions：

```yaml
name: 專案健康度檢查

on: [push, pull_request]

jobs:
  health-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: cursor-check --ci --fail-on-score=70
```

### 7.3 自訂檢查規則

建立`.cursor-check.json`配置檔案：

```json
{
  "rules": {
    "project_structure": {
      "enabled": true,
      "custom_files": ["SECURITY.md", "DEPLOYMENT.md"]
    },
    "security": {
      "enabled": true,
      "fail_on_high": true,
      "fail_on_medium": false
    },
    "performance": {
      "enabled": true,
      "lighthouse_threshold": 85
    }
  },
  "output": {
    "format": "json",
    "file": "health-report.json"
  }
}
```

---

**專案檢查工具設置完成！** ✅

此工具提供：
- 🔍 全面的專案健康度檢查
- 📊 詳細的評分和報告
- 💡 具體的改善建議
- 🚀 CI/CD整合支援
- ⚙️ 靈活的自訂配置

立即開始檢查您的專案品質！