# HACK-SeSAC GitHub 저장소 구조 가이드

**목적**: 예선 개발 현황 확인 + 본선 MVP 시연
**프로젝트**: Study Quest (재수생 AI 학습 관리 플랫폼)

---

## 📋 필수 업로드 항목

### 1. 프로젝트 문서 (Documentation) - 예선 평가용

```
docs/
├── README.md                          # 프로젝트 전체 소개 (필수!)
├── PROJECT_OVERVIEW.md                # 프로젝트 개요 및 목표
├── PRD.md                            # Product Requirements Document
├── ARCHITECTURE.md                   # 시스템 아키텍처
├── API_SPECIFICATION.md              # API 명세서
├── DATABASE_SCHEMA.md                # 데이터베이스 설계
├── AI_STRATEGY.md                    # AI 데이터 및 모델 전략
└── DEVELOPMENT_ROADMAP.md            # 개발 로드맵
```

### 2. 설계 문서 (Design Documents)

```
design/
├── wireframes/                       # 와이어프레임 (Figma 링크 or 이미지)
│   ├── onboarding-flow.png
│   ├── home-screen.png
│   ├── ai-chat.png
│   └── progress-tracking.png
├── user-flow.md                      # 사용자 플로우
├── ui-ux-guide.md                    # UI/UX 디자인 가이드
└── design-system.md                  # 디자인 시스템 (색상, 타이포그래피 등)
```

### 3. MVP 구현 코드 - 본선 시연용

#### Option 1: 실제 코드 (풀스택 개발)

```
src/
├── frontend/                         # React Native 앱
│   ├── package.json
│   ├── App.tsx
│   ├── screens/
│   │   ├── OnboardingScreen.tsx
│   │   ├── HomeScreen.tsx
│   │   ├── AIChatScreen.tsx
│   │   └── ProgressScreen.tsx
│   ├── components/
│   │   ├── QuestCard.tsx
│   │   ├── ProgressChart.tsx
│   │   └── ChatBubble.tsx
│   ├── services/
│   │   ├── api.ts
│   │   └── storage.ts
│   └── utils/
│
├── backend/                          # Node.js + Express API
│   ├── package.json
│   ├── src/
│   │   ├── server.ts
│   │   ├── routes/
│   │   │   ├── auth.ts
│   │   │   ├── onboarding.ts
│   │   │   ├── study-plan.ts
│   │   │   └── chat.ts
│   │   ├── controllers/
│   │   ├── services/
│   │   │   ├── openai.service.ts
│   │   │   └── database.service.ts
│   │   ├── models/
│   │   └── middleware/
│   └── prisma/
│       └── schema.prisma
│
└── shared/                           # 공통 코드
    └── types/
```

#### Option 2: 노코드 툴 활용

```
nocode-implementation/
├── NOCODE_STRATEGY.md                # 노코드 툴 선택 이유 및 전략
├── BUBBLE_GUIDE.md                   # Bubble.io 사용 가이드
├── ADALO_GUIDE.md                    # Adalo 사용 가이드
├── screenshots/                      # 노코드 툴 구현 스크린샷
│   ├── workflow-1.png
│   ├── workflow-2.png
│   └── database-structure.png
├── exported-configs/                 # 노코드 툴 설정 파일
│   ├── workflows.json
│   └── database-schema.json
└── DEMO_LINK.md                      # 라이브 데모 링크
```

### 4. 테스트 및 검증

```
tests/
├── unit/                             # 단위 테스트
├── integration/                      # 통합 테스트
├── e2e/                             # E2E 테스트
└── TEST_RESULTS.md                   # 테스트 결과 보고서
```

### 5. 배포 및 DevOps

```
deployment/
├── docker-compose.yml                # Docker 설정
├── Dockerfile
├── .github/
│   └── workflows/
│       └── ci-cd.yml                # GitHub Actions
└── DEPLOYMENT_GUIDE.md              # 배포 가이드
```

### 6. 데모 및 프레젠테이션

```
demo/
├── PITCH_DECK.pdf                   # 피칭 자료
├── DEMO_SCRIPT.md                   # 데모 시연 스크립트
├── VIDEO_DEMO.md                    # 데모 영상 링크
└── screenshots/                      # MVP 스크린샷
    ├── feature-1.png
    ├── feature-2.png
    └── feature-3.png
```

---

## 🎯 Study Quest MVP 최소 구현 범위

### Must Have 기능 (본선 시연 필수)

1. **온보딩 플로우** (5단계)
   - 기본 정보 입력
   - 현재 성적 입력
   - 목표 설정
   - AI 캐릭터 선택

2. **AI 목표 분해**
   - 목표 입력 → AI가 일일 퀘스트 생성
   - GPT-4o API 통합 (또는 Mock 데이터)

3. **홈 화면 - 일일 퀘스트**
   - 오늘의 퀘스트 3개 표시
   - 체크박스 완료 기능
   - 진도율 표시

4. **AI 캐릭터 대화**
   - 간단한 채팅 UI
   - AI 응답 (GPT-4o 또는 미리 정의된 응답)

5. **인증**
   - 간단한 로그인/회원가입
   - 또는 Guest 모드

### Nice to Have (시간 여유 있으면)

- 푸시 알림
- 진도 추적 차트
- 프로필 관리

---

## 📁 최종 GitHub 저장소 구조 (권장)

```
HACK-SeSAC/
├── README.md                         # ⭐ 가장 중요! 프로젝트 소개
├── docs/                            # 📄 모든 문서
│   ├── PROJECT_OVERVIEW.md
│   ├── PRD.md
│   ├── ARCHITECTURE.md
│   ├── API_SPECIFICATION.md
│   ├── DATABASE_SCHEMA.md
│   └── AI_STRATEGY.md
│
├── design/                          # 🎨 디자인 산출물
│   ├── wireframes/
│   └── user-flow.md
│
├── src/                             # 💻 실제 코드 (Option 1)
│   ├── frontend/
│   ├── backend/
│   └── shared/
│
├── nocode-implementation/           # 🚀 노코드 구현 (Option 2)
│   ├── NOCODE_STRATEGY.md
│   ├── screenshots/
│   └── DEMO_LINK.md
│
├── tests/                           # ✅ 테스트
│   └── TEST_RESULTS.md
│
├── deployment/                      # 🚢 배포 설정
│   ├── docker-compose.yml
│   └── DEPLOYMENT_GUIDE.md
│
├── demo/                            # 🎬 데모 자료
│   ├── PITCH_DECK.pdf
│   ├── DEMO_SCRIPT.md
│   └── screenshots/
│
└── .gitignore                       # Git 무시 파일
```

---

## 🚀 개발 전략 (예선 → 본선)

### 예선 단계 (현재 ~ 본선 전)

**목표**: 개발 현황 확인 → 문서 중심

**업로드 우선순위**:
1. ⭐⭐⭐ **README.md** (필수!)
   - 프로젝트 소개
   - 팀 소개
   - 기술 스택
   - MVP 범위
   - 진행 현황

2. ⭐⭐⭐ **docs/** 폴더
   - PRD (제품 요구사항)
   - 아키텍처 설계
   - API 명세서
   - 데이터베이스 스키마

3. ⭐⭐ **design/** 폴더
   - 와이어프레임
   - 사용자 플로우

4. ⭐ **src/** 또는 **nocode-implementation/**
   - 초기 개발 코드 (있는 만큼)
   - 노코드 구현 스크린샷

**예선 평가 포인트**:
- 문서 완성도 (얼마나 구체적인가?)
- 실현 가능성 (기술적으로 가능한가?)
- 진행 상황 (어디까지 했는가?)

---

### 본선 단계 (본선 당일)

**목표**: MVP 시연 → 동작하는 프로덕트

**필수 준비물**:
1. ⭐⭐⭐ **동작하는 MVP**
   - 실제 앱 (모바일 or 웹)
   - 또는 노코드 프로토타입

2. ⭐⭐⭐ **데모 스크립트**
   - 5분 시연 시나리오
   - 핵심 기능 위주

3. ⭐⭐ **피칭 자료**
   - 문제 정의
   - 솔루션
   - 기술 구현
   - 향후 계획

**본선 시연 시나리오 (5분)**:
```
1. 문제 제시 (30초)
   "재수생들은 막연한 목표 때문에 좌절합니다"

2. 솔루션 소개 (30초)
   "Study Quest는 AI가 목표를 일일 퀘스트로 분해합니다"

3. MVP 시연 (3분)
   - 온보딩: "수학 70점 → 90점" 입력
   - AI 자동 분해: Phase별 계획 생성
   - 홈 화면: 오늘의 퀘스트 3개
   - AI 캐릭터: 간단한 대화
   - 진도 추적: 완료율 확인

4. 기술 스택 및 향후 계획 (1분)
   - 기술: React Native + GPT-4o
   - 향후: 슬럼프 감지, 학원 B2B
```

---

## 🛠️ 빠른 MVP 구현 전략

### 전략 1: 노코드 툴 활용 (추천! ⚡ 빠름)

**장점**:
- ✅ 빠른 개발 (1주일 내 MVP 가능)
- ✅ 디자인 자동 생성
- ✅ 즉시 배포 가능

**추천 툴**:
1. **Bubble.io** (웹앱)
   - AI API 통합 쉬움
   - 데이터베이스 자동 생성
   - 무료 플랜으로 데모 가능

2. **Adalo** (모바일 앱)
   - 네이티브 앱 느낌
   - Drag & Drop UI
   - AI API 연동 가능

3. **Glide** (모바일 웹앱)
   - Google Sheets 기반
   - 가장 빠른 프로토타이핑
   - AI 통합 간단

**구현 범위**:
- ✅ 온보딩 5단계
- ✅ AI 목표 분해 (OpenAI API 연동)
- ✅ 홈 화면 + 퀘스트
- ✅ 간단한 채팅 UI

**필요 문서**:
```
nocode-implementation/
├── NOCODE_STRATEGY.md
│   - 왜 노코드를 선택했는가?
│   - 어떤 툴을 사용했는가?
│   - 실제 개발 대비 제약사항은?
│
├── IMPLEMENTATION_GUIDE.md
│   - 단계별 구현 가이드
│   - API 연동 방법
│   - 데이터베이스 구조
│
├── screenshots/
│   - 각 화면 스크린샷
│   - Workflow 캡처
│
└── DEMO_LINK.md
    - 라이브 데모 URL
    - 테스트 계정 정보
```

---

### 전략 2: 하이브리드 (노코드 + 일부 코드)

**구성**:
- **프론트엔드**: Bubble.io 또는 Webflow
- **백엔드 API**: Supabase (무료) 또는 Firebase
- **AI 부분**: 간단한 Node.js 서버 (Vercel 배포)

**장점**:
- ✅ 빠른 UI 개발
- ✅ AI 기능은 직접 제어 가능
- ✅ 실제 개발로 확장 용이

---

### 전략 3: 풀스택 개발 (시간 충분할 때)

**프론트엔드**:
- React Native (Expo) - 모바일
- 또는 Next.js - 웹

**백엔드**:
- Supabase (무료, PostgreSQL)
- 또는 Firebase (무료 티어)

**AI**:
- OpenAI GPT-4o API
- 또는 Claude 3.5 Sonnet

**배포**:
- Frontend: Vercel 또는 Netlify (무료)
- Backend: Vercel Serverless Functions (무료)

---

## ✅ 체크리스트

### 예선 제출 전 (문서 중심)

- [ ] README.md 작성 완료
- [ ] docs/ 폴더 전체 문서 완성
  - [ ] PROJECT_OVERVIEW.md
  - [ ] PRD.md
  - [ ] ARCHITECTURE.md
  - [ ] API_SPECIFICATION.md
  - [ ] DATABASE_SCHEMA.md
  - [ ] AI_STRATEGY.md
- [ ] design/ 폴더 와이어프레임 업로드
- [ ] 초기 코드 또는 노코드 스크린샷 업로드
- [ ] .gitignore 설정
- [ ] GitHub 저장소 Public 설정

### 본선 시연 전 (MVP 중심)

- [ ] MVP 동작 확인 (5가지 핵심 기능)
  - [ ] 온보딩 플로우
  - [ ] AI 목표 분해
  - [ ] 홈 화면 + 퀘스트
  - [ ] AI 캐릭터 대화
  - [ ] 인증 (또는 Guest 모드)
- [ ] 데모 스크립트 작성
- [ ] 피칭 자료 (PDF) 준비
- [ ] 데모 영상 촬영 (백업용)
- [ ] 라이브 데모 URL 또는 APK 파일 준비
- [ ] GitHub 저장소 최종 업데이트

---

## 💡 핵심 조언

### 예선 통과 포인트
1. **명확한 문제 정의**: 재수생 Pain Point 구체적으로
2. **차별화된 솔루션**: AI 자동 목표 분해 + 3종 캐릭터
3. **실현 가능성**: 기술 스택 명확, 아키텍처 구체적
4. **문서 완성도**: 읽는 사람이 이해하기 쉽게

### 본선 시연 포인트
1. **동작하는 것**: 화려하지 않아도 되니 **반드시 작동**해야 함
2. **핵심 기능 위주**: 5분 내 핵심 가치 전달
3. **스토리텔링**: 사용자 관점의 시나리오
4. **기술력 어필**: AI 통합, 데이터 기반 의사결정

---

**작성일**: 2025-11-17
**다음 업데이트**: 예선 결과 발표 후
