# Study Quest - 시스템 아키텍처

**버전**: 1.0
**작성일**: 2025-11-17
**대상**: MVP 구현

---

## 🏗️ 전체 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────────────┐
│                        Client Layer                             │
│                                                                 │
│  ┌──────────────────────┐      ┌──────────────────────┐        │
│  │                      │      │                      │        │
│  │   iOS Application    │      │  Android Application │        │
│  │   (React Native)     │      │   (React Native)     │        │
│  │                      │      │                      │        │
│  └──────────┬───────────┘      └──────────┬───────────┘        │
│             │                             │                    │
└─────────────┼─────────────────────────────┼────────────────────┘
              │                             │
              │         HTTPS/TLS 1.3       │
              │                             │
              └─────────────┬───────────────┘
                            │
┌───────────────────────────▼───────────────────────────┐
│                     API Gateway                       │
│                   (Load Balancer)                     │
└───────────────────────────┬───────────────────────────┘
                            │
              ┌─────────────┼─────────────┐
              │             │             │
┌─────────────▼──┐  ┌───────▼────────┐  ┌▼──────────────┐
│                │  │                │  │               │
│  Auth Service  │  │  API Service   │  │  AI Service   │
│  (Express)     │  │  (Express)     │  │  (Express)    │
│                │  │                │  │               │
│  - JWT 발급     │  │  - REST API    │  │  - GPT-4o     │
│  - OAuth 2.0   │  │  - Validation  │  │  - Prompt Eng │
│  - 세션 관리    │  │  - Business    │  │  - Caching    │
│                │  │    Logic       │  │               │
└────────┬───────┘  └───────┬────────┘  └───┬───────────┘
         │                  │                │
         └──────────────────┼────────────────┘
                            │
         ┌──────────────────┼────────────────┐
         │                  │                │
┌────────▼────────┐  ┌──────▼──────┐  ┌─────▼──────────┐
│                 │  │             │  │                │
│  PostgreSQL DB  │  │  Redis      │  │  External APIs │
│  (AWS RDS)      │  │  (Cache)    │  │                │
│                 │  │             │  │  - OpenAI      │
│  - Users        │  │  - Session  │  │  - FCM/APNs    │
│  - StudyPlans   │  │  - AI Cache │  │  - OAuth       │
│  - Quests       │  │             │  │                │
│  - ChatHistory  │  │             │  │                │
│                 │  │             │  │                │
└─────────────────┘  └─────────────┘  └────────────────┘
```

---

## 🔧 기술 스택

### Frontend (Mobile)

```yaml
Framework: React Native 0.72
Language: TypeScript 5.x
Navigation: React Navigation 6.x
State Management: Zustand 4.x
UI Components:
  - React Native Paper (Material Design)
  - react-native-chart-kit (Charts)
  - react-native-reanimated (Animations)
Networking: Axios
Storage: AsyncStorage (Local), SecureStore (Sensitive)
Testing: Jest + React Native Testing Library
```

### Backend (API)

```yaml
Runtime: Node.js 18.x
Framework: Express 4.x
Language: TypeScript 5.x
ORM: Prisma 5.x
Validation: Zod
Authentication: jsonwebtoken (JWT)
Password: bcrypt
Logging: Winston
Testing: Jest + Supertest
API Docs: Swagger (OpenAPI 3.0)
```

### Database

```yaml
Primary DB: PostgreSQL 15.x (AWS RDS)
Caching: Redis 7.x
File Storage: AWS S3
Backup: AWS RDS Auto Backup (Daily)
```

### AI & External Services

```yaml
AI Model: OpenAI GPT-4o
Prompt: Custom System Prompts (3 characters)
Caching: Redis (24h TTL)
Push Notifications:
  - iOS: Apple Push Notification Service (APNs)
  - Android: Firebase Cloud Messaging (FCM)
OAuth:
  - Google OAuth 2.0
  - Apple Sign In
  - Kakao OAuth
```

### DevOps & Hosting

```yaml
Cloud Provider: AWS
Compute: EC2 (t3.medium × 2)
Database: RDS PostgreSQL
Storage: S3
CDN: CloudFront
CI/CD: GitHub Actions
Monitoring: CloudWatch + Sentry
Container: Docker + Docker Compose
```

---

## 📊 데이터 모델 (ERD)

### 핵심 테이블

```sql
-- Users 테이블
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255),
    name VARCHAR(100),
    grade VARCHAR(20), -- '재수생', 'N수생', '고3'
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- User Goals 테이블
CREATE TABLE user_goals (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    subject VARCHAR(50), -- '수학', '국어', '영어' 등
    current_score INTEGER,
    target_score INTEGER,
    target_university VARCHAR(100),
    exam_date DATE, -- 수능일
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Study Plans 테이블
CREATE TABLE study_plans (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    goal_id UUID REFERENCES user_goals(id) ON DELETE CASCADE,
    phase INTEGER, -- 1, 2, 3
    phase_name VARCHAR(100), -- '1-3개월: 기본 개념 완성'
    focus_topics TEXT[], -- ['함수', '수열', '미분']
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Daily Quests 테이블
CREATE TABLE daily_quests (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    plan_id UUID REFERENCES study_plans(id) ON DELETE CASCADE,
    date DATE NOT NULL,
    subject VARCHAR(50),
    topic VARCHAR(100),
    description TEXT, -- '수학I 함수 문제 10개'
    estimated_minutes INTEGER,
    is_completed BOOLEAN DEFAULT FALSE,
    completed_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- AI Characters 테이블
CREATE TABLE ai_characters (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(50), -- 'mentor_A', 'friend_B', 'hybrid_C'
    display_name VARCHAR(100),
    persona TEXT, -- System Prompt
    tone VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Chat Histories 테이블
CREATE TABLE chat_histories (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    character_id UUID REFERENCES ai_characters(id),
    user_message TEXT,
    ai_response TEXT,
    emotion VARCHAR(50), -- 'positive', 'negative', 'slump'
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Refresh Tokens 테이블
CREATE TABLE refresh_tokens (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    token VARCHAR(500) UNIQUE NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**ERD 다이어그램**: `design/database-erd.png` 참조

---

## 🔐 보안 아키텍처

### 인증 흐름 (JWT)

```
1. 사용자 로그인
   ↓
2. 이메일/비밀번호 검증 (bcrypt)
   ↓
3. Access Token 발급 (15분, HS256)
   Payload: { userId, email, exp }
   ↓
4. Refresh Token 발급 (7일)
   DB 저장 (refresh_tokens 테이블)
   ↓
5. 클라이언트 저장
   - Access Token: Memory
   - Refresh Token: SecureStore
   ↓
6. API 요청 시
   Authorization: Bearer <access_token>
   ↓
7. Access Token 만료 시
   Refresh Token으로 재발급
```

### 데이터 암호화

- **전송 중**: TLS 1.3 (HTTPS)
- **저장 시**:
  - 비밀번호: bcrypt (salt rounds: 12)
  - 민감 정보: AES-256
  - DB: AWS RDS Encryption at Rest

### API 보안

```typescript
// Rate Limiting
import rateLimit from 'express-rate-limit';

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15분
  max: 100, // 최대 100 요청
  message: 'Too many requests, please try again later.'
});

app.use('/api/', limiter);

// CORS 설정
import cors from 'cors';

app.use(cors({
  origin: process.env.ALLOWED_ORIGINS?.split(','),
  credentials: true
}));

// Helmet (보안 헤더)
import helmet from 'helmet';

app.use(helmet());
```

---

## ⚡ 성능 최적화

### 1. API 응답 시간 (목표: 500ms 이내)

**전략**:
- Database Indexing (user_id, date, subject)
- Redis Caching (자주 조회되는 데이터)
- Connection Pooling (PostgreSQL)

```typescript
// Redis 캐싱 예시
async function getTodayQuests(userId: string) {
  const cacheKey = `quests:${userId}:${today}`;

  // 캐시 확인
  const cached = await redis.get(cacheKey);
  if (cached) return JSON.parse(cached);

  // DB 조회
  const quests = await prisma.dailyQuest.findMany({
    where: { userId, date: today }
  });

  // 캐시 저장 (1시간)
  await redis.setex(cacheKey, 3600, JSON.stringify(quests));

  return quests;
}
```

### 2. AI 응답 시간 (목표: 3초 이내)

**전략**:
- 동일 목표 캐싱 (Redis, 24시간)
- 출력 토큰 제한 (max_tokens: 1500)
- Streaming 응답 (SSE)

```typescript
// AI 캐싱
async function generateStudyPlan(userGoal: string) {
  const cacheKey = `plan:${hashGoal(userGoal)}`;

  const cached = await redis.get(cacheKey);
  if (cached) return JSON.parse(cached);

  const plan = await openai.chat.completions.create({
    model: 'gpt-4o',
    messages: [
      { role: 'system', content: SYSTEM_PROMPT },
      { role: 'user', content: userGoal }
    ],
    max_tokens: 1500,
    temperature: 0.7
  });

  await redis.setex(cacheKey, 86400, JSON.stringify(plan));

  return plan;
}
```

### 3. 데이터베이스 인덱싱

```sql
-- 성능 최적화 인덱스
CREATE INDEX idx_daily_quests_user_date ON daily_quests(user_id, date);
CREATE INDEX idx_chat_histories_user ON chat_histories(user_id, created_at DESC);
CREATE INDEX idx_study_plans_user ON study_plans(user_id, phase);
```

---

## 📡 API 설계

### RESTful API 엔드포인트

#### Authentication
```
POST   /api/auth/register          # 회원가입
POST   /api/auth/login             # 로그인
POST   /api/auth/refresh           # 토큰 갱신
POST   /api/auth/logout            # 로그아웃
POST   /api/auth/oauth/google      # Google OAuth
POST   /api/auth/oauth/apple       # Apple Sign In
POST   /api/auth/oauth/kakao       # Kakao OAuth
```

#### Onboarding
```
POST   /api/onboarding/start       # 온보딩 시작
PUT    /api/onboarding/step/:step  # 단계별 저장
POST   /api/onboarding/complete    # 온보딩 완료
GET    /api/onboarding/status      # 현재 상태
```

#### Study Plans (AI 목표 분해)
```
POST   /api/study-plans/generate   # AI 목표 분해
GET    /api/study-plans/            # 내 학습 계획 목록
GET    /api/study-plans/:id         # 특정 계획 상세
PUT    /api/study-plans/:id         # 계획 수정
DELETE /api/study-plans/:id         # 계획 삭제
```

#### Daily Quests
```
GET    /api/quests/today           # 오늘의 퀘스트
GET    /api/quests/date/:date      # 특정 날짜 퀘스트
PUT    /api/quests/:id/complete    # 퀘스트 완료
GET    /api/quests/progress        # 진도율 조회
```

#### AI Chat
```
POST   /api/chat/send              # 메시지 전송
GET    /api/chat/history           # 대화 히스토리
PUT    /api/chat/character         # 캐릭터 변경
GET    /api/chat/characters        # 캐릭터 목록
```

#### User Profile
```
GET    /api/profile                # 프로필 조회
PUT    /api/profile                # 프로필 수정
DELETE /api/profile                # 계정 삭제
POST   /api/profile/avatar         # 프로필 사진 업로드
```

#### Notifications
```
POST   /api/notifications/register # 디바이스 토큰 등록
GET    /api/notifications/settings # 알림 설정 조회
PUT    /api/notifications/settings # 알림 설정 수정
```

자세한 API 명세는 [API_SPECIFICATION.md](API_SPECIFICATION.md) 참조

---

## 🗄️ 데이터베이스 설계

### 테이블 관계도

```
users (1) ────────────── (N) user_goals
  │                           │
  │                           │
  ├─── (N) study_plans ───────┘
  │           │
  │           └─── (N) daily_quests
  │
  ├─── (N) chat_histories
  │           │
  │           └─── (N) ai_characters
  │
  ├─── (N) refresh_tokens
  │
  └─── (1) user_profiles
```

자세한 스키마는 [DATABASE_SCHEMA.md](DATABASE_SCHEMA.md) 참조

---

## 🤖 AI 통합 아키텍처

### AI Service 구조

```
AI Service
├── Goal Decomposition Engine
│   ├── Input Parser (자연어 → 구조화)
│   ├── Curriculum Matcher (과목/단원 매칭)
│   ├── GPT-4o API Call
│   └── Output Formatter (JSON → DB)
│
├── Character Chat Engine
│   ├── Character Selector (A/B/C)
│   ├── Context Builder (최근 10턴)
│   ├── Emotion Analyzer (슬럼프 감지)
│   ├── GPT-4o API Call
│   └── Response Formatter
│
└── Optimization Layer
    ├── Redis Caching
    ├── Rate Limiting
    └── Cost Tracking
```

### Prompt Engineering

```typescript
const SYSTEM_PROMPTS = {
  goalDecomposition: `
당신은 20년 경력의 입시 컨설턴트입니다.
재수생의 목표를 Phase별 계획과 일일 퀘스트로 분해합니다.

출력 형식: JSON
{
  "phases": [...],
  "daily_quests": [...]
}
  `,

  mentorCharacter: `
당신은 30대 입시 컨설턴트입니다.
단호하지만 격려하는 태도로 데이터 기반 조언을 제공합니다.
  `,

  friendCharacter: `
당신은 20대 재수 성공 선배입니다.
공감하고 격려하는 태도로 작은 성취를 축하합니다.
  `,

  hybridCharacter: `
당신은 25세 대학생 멘토입니다.
상황에 따라 격려와 질책을 적절히 조절합니다.
  `
};
```

---

## 🚀 배포 아키텍처 (AWS)

### Production 환경

```
┌─────────────────────────────────────────────────────┐
│                   AWS Cloud                         │
│                                                     │
│  ┌─────────────────────────────────────────┐       │
│  │          Route 53 (DNS)                 │       │
│  └───────────────┬─────────────────────────┘       │
│                  │                                  │
│  ┌───────────────▼─────────────────────────┐       │
│  │      CloudFront (CDN)                   │       │
│  └───────────────┬─────────────────────────┘       │
│                  │                                  │
│  ┌───────────────▼─────────────────────────┐       │
│  │  Application Load Balancer              │       │
│  └───────────────┬─────────────────────────┘       │
│                  │                                  │
│         ┌────────┴────────┐                        │
│         │                 │                        │
│  ┌──────▼──────┐   ┌──────▼──────┐                │
│  │  EC2 (API)  │   │  EC2 (API)  │                │
│  │  Primary    │   │  Standby    │                │
│  └──────┬──────┘   └──────┬──────┘                │
│         │                 │                        │
│         └────────┬────────┘                        │
│                  │                                  │
│         ┌────────▼─────────┐                       │
│         │                  │                       │
│  ┌──────▼──────┐    ┌──────▼──────┐               │
│  │ RDS Primary │    │  ElastiCache│               │
│  │ (PostgreSQL)│    │   (Redis)   │               │
│  └──────┬──────┘    └─────────────┘               │
│         │                                          │
│  ┌──────▼──────┐                                  │
│  │ RDS Replica │ (Read-only)                      │
│  │ (Standby)   │                                  │
│  └─────────────┘                                  │
│                                                    │
│  ┌─────────────────────────────────────────┐      │
│  │  S3 (File Storage)                      │      │
│  │  - 프로필 사진                           │      │
│  │  - 로그 파일                             │      │
│  └─────────────────────────────────────────┘      │
│                                                    │
└────────────────────────────────────────────────────┘
```

### CI/CD Pipeline (GitHub Actions)

```yaml
# .github/workflows/deploy.yml
name: Deploy to AWS

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - Checkout code
      - Setup Node.js
      - Install dependencies
      - Run tests (Jest)
      - Run linting (ESLint)
      - Check TypeScript

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - Build Docker image
      - Push to ECR

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - SSH to EC2
      - Pull new Docker image
      - Run database migrations
      - Restart containers
      - Health check
```

---

## 📈 확장성 (Scalability)

### 수평 확장 전략

| 시기 | MAU | 서버 구성 | 예상 비용 |
|------|-----|----------|----------|
| **1년 차** | 10,000 | EC2 t3.medium × 1, RDS db.t3.small | 월 $150 (20만원) |
| **2년 차** | 50,000 | EC2 t3.large × 2, RDS db.t3.medium | 월 $500 (67만원) |
| **3년 차** | 100,000 | EC2 t3.xlarge × 3, RDS db.r5.large | 월 $1,200 (160만원) |

### Auto Scaling 설정

```yaml
AutoScaling:
  MinInstances: 1
  MaxInstances: 5
  TargetCPU: 70%
  TargetMemory: 80%
  ScaleUpCooldown: 300s
  ScaleDownCooldown: 600s
```

---

## 🔍 모니터링 및 로깅

### CloudWatch Metrics

```
Custom Metrics:
├── API Response Time (ms)
├── AI Response Time (ms)
├── Quest Completion Rate (%)
├── Daily Active Users (count)
├── AI API Cost ($)
└── Error Rate (%)

Alarms:
├── API Response Time > 1000ms
├── Error Rate > 5%
├── CPU Usage > 80%
└── Database Connections > 90%
```

### Logging Strategy

```typescript
import winston from 'winston';

const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  transports: [
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' }),
    new winston.transports.Console({ format: winston.format.simple() })
  ]
});

// 사용 예시
logger.info('User login', { userId, email });
logger.error('AI API failed', { error, userId });
```

---

## 🎯 비기능 요구사항 구현

### 성능 요구사항

| 항목 | 목표 | 구현 방법 |
|------|------|-----------|
| 앱 초기 로딩 | 3초 이내 | Code Splitting, Lazy Loading |
| AI 응답 속도 | 3초 이내 | Redis 캐싱, 출력 토큰 제한 |
| API 응답 시간 | 500ms 이내 | DB 인덱싱, Connection Pooling |
| 동시 사용자 | 10,000 MAU | Auto Scaling, Load Balancer |

### 가용성 요구사항

| 항목 | 목표 | 구현 방법 |
|------|------|-----------|
| Uptime | 99.5% | Multi-AZ 배포, Health Check |
| RTO | 1시간 | Auto Recovery, Standby Instance |
| RPO | 1시간 | RDS Auto Backup (5분 간격) |

---

## 🔄 향후 아키텍처 개선 계획

### Phase 2 (6개월 차)
- Microservices 전환 (Auth, API, AI 분리)
- Kubernetes 도입 (Container Orchestration)
- GraphQL API 추가 (React Native 최적화)

### Phase 3 (1년 차)
- Multi-Region 배포 (서울 + 도쿄)
- CDN 최적화 (CloudFront)
- AI 모델 자체 호스팅 (비용 절감)

---

**작성자**: Study Quest 개발팀
**검토자**: System Architect
**승인일**: 2025-11-17
