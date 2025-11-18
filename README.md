# 📚 Study Quest - AI 기반 재수생 학습 관리 플랫폼

> **"막연한 목표를 오늘 할 수 있는 퀘스트로"**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React Native](https://img.shields.io/badge/React_Native-0.72-blue.svg)](https://reactnative.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-green.svg)](https://nodejs.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-purple.svg)](https://openai.com/)

---

## 🎯 프로젝트 개요

**Study Quest**는 재수생/N수생의 막연한 학습 목표를 AI가 자동으로 실행 가능한 일일 퀘스트로 분해하고, 다양한 성격의 AI 캐릭터 동반자가 계획 수립부터 멘탈 관리까지 제공하는 **목표 달성 학습 플랫폼**입니다.

### 핵심 가치

- ✅ **AI 자동 목표 분해**: 업계 최초, 장기 목표를 일일 실행 가능한 퀘스트로 자동 변환
- ✅ **재수생 특화 AI 캐릭터 3종**: 멘토형/친구형/하이브리드형 선택 가능
- ✅ **계획 + 멘탈 관리 통합**: 학습 계획과 심리적 지원을 하나의 플랫폼에서

---

## 🚀 주요 기능 (MVP)

### 1. 사용자 온보딩 (5단계)
<img src="docs/images/onboarding-flow.png" alt="온보딩 플로우" width="800">

- 기본 정보 입력 (이름, 학년)
- 현재 성적 입력 (과목별)
- 목표 점수 및 대학 설정
- 수능 D-Day 자동 계산
- AI 캐릭터 선택 (3종)

### 2. AI 기반 자동 목표 분해 ⭐ **핵심 차별화**
<img src="docs/images/ai-goal-decomposition.png" alt="AI 목표 분해" width="800">

**입력**: "수학 70점 → 90점"
**AI 자동 분해**:
- Phase별 학습 계획 (1-3개월 / 4-6개월 / 7-8개월)
- 일일 퀘스트 자동 생성 (예: "수학I 함수 문제 10개, 120분")
- 응답 시간: 5초 이내

### 3. 일일 퀘스트 제공 및 진도 추적
<img src="docs/images/home-screen.png" alt="홈 화면" width="400">

- 오늘의 퀘스트 3-5개 표시
- 체크박스로 즉시 완료 표시
- 일일/주간/전체 진도율 시각화

### 4. AI 캐릭터 동반자 (3종)
<img src="docs/images/ai-characters.png" alt="AI 캐릭터" width="800">

- **캐릭터 A**: 엄근진 멘토형 (30대 입시 컨설턴트, 데이터 기반 조언)
- **캐릭터 B**: 공감 친구형 (20대 재수 성공 선배, 공감 능력)
- **캐릭터 C**: 하이브리드형 (25세 대학생 멘토, 친근+단호)

### 5. 푸시 알림
- 매일 오전 8시: "오늘의 퀘스트 확인하기"
- 오후 9시: "오늘 진도 체크하기"
- 3일 미접속 시: "힘들어도 괜찮아요. 다시 시작해요!"

### 6. 사용자 인증
- 이메일 + 비밀번호
- 소셜 로그인 (구글, 애플, 카카오)
- Guest 모드 지원 (MVP)

---

## 💡 문제 정의

### 재수생들의 Pain Points

1. **계획 수립의 어려움**: "수능까지 8개월, 뭘 어떻게 해야 할지 막막해요"
2. **중도 포기 위험**: "처음엔 의지가 강했는데 3개월 지나니 슬럼프가 와요"
3. **멘탈 관리 한계**: "혼자 공부하다 보니 우울하고 불안해요"
4. **비싼 학원비**: "학원비 월 250만원은 부담스러워요"

### 기존 솔루션의 한계

| 기존 솔루션 | 한계점 |
|-----------|--------|
| **학원** | 월 250만원 고비용, 획일화된 커리큘럼 |
| **독학 플래너** | 수기 작성 부담, 목표 분해 어려움 |
| **유료 앱** | 단순 타이머/기록만, AI 부재 |
| **유튜브 강의** | 산발적 학습, 체계성 부족 |

---

## 🎨 기술 스택

### Frontend (모바일)
- **React Native** 0.72 + TypeScript
- **Navigation**: React Navigation
- **State Management**: Zustand
- **UI Library**: React Native Paper
- **Charts**: react-native-chart-kit

### Backend (API)
- **Node.js** 18.x + Express + TypeScript
- **Database**: PostgreSQL (AWS RDS)
- **ORM**: Prisma
- **Authentication**: JWT (Access + Refresh Token)
- **Validation**: Zod

### AI Integration
- **OpenAI GPT-4o API**: 목표 분해 + AI 캐릭터
- **Prompt Engineering**: 재수생 특화 System Prompt
- **Caching**: Redis (비용 최적화)

### DevOps & Hosting
- **Cloud**: AWS (EC2 + RDS + S3)
- **CI/CD**: GitHub Actions
- **Monitoring**: AWS CloudWatch
- **Push Notifications**: Firebase Cloud Messaging (FCM) + APNs

---

## 📐 시스템 아키텍처

```
┌─────────────────────────────────────────────────────────┐
│                     Client Layer                        │
│  ┌──────────────────┐      ┌──────────────────┐        │
│  │  iOS App         │      │  Android App     │        │
│  │  (React Native)  │      │  (React Native)  │        │
│  └────────┬─────────┘      └────────┬─────────┘        │
│           │                         │                   │
└───────────┼─────────────────────────┼───────────────────┘
            │                         │
            └────────────┬────────────┘
                         │ HTTPS/REST API
            ┌────────────▼────────────┐
            │    API Gateway (AWS)    │
            └────────────┬────────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
┌───────▼──────┐  ┌──────▼──────┐  ┌────▼────────┐
│ Express API  │  │  AI Service │  │ Auth Service│
│ (Node.js)    │  │  (GPT-4o)   │  │   (JWT)     │
└───────┬──────┘  └──────┬──────┘  └────┬────────┘
        │                │               │
        └────────────────┼───────────────┘
                         │
            ┌────────────▼────────────┐
            │  PostgreSQL Database    │
            │       (AWS RDS)         │
            └─────────────────────────┘
```

자세한 아키텍처는 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) 참조

---

## 🗂️ 프로젝트 구조

```
HACK-SeSAC/
├── docs/                          # 📄 프로젝트 문서
│   ├── PROJECT_OVERVIEW.md       # 프로젝트 개요
│   ├── PRD.md                    # 제품 요구사항 명세서
│   ├── ARCHITECTURE.md           # 시스템 아키텍처
│   ├── API_SPECIFICATION.md      # API 명세서
│   ├── DATABASE_SCHEMA.md        # 데이터베이스 설계
│   └── AI_STRATEGY.md            # AI 데이터 및 모델 전략
│
├── design/                        # 🎨 디자인 산출물
│   ├── wireframes/               # 와이어프레임
│   └── user-flow.md              # 사용자 플로우
│
├── src/                          # 💻 소스 코드
│   ├── frontend/                 # React Native 앱
│   ├── backend/                  # Node.js API
│   └── shared/                   # 공통 코드
│
├── tests/                        # ✅ 테스트
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── deployment/                   # 🚢 배포 설정
│   ├── docker-compose.yml
│   └── DEPLOYMENT_GUIDE.md
│
└── demo/                         # 🎬 데모 자료
    ├── PITCH_DECK.pdf
    ├── DEMO_SCRIPT.md
    └── screenshots/
```

---

## 🚀 시작하기

### 사전 요구사항

- Node.js 18.x 이상
- React Native CLI
- PostgreSQL 13 이상
- OpenAI API Key

### 설치 및 실행

#### 1. 저장소 클론
```bash
git clone https://github.com/Aithor-organization/HACK-SeSAC-.git
cd HACK-SeSAC-
```

#### 2. 환경 변수 설정
```bash
# Backend 환경 변수
cp src/backend/.env.example src/backend/.env
# .env 파일에 다음 설정:
# - DATABASE_URL
# - OPENAI_API_KEY
# - JWT_SECRET
```

#### 3. 백엔드 실행
```bash
cd src/backend
npm install
npx prisma migrate dev
npm run dev
# 서버 실행: http://localhost:3000
```

#### 4. 프론트엔드 실행
```bash
cd src/frontend
npm install

# iOS
npx react-native run-ios

# Android
npx react-native run-android
```

자세한 설치 가이드는 [deployment/DEPLOYMENT_GUIDE.md](deployment/DEPLOYMENT_GUIDE.md) 참조

---

## 📊 개발 현황

### 완료 항목 ✅
- [x] 프로젝트 기획 및 PRD 작성
- [x] 시스템 아키텍처 설계
- [x] 데이터베이스 스키마 설계
- [x] API 명세서 작성
- [x] 와이어프레임 디자인 (12개 화면)
- [x] AI 프롬프트 엔지니어링 (GPT-4o)

### 진행 중 🔄
- [ ] React Native 프론트엔드 개발 (60%)
- [ ] Node.js 백엔드 API 개발 (70%)
- [ ] OpenAI API 통합 (80%)
- [ ] 데이터베이스 마이그레이션 (100%)

### 예정 ⏳
- [ ] E2E 테스트 작성
- [ ] AWS 배포 (EC2 + RDS)
- [ ] 푸시 알림 시스템 구축
- [ ] 베타 테스트 (100명)

---

## 📈 향후 계획

### Phase 1: MVP 출시 (2026년 4월)
- 베타 테스터 100명 모집
- 핵심 기능 6개 완성
- iOS/Android 동시 출시

### Phase 2: 기능 확장 (2026년 5월 - 10월)
- 슬럼프 감지 및 자동 개입
- 모의고사 연동 및 취약점 분석
- 주간/월간 학습 리포트

### Phase 3: 시장 확장 (2026년 11월 - 2027년 4월)
- 고3 시장 진출
- B2B 학원 라이선스 프로그램
- MAU 10,000명 달성

---

## 👥 팀 소개

| 역할 | 이름 | GitHub | 담당 |
|------|------|--------|------|
| **Team Lead & Backend** | [이름] | [@github] | 백엔드 API, AI 통합 |
| **Frontend Developer** | [이름] | [@github] | React Native 앱 개발 |
| **UI/UX Designer** | [이름] | [@behance] | 디자인 시스템, 와이어프레임 |
| **Product Manager** | [이름] | [@linkedin] | 기획, 요구사항 정의 |

---

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

## 📞 연락처

- **이메일**: contact@studyquest.com
- **GitHub Issues**: [이슈 등록](https://github.com/Aithor-organization/HACK-SeSAC-/issues)
- **데모 영상**: [YouTube 링크]
- **피칭 자료**: [demo/PITCH_DECK.pdf](demo/PITCH_DECK.pdf)

---

## 🙏 감사의 말

이 프로젝트는 재수생/N수생들의 목표 달성을 돕기 위해 시작되었습니다.
여러분의 피드백과 기여를 환영합니다!

**⭐ 이 프로젝트가 마음에 드신다면 Star를 눌러주세요!**

---

**Last Updated**: 2025-11-17
**Version**: MVP 1.0
**Status**: 🚧 In Development (예선 진행 중)
