# 後端工程師專用 Cursor User Rules 配置

## ⚙️ 後端工程師角色配置

```yaml
# 後端工程師專用設定
USER_ROLE: "backend-dev"
specialization: "backend"
primary_technologies: ["Node.js", "Python", "Go", "Java"]
focus_areas: ["API Design", "Database", "Performance", "Security"]
```

---

## § 1 後端特化核心設定

### 1.1 技術棧優先配置 (2025年標準)

```yaml
BACKEND_TECH_STACK:
  languages:
    primary: ["Python 3.11+", "Node.js 20+", "Go 1.21+", "Java 21"]
    secondary: ["Rust", "C#", "PHP 8.3", "Ruby 3.2"]
    
  frameworks:
    python: ["FastAPI", "Django 5", "Flask 3", "Starlette"]
    nodejs: ["Express.js", "Fastify", "Koa", "NestJS"]
    go: ["Gin", "Echo", "Fiber", "Chi"]
    java: ["Spring Boot 3", "Quarkus", "Micronaut"]
    
  databases:
    relational: ["PostgreSQL 16", "MySQL 8", "SQLite", "MariaDB"]
    nosql: ["MongoDB 7", "Redis 7", "Cassandra", "DynamoDB"]
    search: ["Elasticsearch 8", "OpenSearch", "Solr"]
    timeseries: ["InfluxDB", "TimescaleDB", "Prometheus"]
    
  orm_tools:
    python: ["SQLAlchemy 2.0", "Django ORM", "Tortoise ORM"]
    nodejs: ["Prisma", "TypeORM", "Sequelize", "Drizzle"]
    go: ["GORM", "Ent", "SQLBoiler"]
    java: ["Hibernate", "MyBatis", "JOOQ"]
    
  api_frameworks:
    rest: ["OpenAPI 3.1", "JSON:API", "HAL"]
    graphql: ["Apollo Server", "GraphQL Yoga", "Strawberry"]
    grpc: ["Protocol Buffers", "gRPC-Go", "gRPC-Java"]
    
  message_queues:
    async: ["Apache Kafka", "RabbitMQ", "Redis Pub/Sub"]
    cloud: ["AWS SQS", "Google Pub/Sub", "Azure Service Bus"]
    
  caching:
    memory: ["Redis", "Memcached", "Hazelcast"]
    cdn: ["Cloudflare", "AWS CloudFront", "KeyCDN"]
    
  monitoring:
    apm: ["OpenTelemetry", "Jaeger", "Zipkin"]
    metrics: ["Prometheus", "Grafana", "DataDog"]
    logging: ["ELK Stack", "Loki", "Fluentd"]
    
  security:
    authentication: ["JWT", "OAuth 2.1", "OpenID Connect"]
    authorization: ["RBAC", "ABAC", "Casbin"]
    encryption: ["TLS 1.3", "AES-256", "RSA-4096"]
```

### 1.2 後端專用開發流程

**MVP階段 (個人專案)**：
```yaml
mvp_backend_workflow:
  setup:
    - "建立基礎API框架"
    - "設定簡單資料庫schema"
    - "實作核心業務邏輯"
    
  development:
    - "RESTful API設計"
    - "基本CRUD操作"
    - "簡單認證機制"
    
  quality:
    - "API測試覆蓋"
    - "基本錯誤處理"
    - "簡單日誌記錄"
```

**標準階段 (小團隊)**：
```yaml
standard_backend_workflow:
  setup:
    - "OpenAPI文檔生成"
    - "資料庫遷移系統"
    - "環境配置管理"
    
  development:
    - "完整認證授權"
    - "資料驗證機制"
    - "錯誤處理標準化"
    
  quality:
    - "整合測試覆蓋"
    - "效能基準測試"
    - "安全性檢查"
```

**企業階段 (大型團隊)**：
```yaml
enterprise_backend_workflow:
  setup:
    - "微服務架構"
    - "服務發現機制"
    - "分散式追蹤"
    
  development:
    - "事件驅動架構"
    - "CQRS模式實作"
    - "Circuit Breaker模式"
    
  quality:
    - "端到端測試"
    - "混沌工程"
    - "SLA監控"
```

---

## § 2 後端品質門檻標準

### 2.1 效能指標要求

```yaml
BACKEND_PERFORMANCE_GATES:
  api_response_times:
    get_requests: "≤ 100ms (P95)"
    post_requests: "≤ 200ms (P95)"
    complex_queries: "≤ 500ms (P95)"
    
  database_performance:
    query_time: "≤ 100ms (P95)"
    connection_pool: "≥ 95% efficiency"
    index_usage: "≥ 90% queries use indexes"
    
  throughput:
    concurrent_requests: "≥ 1000 RPS"
    cpu_utilization: "≤ 70% under load"
    memory_usage: "≤ 80% of allocated"
    
  scalability:
    horizontal_scaling: "Linear performance gain"
    auto_scaling: "Response time ≤ 2min"
    load_balancing: "Even distribution ±10%"
```

### 2.2 可靠性指標

```yaml
BACKEND_RELIABILITY_GATES:
  availability:
    uptime: "≥ 99.9%"
    mttr: "≤ 30min"
    mtbf: "≥ 720 hours"
    
  error_handling:
    error_rate: "≤ 0.1%"
    timeout_handling: "Graceful degradation"
    circuit_breaker: "Automatic recovery"
    
  data_integrity:
    backup_success: "100%"
    data_validation: "100% input validation"
    transaction_consistency: "ACID compliance"
```

---

## § 3 API設計最佳實踐

### 3.1 RESTful API標準

```yaml
REST_API_STANDARDS:
  url_structure:
    pattern: "/api/v1/resources/{id}/sub-resources"
    naming: "kebab-case for URLs"
    versioning: "URL path versioning"
    
  http_methods:
    GET: "Retrieve resources (idempotent)"
    POST: "Create new resources"
    PUT: "Full update (idempotent)"
    PATCH: "Partial update"
    DELETE: "Remove resources (idempotent)"
    
  status_codes:
    success: [200, 201, 202, 204]
    client_error: [400, 401, 403, 404, 409, 422]
    server_error: [500, 502, 503, 504]
    
  response_format:
    success: |
      {
        "data": {...},
        "meta": {
          "timestamp": "2025-06-16T10:49:55+08:00",
          "version": "1.0"
        }
      }
    error: |
      {
        "error": {
          "code": "VALIDATION_ERROR",
          "message": "Invalid input data",
          "details": [...],
          "trace_id": "abc123"
        }
      }
```

### 3.2 GraphQL最佳實踐

```yaml
GRAPHQL_STANDARDS:
  schema_design:
    naming: "PascalCase for types, camelCase for fields"
    nullable: "Explicit nullable/non-nullable"
    pagination: "Relay-style cursor pagination"
    
  query_optimization:
    depth_limiting: "Maximum 10 levels"
    complexity_analysis: "Cost-based limiting"
    dataloader: "N+1 query prevention"
    
  security:
    query_whitelist: "Production query whitelist"
    rate_limiting: "Query-based rate limiting"
    authentication: "Context-based auth"
```

---

## § 4 資料庫設計與優化

### 4.1 關聯式資料庫最佳實踐

```sql
-- 資料表設計標準
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    deleted_at TIMESTAMP WITH TIME ZONE NULL,
    
    -- 索引設計
    CONSTRAINT valid_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$')
);

-- 效能索引
CREATE INDEX CONCURRENTLY idx_users_email ON users(email) WHERE deleted_at IS NULL;
CREATE INDEX CONCURRENTLY idx_users_created_at ON users(created_at);

-- 軟刪除視圖
CREATE VIEW active_users AS 
SELECT * FROM users WHERE deleted_at IS NULL;
```

### 4.2 NoSQL資料庫模式

```javascript
// MongoDB文檔設計
{
  "_id": ObjectId("..."),
  "user_id": "uuid-here",
  "profile": {
    "first_name": "John",
    "last_name": "Doe",
    "avatar_url": "https://...",
    "preferences": {
      "language": "zh-TW",
      "timezone": "Asia/Taipei"
    }
  },
  "metadata": {
    "created_at": ISODate("2025-06-16T02:49:55Z"),
    "updated_at": ISODate("2025-06-16T02:49:55Z"),
    "version": 1
  },
  
  // 索引設計
  "indexes": [
    { "user_id": 1 },
    { "profile.email": 1 },
    { "metadata.created_at": -1 }
  ]
}
```

---

## § 5 後端安全最佳實踐

### 5.1 認證與授權

```python
# JWT實作範例
import jwt
from datetime import datetime, timedelta
from passlib.context import CryptContext

class AuthService:
    def __init__(self):
        self.pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")
        self.secret_key = os.getenv("JWT_SECRET_KEY")
        self.algorithm = "HS256"
        self.access_token_expire = timedelta(minutes=30)
        self.refresh_token_expire = timedelta(days=7)
    
    def verify_password(self, plain_password: str, hashed_password: str) -> bool:
        return self.pwd_context.verify(plain_password, hashed_password)
    
    def get_password_hash(self, password: str) -> str:
        return self.pwd_context.hash(password)
    
    def create_access_token(self, data: dict) -> str:
        to_encode = data.copy()
        expire = datetime.utcnow() + self.access_token_expire
        to_encode.update({"exp": expire, "type": "access"})
        return jwt.encode(to_encode, self.secret_key, algorithm=self.algorithm)
    
    def create_refresh_token(self, data: dict) -> str:
        to_encode = data.copy()
        expire = datetime.utcnow() + self.refresh_token_expire
        to_encode.update({"exp": expire, "type": "refresh"})
        return jwt.encode(to_encode, self.secret_key, algorithm=self.algorithm)
```

### 5.2 API安全檢查清單

```yaml
API_SECURITY_CHECKLIST:
  input_validation:
    - "所有輸入進行嚴格驗證"
    - "使用允許清單而非阻止清單"
    - "SQL注入防護"
    - "XSS防護"
    
  authentication:
    - "強密碼政策"
    - "多因素認證支援"
    - "帳號鎖定機制"
    - "密碼雜湊使用bcrypt/scrypt"
    
  authorization:
    - "最小權限原則"
    - "資源層級權限檢查"
    - "API端點權限矩陣"
    - "RBAC/ABAC實作"
    
  data_protection:
    - "敏感資料加密"
    - "HTTPS強制執行"
    - "安全標頭設定"
    - "CORS正確配置"
    
  monitoring:
    - "異常登入偵測"
    - "API濫用監控"
    - "安全事件日誌"
    - "漏洞掃描自動化"
```

---

## § 6 後端專用自然語言指令

### 6.1 API開發指令

```bash
# API相關
create-api [ResourceName]           # 建立RESTful API資源
create-endpoint [Method] [Path]     # 建立特定API端點
generate-docs                       # 生成OpenAPI文檔
test-api [EndpointName]            # 測試特定API端點

# 資料庫相關
create-model [ModelName]           # 建立資料模型
create-migration [Description]     # 建立資料庫遷移
seed-database                      # 填充測試資料
optimize-queries                   # 優化資料庫查詢

# 服務相關
create-service [ServiceName]       # 建立業務服務
create-middleware [MiddlewareName] # 建立中介軟體
setup-auth                        # 設定認證機制
setup-cache                       # 設定快取系統
```

### 6.2 效能與監控指令

```bash
# 效能分析
profile-api                        # API效能分析
analyze-queries                    # 資料庫查詢分析
memory-usage                       # 記憶體使用分析
load-test [Endpoint]              # 負載測試

# 監控設定
setup-logging                      # 設定日誌系統
setup-metrics                     # 設定監控指標
setup-alerts                      # 設定告警規則
health-check                      # 健康檢查端點
```

---

## § 7 後端專用TODO模板

### 7.1 API開發TODO

```markdown
## TODO-P1-API-BACKEND-用戶管理API

**建立時間**: 2025-06-16T10:49:55+08:00
**負責人**: @{{USER_ROLE}}
**預計完成**: 2025-06-23T23:59:59+08:00
**狀態**: 待開始
**專案階段**: 標準

### API規格需求
- **資源**: User, Profile, Settings
- **端點**: CRUD操作 + 特殊業務邏輯
- **認證**: JWT Bearer Token
- **權限**: Role-based access control

### 技術實作需求
- **資料模型**: User, UserProfile, UserSettings
- **API路由**: /api/v1/users/* 
- **中介軟體**: 認證、授權、驗證、日誌
- **測試**: 單元測試 + 整合測試

### 接受條件
- [ ] 資料模型設計完成
- [ ] API端點實作完成
- [ ] 認證授權機制整合
- [ ] 輸入驗證實作
- [ ] 錯誤處理標準化
- [ ] API文檔生成
- [ ] 單元測試覆蓋率 ≥ 90%
- [ ] 整合測試完成
- [ ] 效能測試通過
- [ ] 安全性檢查通過

### 技術風險
- **效能**: 大量用戶查詢可能影響效能
- **安全**: 敏感資料保護需要特別注意
- **擴展性**: 設計需考慮未來功能擴展

### 相關資源
- API設計文檔: docs/api/users.md
- 資料庫Schema: docs/database/users.sql
- 安全規範: docs/security/auth.md
```

---

## § 8 微服務架構指導

### 8.1 服務拆分原則

```yaml
MICROSERVICES_PRINCIPLES:
  service_boundaries:
    business_capability: "按業務能力拆分服務"
    data_ownership: "每個服務擁有自己的資料"
    team_structure: "符合康威定律的團隊結構"
    
  service_size:
    team_rule: "兩個披薩團隊可以維護"
    complexity_rule: "單一職責原則"
    deployment_rule: "獨立部署單元"
    
  communication:
    synchronous: "HTTP/gRPC for request-response"
    asynchronous: "Message queues for events"
    data_consistency: "Eventual consistency"
```

### 8.2 服務間通訊模式

```javascript
// Event-driven communication
class EventBus {
    constructor() {
        this.kafka = new KafkaJS({
            clientId: 'user-service',
            brokers: ['kafka1:9092', 'kafka2:9092']
        });
    }
    
    async publishEvent(topic, event) {
        const producer = this.kafka.producer();
        await producer.connect();
        
        await producer.send({
            topic,
            messages: [{
                key: event.aggregateId,
                value: JSON.stringify({
                    ...event,
                    timestamp: new Date().toISOString(),
                    version: '1.0'
                })
            }]
        });
        
        await producer.disconnect();
    }
    
    async subscribeToEvents(topic, handler) {
        const consumer = this.kafka.consumer({ 
            groupId: `${topic}-consumer-group` 
        });
        
        await consumer.connect();
        await consumer.subscribe({ topic });
        
        await consumer.run({
            eachMessage: async ({ message }) => {
                const event = JSON.parse(message.value.toString());
                await handler(event);
            }
        });
    }
}
```

---

## § 9 部署與維運最佳實踐

### 9.1 容器化配置

```dockerfile
# 多階段建置 - Node.js範例
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

FROM node:20-alpine AS runtime
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001

# 安全性設定
RUN apk add --no-cache dumb-init
USER nextjs

WORKDIR /app
COPY --from=builder --chown=nextjs:nodejs /app/node_modules ./node_modules
COPY --chown=nextjs:nodejs ./src ./src
COPY --chown=nextjs:nodejs ./package.json ./

# 健康檢查
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

EXPOSE 3000
ENTRYPOINT ["dumb-init", "--"]
CMD ["node", "src/index.js"]
```

### 9.2 Kubernetes部署配置

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
  labels:
    app: user-service
    version: v1
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
        version: v1
    spec:
      securityContext:
        runAsNonRoot: true
        runAsUser: 1001
        fsGroup: 1001
      containers:
      - name: user-service
        image: myregistry/user-service:v1.2.0
        ports:
        - containerPort: 3000
          name: http
        env:
        - name: NODE_ENV
          value: "production"
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: user-service-secrets
              key: database-url
        resources:
          requests:
            memory: "256Mi"
            cpu: "200m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 5
        securityContext:
          allowPrivilegeEscalation: false
          readOnlyRootFilesystem: true
          capabilities:
            drop:
            - ALL
```

---

## § 10 監控與可觀測性

### 10.1 結構化日誌

```python
import structlog
import logging

# 設定結構化日誌
structlog.configure(
    processors=[
        structlog.stdlib.filter_by_level,
        structlog.stdlib.add_logger_name,
        structlog.stdlib.add_log_level,
        structlog.stdlib.PositionalArgumentsFormatter(),
        structlog.processors.TimeStamper(fmt="iso"),
        structlog.processors.StackInfoRenderer(),
        structlog.processors.format_exc_info,
        structlog.processors.UnicodeDecoder(),
        structlog.processors.JSONRenderer()
    ],
    context_class=dict,
    logger_factory=structlog.stdlib.LoggerFactory(),
    wrapper_class=structlog.stdlib.BoundLogger,
    cache_logger_on_first_use=True,
)

logger = structlog.get_logger()

# 使用範例
@app.middleware("http")
async def logging_middleware(request: Request, call_next):
    start_time = time.time()
    
    # 請求日誌
    logger.info(
        "Request started",
        method=request.method,
        url=str(request.url),
        user_id=getattr(request.state, 'user_id', None),
        trace_id=getattr(request.state, 'trace_id', None)
    )
    
    response = await call_next(request)
    
    # 回應日誌
    duration = time.time() - start_time
    logger.info(
        "Request completed",
        method=request.method,
        url=str(request.url),
        status_code=response.status_code,
        duration=duration,
        user_id=getattr(request.state, 'user_id', None),
        trace_id=getattr(request.state, 'trace_id', None)
    )
    
    return response
```

### 10.2 監控指標收集

```python
from prometheus_client import Counter, Histogram, Gauge, start_http_server
import time

# 定義監控指標
REQUEST_COUNT = Counter(
    'http_requests_total',
    'Total HTTP requests',
    ['method', 'endpoint', 'status']
)

REQUEST_DURATION = Histogram(
    'http_request_duration_seconds',
    'HTTP request duration',
    ['method', 'endpoint']
)

ACTIVE_CONNECTIONS = Gauge(
    'active_connections',
    'Active database connections'
)

# 中介軟體範例
@app.middleware("http")
async def metrics_middleware(request: Request, call_next):
    start_time = time.time()
    
    response = await call_next(request)
    
    # 記錄指標
    REQUEST_COUNT.labels(
        method=request.method,
        endpoint=request.url.path,
        status=response.status_code
    ).inc()
    
    REQUEST_DURATION.labels(
        method=request.method,
        endpoint=request.url.path
    ).observe(time.time() - start_time)
    
    return response

# 自訂業務指標
def track_user_action(action: str, user_id: str):
    USER_ACTIONS.labels(
        action=action,
        user_type=get_user_type(user_id)
    ).inc()
```

---

## § 11 後端學習成長路徑

### 11.1 技能發展階梯

**初級後端工程師**：
- HTTP協議和RESTful API基礎
- 關聯式資料庫設計和SQL
- 單一語言框架熟練使用
- 基礎的錯誤處理和日誌

**中級後端工程師**：
- 微服務架構理解和實踐
- NoSQL資料庫選型和使用
- 快取策略和效能優化
- 安全性最佳實踐實作

**高級後端工程師**：
- 分散式系統設計能力
- 高併發和高可用架構
- 系統監控和故障排除
- 技術選型和架構決策

**後端架構師**：
- 企業級系統架構設計
- 跨團隊技術領導能力
- 業務需求轉技術實作
- 技術風險評估和管理

### 11.2 2025年重點學習領域

```yaml
learning_priorities_2025:
  cloud_native:
    - "Kubernetes深度應用和優化"
    - "Service Mesh架構實踐"
    - "Serverless架構模式"
    - "邊緣計算開發模式"
    
  data_architecture:
    - "事件驅動架構設計"
    - "CQRS和Event Sourcing"
    - "分散式資料一致性"
    - "實時資料處理管道"
    
  ai_integration:
    - "大語言模型API整合"
    - "向量資料庫應用"
    - "AI輔助代碼生成"
    - "智能監控和預警"
    
  advanced_patterns:
    - "領域驅動設計實踐"
    - "Hexagonal架構"
    - "Clean Architecture"
    - "功能式程式設計模式"
```

---

## § 12 後端項目檢查清單

### 12.1 專案啟動檢查

- [ ] **架構設計**：確認單體、微服務或混合架構
- [ ] **技術選型**：語言、框架、資料庫、部署平台
- [ ] **開發環境**：Docker、IDE配置、代碼規範
- [ ] **API設計**：RESTful規範、OpenAPI文檔

### 12.2 開發中檢查

- [ ] **程式碼品質**：Linting、格式化、複雜度控制
- [ ] **測試覆蓋**：單元測試、整合測試、API測試
- [ ] **安全性**：認證授權、輸入驗證、加密傳輸
- [ ] **效能**：查詢優化、快取策略、負載測試

### 12.3 發布前檢查

- [ ] **生產準備**：環境變數、健康檢查、監控告警
- [ ] **資料庫**：遷移腳本、備份策略、效能調優
- [ ] **部署**：CI/CD管道、回滾計劃、藍綠部署
- [ ] **文檔**：API文檔、運維手冊、故障排除指南

---

**後端工程師專用配置完成！** ⚙️

此配置專為後端開發優化，提供：
- ✅ 現代後端技術棧支援
- ✅ API設計和資料庫最佳實踐
- ✅ 微服務架構指導
- ✅ 安全性和效能標準
- ✅ 監控和可觀測性實踐

立即開始您的高效後端開發之旅！