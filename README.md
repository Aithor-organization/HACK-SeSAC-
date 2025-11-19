# 📚 Co-Plan - AI 기반 N수생 학습 관리 플랫폼

> **"막연한 목표를 오늘 할 수 있는 퀘스트로"**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React Native](https://img.shields.io/badge/React_Native-0.72-blue.svg)](https://reactnative.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-green.svg)](https://nodejs.org/)
[![Claude](https://img.shields.io/badge/Claude-Sonnet_4.5-purple.svg)](https://www.anthropic.com/)

---

## 🎯 프로젝트 개요

**Co-Plan**은 N수생의 장기 목표인 대학 합격이라는 목표를 AI와의 대화를 통해 SMART 원칙에 따라 실행 가능한 일일 퀘스트로 자동 분해하고, 사용자의 학습 패턴을 학습한 AI 캐릭터 동반자가 개인 맞춤형 동기 부여, 일정 조정, 피드백, 코칭을 제공하는 **목표 달성 학습 플랫폼**입니다.

### 핵심 가치

- ✅ **AI 대화형 SMART 목표 설정**: AI와 대화하며 막연한 목표를 구체적(Specific), 측정가능(Measurable), 달성가능(Achievable), 현실적(Realistic), 시간제한(Time-bound) 일일 퀘스트로 최적화
- ✅ **학습하는 AI 캐릭터**: 사용자의 학습 패턴, 선호도, 성취도를 지속적으로 학습하여 점점 더 정교한 동기부여와 일정 조정 제공
- ✅ **N수생 특화 통합 솔루션**: 계획 수립뿐만 아니라 N수생 특유의 불안과 슬럼프에 대한 지속적인 동기부여와 코칭 제공

---

## 🚀 주요 기능 (MVP)

### 1. 사용자 온보딩 및 목표 설정 (5단계)

- 기본 정보 입력 (이름, 학년)
- 현재 성적 입력 (과목별)
- 목표 점수 및 대학 설정
- 수능 D-Day 자동 계산
- AI 캐릭터 선택 (3종)
- **온보딩 완료 후 AI와 대화하며 약 180개 일일 퀘스트 최적화 생성**

### 2. AI 대화형 SMART 목표 자동 분해 ⭐ **핵심 차별화**

**SMART 원칙 적용 예시**

사용자 입력: "수학 70점 → 90점"

**AI 대화 과정**:
```
AI: "현재 어떤 단원이 가장 약한가요?"
사용자: "함수랑 미적분이요"
AI: "하루에 몇 시간 공부 가능하세요?"
사용자: "4시간 정도요"
```

**AI 최적화 결과**:
- ✅ **Specific (구체적)**: 수학I 함수 개념 정리 + 기출 10문제
- ✅ **Measurable (측정 가능)**: 정답률 80% 이상
- ✅ **Achievable (달성 가능)**: 40분 소요
- ✅ **Realistic (현실적)**: 하루 학습 시간 4시간 중 40분 배분
- ✅ **Time-bound (기한 명확)**: 오늘 오후 2시~2시 40분

**Phase별 로드맵 자동 구성**:
- **Phase 1 (개념)**: 1-3개월, 기본 개념 정리
- **Phase 2 (유형)**: 4-6개월, 문제 유형별 훈련
- **Phase 3 (실전)**: 7-8개월, 실전 모의고사

### 3. 학습하는 AI 캐릭터 동반자 (3종)

**초기 (1-4주)**: 일반적 응원 및 격려
**중기 (4-12주)**: 학습 패턴 분석 기반 맞춤 조언
**후기 (12주+)**: 선제적 슬럼프 감지 및 자동 개입

**패턴 학습 항목**:
- 선호 학습 시간대 (오전/오후/저녁)
- 집중 가능 시간 (30분/60분/90분)
- 과목별 학습 속도
- 휴식 주기 및 패턴

**캐릭터 유형**:
- **캐릭터 A**: 엄근진 멘토형 (30대 입시 컨설턴트, 데이터 기반 조언)
- **캐릭터 B**: 공감 친구형 (20대 재수 성공 선배, 공감 능력)
- **캐릭터 C**: 하이브리드형 (25세 대학생 멘토, 친근+단호)

### 4. 일일 퀘스트 제공 및 진도 추적

- 오늘의 퀘스트 3-5개 표시
- 체크박스로 즉시 완료 표시
- 일일/주간/전체 진도율 시각화
- 퀘스트 완료 시 애니메이션, 사운드, AI 칭찬

### 5. 푸시 알림
- 매일 오전 8시: "오늘의 퀘스트 확인하기"
- 오후 9시: "오늘 진도 체크하기"
- 3일 미접속 시: "힘들어도 괜찮아요. 다시 시작해요!"
- 주간 리포트: 성취감 제공

### 6. 사용자 인증
- 이메일 + 비밀번호
- 소셜 로그인 (구글, 애플, 카카오)
- Guest 모드 지원 (MVP)
- 여러 기기 동기화

---

## 💡 문제 정의

### N수생들의 Pain Points

1. **계획 수립의 막막함**: "수능까지 8개월, 뭘 어떻게 해야 할지 막막해요"
2. **동기 부여의 한계**: "N수 기간 중 불안, 슬럼프, 외로움"
3. **중도 포기 위험**: "처음엔 의지가 강했는데 3개월 지나니 슬럼프가 와요" (중도 포기율 20-30%)
4. **비싼 학원비**: "학원 플래너 월 250만원은 부담스러워요"

### 기존 솔루션의 한계

| 기존 솔루션 | 한계점 |
|-----------|--------|
| **학원 플래너** | 월 250만원 고비용, 획일화된 커리큘럼 |
| **독학 플래너** | 수기 작성 부담 1-2시간, SMART 목표 분해 어려움 |
| **유료 앱** | 단순 타이머/기록만, AI 부재, 멘탈 케어 기능 없음 |
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
- **Database**: Firebase (사용자 데이터, 학습 패턴)
- **Authentication**: JWT (Access + Refresh Token)
- **Validation**: Zod

### AI Integration
- **Claude Sonnet 4.5 API** (Anthropic): SMART 목표 최적화 + AI 캐릭터
- **RAGFlow**: 수능 기출 데이터 검색 및 활용
  - 과목별 출제 빈도 데이터 (2020-2024)
  - 등급별 필수 단원 매핑
  - 단원별 평균 학습 소요 시간
  - N수생 성공 사례 데이터
- **Prompt Engineering**: N수생 특화 System Prompt
- **Caching**: Redis (비용 최적화)

### DevOps & Hosting
- **Cloud**: AWS (EC2 + S3)
- **Database**: Firebase Realtime Database / Firestore
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
│ (Node.js)    │  │ (Claude 4.5)│  │   (JWT)     │
└───────┬──────┘  └──────┬──────┘  └────┬────────┘
        │                │               │
        │         ┌──────▼──────┐        │
        │         │  RAGFlow    │        │
        │         │ (수능 데이터) │        │
        │         └──────┬──────┘        │
        │                │               │
        └────────────────┼───────────────┘
                         │
            ┌────────────▼────────────┐
            │  Firebase Database      │
            │  (User Data & Patterns) │
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
- Firebase 프로젝트 설정
- Claude API Key (Anthropic)
- RAGFlow 설치 및 설정

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
# - FIREBASE_CONFIG
# - CLAUDE_API_KEY
# - JWT_SECRET
# - RAGFLOW_API_ENDPOINT
```

#### 3. 백엔드 실행
```bash
cd src/backend
npm install
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
- [x] AI 프롬프트 엔지니어링 (Claude Sonnet 4.5)
- [x] RAGFlow 수능 데이터 시스템 설계

### 진행 중 🔄
- [ ] React Native 프론트엔드 개발 (60%)
- [ ] Node.js 백엔드 API 개발 (70%)
- [ ] Claude API 통합 (80%)
- [ ] RAGFlow 연동 (50%)
- [ ] Firebase 데이터베이스 구축 (100%)

### 예정 ⏳
- [ ] 학습 패턴 분석 시스템
- [ ] E2E 테스트 작성
- [ ] AWS 배포 (EC2 + Firebase)
- [ ] 푸시 알림 시스템 구축
- [ ] 베타 테스트 (100명)

---

## 📈 향후 계획

### Phase 1: MVP 출시 (2026년 4월)
- 베타 테스터 100명 모집
- 핵심 기능 6개 완성
- iOS/Android 동시 출시
- 4주 개발 완료

### Phase 2: 기능 확장 (2026년 5월 - 10월)
- 선제적 슬럼프 감지 및 자동 개입 고도화
- 모의고사 연동 및 취약점 자동 분석
- 주간/월간 학습 리포트 AI 생성
- 학습 데이터 18만 건 축적

### Phase 3: 시장 확장 (2026년 11월 - 2027년 4월)
- 고3 시장 진출 (50만명)
- B2B 중소형 학원 라이선스 프로그램
- 자격증/공무원 수험생 확장
- MAU 10,000명 달성

---

## 💰 비즈니스 모델

### 시장 규모
- **1차 타겟**: N수생 18만명
- **2차 타겟**: 고3 수험생 50만명
- **3차 확장**: 자격증/공무원 수험생

### 매출 추정
- N수생 10% 전환 (1.8만명) × 월 14,900원 × 12개월 = **약 32.2억원**
- 학원비(월 250만원) 대비 **1/167 가격**으로 접근성 향상

### 수익 모델
- 프리미엄 구독 (월 14,900원)
- B2B 학원 라이선스
- 기업 연수 프로그램

---

## 🎯 핵심 차별화 요소

### 1. AI 대화형 SMART 목표 설정 시스템
- **대화형 목표 최적화**: AI가 사용자와 대화하며 막연한 목표를 구체적인 SMART 일일 퀘스트로 변환
- **목표별 전체 로드맵**: Phase 1 (개념), Phase 2 (유형), Phase 3 (실전)로 체계화
- **데이터 기반**: 실제 수능 출제 빈도 데이터를 RAGFlow로 활용하여 신뢰도 향상
- **시간 단축**: 기존 1-2시간 계획 수립 → AI 대화 몇 분으로 단축

### 2. 학습하는 AI 캐릭터 시스템
- **패턴 학습**: 선호 학습 시간대, 집중 가능 시간, 과목별 속도, 휴식 주기 분석
- **진화형 코칭**: 초기에는 일반적 응원, 4주 후에는 데이터 기반 맞춤 조언 제공
- **선제적 개입**: 슬럼프 징후 조기 감지 및 자동 목표 조정

### 3. N수생 특화 통합 솔루션
- **계획 수립**: 학원 플래너(월 250만원) 대비 AI 대화형 자동 생성
- **동기부여&코칭**: AI 캐릭터 24/7 무제한 대화로 지속적인 동기 부여
- **중도 포기 방지**: N수생 중도 포기율 20-30%를 AI 선제적 개입으로 개선

---

## 📅 사용자 여정 예시

### 2025년 12월: 앱 설치 (5분 소요)
- 온보딩 5단계 완료 → AI와 대화하며 약 180개 퀘스트 최적화
- 오늘의 첫 퀘스트 3개 확인 후 즉시 학습 시작 가능

### 2026년 1월 (4주차): 학습 데이터 축적
- AI가 학습 시간대, 집중 시간, 과목별 속도 패턴 파악
- 맞춤 조언: "오전에 수학, 저녁에 영어" 자동 일정 조정

### 2026년 3월 (12주차): 슬럼프 감지 및 개입
- 진도율 하락 패턴 감지 → AI가 선제적으로 목표 조정 제안
- "이번 주 목표 60%로 낮추고 쉬운 문제만" 자신감 회복 유도

### 2026년 11월: 수능 D-Day
- 12개월간의 학습 데이터 분석, 168개 퀘스트 완료 (완료율 93%)
- 목표 달성: 수학 65점 → 88점 향상

---

## 👥 팀 소개

| 역할 | 이름 | 담당 |
|------|------|------|
| **Team Leader & PM** | 서현 | 기획/PM 총괄, 사업 기획 및 시장 분석, UX/UI 설계 및 사용자 시나리오 작성 |
| **Full-stack Developer** | 서훈 | 풀스택 개발 총괄, 백엔드 API, AI 통합, RAGFlow (다수의 AI 서비스 개발 경험 보유) |

---

## 🎓 기대효과

### 사회적 효과
- **N수생 접근성 향상**: 학원비(월 250만원) 대비 1/167 가격으로 18만 N수생에게 양질의 학습 지원
- **중도 포기율 감소**: AI 선제적 슬럼프 감지로 N수생 20-30% 중도 포기율 개선
- **지속적 동기부여 대중화**: 24/7 AI 동기부여 및 코칭으로 N수생의 정서적 안정 지원
- **교육 격차 해소**: 지역, 경제적 여건 관계없이 데이터 기반 학습 계획 접근

### 기술적 효과
- **교육 AI 혁신**: SMART 원칙 기반 AI 대화형 최적화로 에듀테크 새로운 기준 제시
- **학습 데이터 축적**: 18만 N수생의 학습 패턴 데이터로 AI 모델 고도화
- **RAG 활용 사례**: 실제 수능 데이터 기반 학습 계획 생성으로 신뢰도 검증

---

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

## 🙏 감사의 말

이 프로젝트는 N수생들의 목표 달성을 돕기 위해 시작되었습니다.
여러분의 피드백과 기여를 환영합니다!

**⭐ 이 프로젝트가 마음에 드신다면 Star를 눌러주세요!**

---

**Last Updated**: 2025-11-19
**Version**: MVP 1.0
**Status**: 🚧 In Development (2025 새싹 해커톤 진행 중)
**Team**: 에이아이터 (서현, 서훈)
