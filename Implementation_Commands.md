# Study Quest 프로젝트 설계 및 구현 명령어 가이드

**프로젝트명**: Study Quest
**버전**: 1.0
**작성일**: 2025-11-17
**목적**: MVP Must Have 기능 완전 구현

---

## 📋 목차

1. [프로젝트 준비 단계](#1-프로젝트-준비-단계)
2. [Constitution 작성 단계](#2-constitution-작성-단계)
3. [SPECIFY 단계 - 명세 작성](#3-specify-단계---명세-작성)
4. [PLAN 단계 - 계획 수립](#4-plan-단계---계획-수립)
5. [TASKS 단계 - 작업 분해](#5-tasks-단계---작업-분해)
6. [IMPLEMENT 단계 - 구현](#6-implement-단계---구현)
7. [검증 및 테스트](#7-검증-및-테스트)
8. [문서화 및 완료](#8-문서화-및-완료)

---

## 1. 프로젝트 준비 단계

### 1.1 Spec-Kit 프로젝트 초기화

```bash
# 프로젝트 디렉토리 생성
cd /Users/seohun/Documents/에이전트/infiniteAgent

# Spec-Kit 프로젝트 초기화
specify init study-quest --ai claude

# 프로젝트로 이동
cd study-quest

# Git 초기화 확인
git status
```

### 1.2 SuperClaude 세션 시작

```bash
# Claude Code 실행
claude

# SuperClaude 세션 로드
/sc:load
```

### 1.3 PRD 및 디자인 파일 복사

```bash
# PRD 파일 복사
cp /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md .specify/memory/

# 디자인 파일들 복사 (specdocsfile 폴더의 디자인 관련 파일)
mkdir -p .specify/memory/designs
cp /Users/seohun/Documents/에이전트/infiniteAgent/specdocsfile/*.md .specify/memory/designs/
```

---

## 2. Constitution 작성 단계

### 2.1 프로젝트 헌법 작성

```
/speckit.constitution

다음 내용을 기반으로 Study Quest 프로젝트의 헌법을 작성해주세요:

**프로젝트 비전**
재수생/N수생의 막연한 목표를 AI가 실행 가능한 일일 퀘스트로 자동 분해하고,
다양한 성격의 AI 캐릭터 동반자가 계획 수립부터 멘탈 관리까지 제공하는
목표 달성 학습 플랫폼

**핵심 원칙**
1. Complete Implementation: MVP라도 선택한 기능은 100% 완성
2. User-First Design: 재수생의 Pain Points 해결 우선
3. AI-Powered: GPT-4o 기반 자동 목표 분해 및 캐릭터 동반자
4. Mobile-First: React Native 기반 크로스플랫폼
5. Security & Privacy: 개인정보보호법 완전 준수

**기술 스택 원칙**
- Frontend: React Native + TypeScript + Tailwind CSS
- Backend: Node.js + Express + TypeScript
- Database: PostgreSQL (RDS)
- AI: OpenAI GPT-4o API
- Hosting: AWS (EC2 + RDS + S3)
- Testing: Jest + React Native Testing Library

**품질 기준**
- TypeScript strict mode 필수
- 테스트 커버리지 80% 이상
- API 응답 시간 500ms 이내 (95 percentile)
- AI 응답 시간 3초 이내
- 앱 크래시율 0.5% 이하

**금지사항**
- TODO 코멘트로 구현 미루기
- Mock 데이터로 기능 대체
- 테스트 없는 코드 커밋
- 명세 없는 기능 추가
```

### 2.2 헌법 검토 및 확정

```
/sc:analyze .specify/memory/constitution.md --validate

헌법이 다음을 만족하는지 확인:
1. 프로젝트 비전이 명확한가?
2. 기술 스택이 구체적인가?
3. 품질 기준이 측정 가능한가?
4. 제약사항이 실행 가능한가?
```

---

## 3. SPECIFY 단계 - 명세 작성

### 3.1 Must Have 기능 명세 작성

각 Must Have 기능에 대해 개별 명세 작성:

#### F1: 사용자 온보딩 및 목표 설정

```
/speckit.specify

feature: 사용자 온보딩 및 목표 설정 (F1)
priority: P0 (Critical)
reference: /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md (F1 섹션)

다음 내용을 포함하여 명세를 작성해주세요:

**기능 개요**
- 5단계 온보딩 프로세스
- 현재 성적 및 목표 설정
- AI 캐릭터 선택 (3종)
- 온보딩 완료 시간 5분 이내

**User Story**
- As a 재수생
- I want to 앱 최초 실행 시 나의 현재 상태와 목표를 입력하고 싶다
- So that AI가 나에게 맞는 학습 계획을 만들어줄 수 있다

**Acceptance Criteria** (PRD F1 섹션 참조)
- 5단계 온보딩 완료 가능
- 온보딩 Skip 가능
- 모든 입력 항목 나중에 수정 가능
- 온보딩 이탈률 30% 이하

**UI/UX 요구사항**
- 디자인 파일 참조: .specify/memory/designs/ 폴더
- 온보딩 각 단계별 화면 디자인 존재
- 프로그레스 바 표시
- 뒤로가기 가능

**데이터 모델**
- User 테이블: 기본 정보, 학년
- UserGoal 테이블: 과목별 현재/목표 점수
- UserPreference 테이블: 선택한 AI 캐릭터
```

#### F2: AI 기반 자동 목표 분해

```
/speckit.specify

feature: AI 기반 자동 목표 분해 (F2)
priority: P0 (Critical) - 핵심 차별화 기능
reference: /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md (F2 섹션)

**기능 개요**
- 자연어 목표 입력 → AI 자동 분해
- Phase별 학습 계획 생성 (1-3개월/4-6개월/7-8개월)
- 일일 퀘스트 자동 생성
- 응답 시간 5초 이내

**AI 요구사항**
- 모델: GPT-4o API
- Prompt Engineering: 재수생 특화 커리큘럼 데이터 학습
- 정확도 목표: 90% 이상 (사용자 만족도 기준)

**Acceptance Criteria**
- 자연어 목표 입력 가능 (예: "수학 70점 → 90점")
- 5초 이내 계획 생성
- Phase별 + 일일 퀘스트 포함
- 계획 수정 가능 (난이도, 하루 학습시간)

**데이터 모델**
- StudyPlan 테이블: 전체 학습 계획
- Phase 테이블: 단계별 계획 (1-3개월 등)
- DailyQuest 테이블: 일일 퀘스트
- CurriculumData 테이블: AI 학습용 커리큘럼 데이터
```

#### F3: AI 캐릭터 동반자 (3종)

```
/speckit.specify

feature: AI 캐릭터 동반자 (F3)
priority: P0 (Critical)
reference: /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md (F3 섹션)

**기능 개요**
- 3종 AI 캐릭터: 엄근진 멘토형, 공감 친구형, 하이브리드형
- 텍스트 기반 대화
- 응답 속도 3초 이내
- 대화 히스토리 30일 유지

**캐릭터 정의**
- 캐릭터 A (엄근진 멘토형): 30대 입시 컨설턴트, 데이터 기반 조언
- 캐릭터 B (공감 친구형): 20대 재수 성공 선배, 공감 능력
- 캐릭터 C (하이브리드형): 25세 대학생 멘토, 친근+단호

**Acceptance Criteria**
- 3종 캐릭터 제공 및 언제든 변경 가능
- 텍스트 대화 지원 (응답 3초 이내)
- 대화 히스토리 최근 30일 유지
- 무료: 하루 10회 제한, 프리미엄: 무제한

**AI 요구사항**
- System Prompt 설계: 각 캐릭터별 페르소나
- 대화 컨텍스트 관리: 최근 10턴 유지
- 감정 분석: 슬럼프 징후 감지

**데이터 모델**
- AICharacter 테이블: 캐릭터 정의 및 System Prompt
- ChatHistory 테이블: 대화 히스토리
- UserCharacterPreference 테이블: 사용자 선택 캐릭터
```

#### F4: 일일 퀘스트 제공 및 진도 추적

```
/speckit.specify

feature: 일일 퀘스트 제공 및 진도 추적 (F4)
priority: P0 (Critical)
reference: /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md (F4 섹션)

**기능 개요**
- 홈 화면에 오늘의 퀘스트 3-5개 표시
- 체크박스로 완료 표시
- 진도율 시각화 (일일/주간/전체)

**Acceptance Criteria**
- 홈 화면에 오늘의 퀘스트 3-5개 표시
- 각 퀘스트 체크박스 완료 표시
- 완료 시 즉시 피드백 (애니메이션, 사운드)
- 진도율 차트 시각화 (막대/선 그래프)

**UI/UX 요구사항**
- 디자인 파일 참조: 홈 화면 디자인
- 퀘스트 완료 애니메이션
- 진도율 차트 (React Native Charts)

**데이터 모델**
- DailyQuest 테이블: 일일 퀘스트
- QuestCompletion 테이블: 완료 기록
- Progress 테이블: 진도율 통계
```

#### F5: 푸시 알림

```
/speckit.specify

feature: 푸시 알림 (F5)
priority: P0 (Critical)
reference: /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md (F5 섹션)

**기능 개요**
- 시간 기반 자동 알림
- 커스터마이징 가능한 알림 시간
- 알림 끄기 옵션

**Acceptance Criteria**
- 매일 오전 8시: "오늘의 퀘스트 확인하기"
- 오후 9시: "오늘 진도 체크하기"
- 3일 미접속 시: "힘들어도 괜찮아요. 다시 시작해요!"
- 알림 시간 커스터마이징 가능
- 알림 끄기 옵션 제공
- 알림 오픈율 30% 이상

**기술 요구사항**
- iOS: APNs
- Android: Firebase Cloud Messaging (FCM)
- 백엔드: 스케줄링 시스템 (node-cron)

**데이터 모델**
- NotificationSchedule 테이블: 알림 스케줄
- UserNotificationPreference 테이블: 사용자 알림 설정
- NotificationLog 테이블: 발송 로그
```

#### F6: 사용자 인증 및 프로필 관리

```
/speckit.specify

feature: 사용자 인증 및 프로필 관리 (F6)
priority: P0 (Critical)
reference: /Users/seohun/Documents/에이전트/infiniteAgent/files/Study_Quest_PRD.md (F6 섹션)

**기능 개요**
- 회원가입: 이메일 + 비밀번호, 소셜 로그인
- 프로필 관리: 목표 대학, 수능 D-Day
- 계정 삭제 기능 (GDPR 준수)

**Acceptance Criteria**
- 회원가입: 이메일 + 비밀번호, 소셜 로그인 (구글, 애플, 카카오)
- 이메일 인증 필수
- 비밀번호 정책: 최소 8자, 영문+숫자 조합
- 프로필 정보: 이름, 프로필 사진(선택), 목표 대학, 수능 D-Day
- 계정 삭제 기능 제공

**보안 요구사항**
- JWT 기반 인증
- 소셜 로그인: OAuth 2.0
- 비밀번호 암호화: bcrypt
- Access Token (15분), Refresh Token (7일)

**데이터 모델**
- User 테이블: 기본 정보, 인증 정보
- UserProfile 테이블: 프로필 정보
- RefreshToken 테이블: Refresh Token 관리
- SocialAccount 테이블: 소셜 로그인 연동
```

### 3.2 명세 명확화

각 명세에 대해 불명확한 부분 명확화:

```
/speckit.clarify

feature: F1 - 사용자 온보딩 및 목표 설정

다음 질문들에 답변해주세요:
1. 온보딩 Skip 시 기본값은?
2. 과목별 점수 입력 시 모든 과목 필수인가 선택인가?
3. AI 캐릭터 미선택 시 기본 캐릭터는?
4. 온보딩 중간에 앱 종료 시 재시작 위치는?
5. 프로필 사진 업로드 형식 및 크기 제한은?
```

(각 기능별로 반복)

---

## 4. PLAN 단계 - 계획 수립

### 4.1 시스템 아키텍처 설계

```
/sc:design --agent system-architect

Study Quest 프로젝트의 시스템 아키텍처를 설계해주세요.

**요구사항**
- React Native 모바일 앱 (iOS + Android)
- Node.js + Express 백엔드 API
- PostgreSQL 데이터베이스
- OpenAI GPT-4o API 통합
- AWS 호스팅 (EC2 + RDS + S3)

**고려사항**
- 확장성: 1년 차 MAU 10,000명 → 3년 차 100,000명
- 성능: API 응답 500ms 이내, AI 응답 3초 이내
- 보안: JWT 인증, HTTPS, 개인정보보호법 준수
- 비용: 1년 차 예산 2억원 내

다음을 포함한 아키텍처 설계를 제공해주세요:
1. 전체 시스템 아키텍처 다이어그램
2. 컴포넌트 구조 (Frontend + Backend)
3. 데이터베이스 ERD
4. API 설계 (RESTful)
5. AI 통합 아키텍처
6. 배포 전략 (CI/CD)
```

### 4.2 기술 스택 상세 계획

```
/sc:research --tavily

다음 기술 스택에 대한 최신 베스트 프랙티스를 조사해주세요:

1. React Native + TypeScript
   - 최신 버전 및 권장 라이브러리
   - Navigation: React Navigation vs Expo Router
   - State Management: Zustand vs Redux Toolkit
   - UI Library: React Native Paper vs NativeBase

2. Node.js + Express + TypeScript 백엔드
   - 최신 보안 패치 버전
   - ORM: Prisma vs TypeORM
   - Validation: Zod vs Joi
   - Testing: Jest + Supertest

3. PostgreSQL
   - RDS 최적 설정
   - 인덱싱 전략
   - 백업 및 복구 전략

4. OpenAI GPT-4o API
   - 최신 API 버전 및 가격
   - Rate Limiting 전략
   - Cost Optimization 방법
```

### 4.3 각 기능별 구현 계획 작성

```
/speckit.plan

feature: F1 - 사용자 온보딩 및 목표 설정

.specify/specs/001-onboarding/spec.md를 참조하여 구현 계획을 작성해주세요.

**기술적 접근**
- React Native: 5개 Screen 컴포넌트
- Navigation: Stack Navigator
- State: Zustand store
- Validation: Zod schema
- API: POST /api/onboarding

**컴포넌트 구조**
OnboardingFlow/
├── OnboardingScreen1.tsx  (기본 정보)
├── OnboardingScreen2.tsx  (현재 성적)
├── OnboardingScreen3.tsx  (목표 설정)
├── OnboardingScreen4.tsx  (수능 D-Day)
├── OnboardingScreen5.tsx  (AI 캐릭터 선택)
├── ProgressBar.tsx
└── SkipButton.tsx

**API 설계**
- POST /api/onboarding/start
- PUT /api/onboarding/step/:step
- POST /api/onboarding/complete
- GET /api/onboarding/status

**데이터베이스**
- User 테이블 DDL
- UserGoal 테이블 DDL
- UserPreference 테이블 DDL

**테스트 계획**
- Unit Tests: 컴포넌트별 테스트
- Integration Tests: API 엔드포인트 테스트
- E2E Tests: 전체 온보딩 플로우

**예상 작업량**
- 프론트엔드: 3일
- 백엔드: 2일
- 테스트: 1일
- 총: 6일
```

(F2, F3, F4, F5, F6에 대해 반복)

### 4.4 데이터베이스 스키마 설계

```
/sc:design --agent backend-architect

PostgreSQL 데이터베이스 스키마를 설계해주세요.

**요구사항**
- Must Have 기능 6개 지원
- 확장성: 100,000 사용자 대응
- 성능: 인덱싱 최적화
- GDPR 준수: 데이터 삭제 지원

**테이블 목록**
- users
- user_profiles
- user_goals
- user_preferences
- study_plans
- phases
- daily_quests
- quest_completions
- ai_characters
- chat_histories
- notification_schedules
- refresh_tokens

각 테이블에 대해 다음 제공:
1. DDL (CREATE TABLE)
2. 인덱스 정의
3. 외래키 제약조건
4. 샘플 데이터
```

---

## 5. TASKS 단계 - 작업 분해

### 5.1 전체 작업 분해

```
/speckit.tasks

.specify/specs/ 폴더의 모든 plan.md를 참조하여
실행 가능한 작업으로 분해해주세요.

**작업 분해 원칙**
- 각 작업은 1-2일 내 완료 가능
- 의존성 명확히 표시
- 우선순위 정의 (P0 > P1 > P2)
- 테스트 작업 포함

**작업 카테고리**
1. 환경 설정 및 초기 셋업
2. 백엔드 API 개발
3. 데이터베이스 마이그레이션
4. 프론트엔드 개발
5. AI 통합
6. 테스트 및 QA
7. 배포 및 DevOps
```

### 5.2 작업 우선순위 및 일정 수립

```
/sc:estimate

.specify/specs/001-onboarding/tasks.md의 각 작업에 대해
예상 공수를 산정해주세요.

**고려사항**
- 개발자 2명 (CTO + 기술고문)
- MVP 개발 기간: 2개월
- 각 개발자의 일일 생산성: 6시간
- 버퍼: 20% 추가

각 작업별로 다음 제공:
1. 예상 시간 (hours)
2. 담당자 (Frontend/Backend/Fullstack)
3. 의존성
4. 리스크 요인
```

---

## 6. IMPLEMENT 단계 - 구현

### 6.1 프로젝트 초기 셋업

```
/sc:implement

작업: 프로젝트 초기 셋업

다음을 구현해주세요:

1. React Native 프로젝트 생성
   - npx react-native init StudyQuest --template react-native-template-typescript
   - 디렉토리 구조 설정

2. Node.js + Express 백엔드 생성
   - Express + TypeScript 보일러플레이트
   - Prisma ORM 설정
   - 환경 변수 설정 (.env.example)

3. 데이터베이스 초기화
   - PostgreSQL 연결 설정
   - Prisma schema 정의
   - 마이그레이션 스크립트

4. CI/CD 파이프라인
   - GitHub Actions 워크플로우
   - 테스트 자동화
   - 배포 스크립트

5. 문서화
   - README.md
   - API 문서 (Swagger)
   - 개발 환경 설정 가이드
```

### 6.2 기능별 구현 (병렬 처리)

SuperClaude의 TodoWrite와 병렬 실행 활용:

```
TodoWrite 작성:
1. ⏳ F1 온보딩 프론트엔드 구현
2. ⏳ F1 온보딩 백엔드 API 구현
3. ⏳ F2 AI 목표 분해 프론트엔드 구현
4. ⏳ F2 AI 목표 분해 백엔드 + OpenAI 통합
5. ⏳ F3 AI 캐릭터 채팅 UI 구현
6. ⏳ F3 AI 캐릭터 백엔드 + OpenAI 통합
7. ⏳ F4 일일 퀘스트 홈 화면 구현
8. ⏳ F4 진도 추적 차트 구현
9. ⏳ F5 푸시 알림 시스템 구현
10. ⏳ F6 인증 시스템 구현
```

#### F1 온보딩 구현

```
/sc:implement --agent frontend-architect

작업: F1 온보딩 프론트엔드 구현

**참조**
- spec: .specify/specs/001-onboarding/spec.md
- plan: .specify/specs/001-onboarding/plan.md
- tasks: .specify/specs/001-onboarding/tasks.md
- 디자인: .specify/memory/designs/

**구현 내용**
1. 5개 온보딩 화면 컴포넌트
   - OnboardingScreen1: 기본 정보 입력
   - OnboardingScreen2: 현재 성적 입력
   - OnboardingScreen3: 목표 설정
   - OnboardingScreen4: 수능 D-Day
   - OnboardingScreen5: AI 캐릭터 선택

2. 공통 컴포넌트
   - ProgressBar: 진행 상태 표시
   - SkipButton: 건너뛰기 버튼
   - BackButton: 이전 단계로

3. 상태 관리
   - Zustand store: onboardingStore.ts
   - Validation: Zod schemas

4. Navigation
   - Stack Navigator 설정
   - 화면 전환 애니메이션

**품질 기준**
- TypeScript strict mode
- 모든 컴포넌트 테스트 작성
- 디자인 파일 100% 반영
- 접근성 (accessibility) 준수
```

```
/sc:implement --agent backend-architect

작업: F1 온보딩 백엔드 API 구현

**참조**
- spec: .specify/specs/001-onboarding/spec.md
- plan: .specify/specs/001-onboarding/plan.md

**구현 내용**
1. API 엔드포인트
   - POST /api/onboarding/start
   - PUT /api/onboarding/step/:step
   - POST /api/onboarding/complete
   - GET /api/onboarding/status

2. 데이터베이스
   - User 테이블
   - UserGoal 테이블
   - UserPreference 테이블
   - Prisma migration

3. Validation
   - Zod schemas
   - 입력 데이터 검증

4. 에러 핸들링
   - 표준 에러 응답
   - 로깅 (Winston)

**품질 기준**
- API 테스트 (Jest + Supertest)
- Swagger 문서 자동 생성
- 에러 처리 100% 커버
```

#### F2 AI 목표 분해 구현

```
/sc:implement --agent python-expert

작업: F2 AI 목표 분해 - OpenAI GPT-4o 통합

**참조**
- spec: .specify/specs/002-ai-goal-decomposition/spec.md
- plan: .specify/specs/002-ai-goal-decomposition/plan.md

**구현 내용**
1. OpenAI API 통합
   - GPT-4o API 클라이언트
   - Rate Limiting (10 req/min)
   - Cost Tracking

2. Prompt Engineering
   - System Prompt: 재수생 특화 커리큘럼 전문가
   - User Prompt Template
   - Few-shot Examples (재수생 실제 사례 5개)

3. 응답 파싱 및 검증
   - JSON 응답 파싱
   - Phase별 계획 추출
   - 일일 퀘스트 생성

4. 캐싱 및 최적화
   - Redis 캐싱 (동일 목표 입력)
   - 응답 시간 모니터링
   - Cost Optimization

**품질 기준**
- 응답 시간 5초 이내 (95 percentile)
- 정확도 90% 이상 (베타 테스터 평가)
- Cost: 사용자당 월 $3 이하
```

#### F3 AI 캐릭터 동반자 구현

```
/sc:implement --magic --agent frontend-architect

작업: F3 AI 캐릭터 채팅 UI 구현

**참조**
- spec: .specify/specs/003-ai-character/spec.md
- 디자인: .specify/memory/designs/ai-chat-screen.md

**구현 내용**
1. 채팅 UI 컴포넌트
   - ChatBubble: 메시지 버블
   - ChatInput: 입력창
   - CharacterAvatar: 캐릭터 아바타
   - TypingIndicator: 입력 중 표시

2. 캐릭터 선택 화면
   - 3종 캐릭터 카드
   - 캐릭터 설명 및 예시 대사
   - 선택 및 변경 기능

3. 대화 히스토리
   - 무한 스크롤
   - 날짜 구분선
   - 대화 검색

**MCP 통합**
- Magic MCP: UI 컴포넌트 자동 생성
- 디자인 시스템 일관성 유지
```

```
/sc:implement --agent backend-architect

작업: F3 AI 캐릭터 백엔드 구현

**참조**
- spec: .specify/specs/003-ai-character/spec.md

**구현 내용**
1. AI 캐릭터 System Prompts
   - 캐릭터 A: 엄근진 멘토형 페르소나
   - 캐릭터 B: 공감 친구형 페르소나
   - 캐릭터 C: 하이브리드형 페르소나

2. 대화 API
   - POST /api/chat/send
   - GET /api/chat/history
   - PUT /api/chat/character (캐릭터 변경)

3. 대화 컨텍스트 관리
   - 최근 10턴 유지
   - 감정 분석 (슬럼프 감지)
   - 대화 히스토리 30일 보관

4. 무료/프리미엄 제한
   - 하루 10회 제한 (무료)
   - Rate Limiting
```

#### F4 일일 퀘스트 및 진도 추적 구현

```
/sc:implement --agent frontend-architect

작업: F4 홈 화면 및 진도 추적 구현

**참조**
- spec: .specify/specs/004-daily-quest/spec.md
- 디자인: .specify/memory/designs/home-screen.md

**구현 내용**
1. 홈 화면
   - TodayQuestList: 오늘의 퀘스트 3-5개
   - ProgressCard: 진도율 카드
   - CompletionAnimation: 완료 애니메이션

2. 진도 추적 화면
   - ProgressChart: 차트 (react-native-chart-kit)
   - WeeklyProgress: 주간 진도율
   - OverallProgress: 전체 진도율

3. 퀘스트 완료 처리
   - 체크박스 토글
   - 즉시 피드백 (애니메이션 + 사운드)
   - 진도율 자동 업데이트

**라이브러리**
- react-native-chart-kit: 차트
- react-native-sound: 사운드
- react-native-reanimated: 애니메이션
```

#### F5 푸시 알림 구현

```
/sc:implement --agent devops-engineer

작업: F5 푸시 알림 시스템 구현

**참조**
- spec: .specify/specs/005-push-notification/spec.md

**구현 내용**
1. FCM 통합 (Android)
   - Firebase 프로젝트 설정
   - FCM SDK 통합
   - 토큰 관리

2. APNs 통합 (iOS)
   - Apple Developer 인증서
   - APNs SDK 통합
   - 토큰 관리

3. 백엔드 스케줄러
   - node-cron: 시간 기반 알림
   - 알림 템플릿 관리
   - 발송 로그

4. 사용자 설정
   - 알림 시간 커스터마이징
   - 알림 끄기
   - 알림 타입별 제어

**테스트**
- 실제 디바이스 테스트 (iOS + Android)
- 알림 오픈율 추적
```

#### F6 인증 시스템 구현

```
/sc:implement --agent security-engineer

작업: F6 사용자 인증 및 프로필 관리 구현

**참조**
- spec: .specify/specs/006-authentication/spec.md

**구현 내용**
1. JWT 인증
   - Access Token (15분)
   - Refresh Token (7일)
   - 토큰 갱신 로직

2. 이메일 + 비밀번호 인증
   - 회원가입: 이메일 인증
   - 로그인: bcrypt 검증
   - 비밀번호 재설정

3. 소셜 로그인 (OAuth 2.0)
   - Google OAuth
   - Apple Sign In
   - Kakao OAuth

4. 프로필 관리
   - 프로필 정보 CRUD
   - 프로필 사진 업로드 (S3)
   - 계정 삭제 (GDPR)

**보안 기준**
- OWASP Top 10 준수
- HTTPS 강제
- Rate Limiting
- CSRF 방어
```

### 6.3 통합 테스트

```
/sc:test --agent qa-expert

전체 시스템 통합 테스트를 수행해주세요.

**테스트 범위**
1. Unit Tests
   - 프론트엔드: Jest + React Native Testing Library
   - 백엔드: Jest + Supertest
   - 커버리지: 80% 이상

2. Integration Tests
   - API 엔드포인트 테스트
   - 데이터베이스 연동 테스트
   - AI API 통합 테스트

3. E2E Tests (Playwright MCP 활용)
   - 온보딩 플로우 전체
   - AI 목표 분해 → 퀘스트 생성
   - AI 캐릭터 대화
   - 퀘스트 완료 → 진도율 업데이트
   - 푸시 알림 수신
   - 로그인/로그아웃

4. 성능 테스트
   - API 응답 시간 (500ms 이내)
   - AI 응답 시간 (3초 이내)
   - 앱 로딩 시간 (3초 이내)
   - 동시 사용자 부하 테스트

**자동화**
- GitHub Actions CI/CD
- 테스트 실패 시 자동 알림
- 커버리지 리포트 자동 생성
```

---

## 7. 검증 및 테스트

### 7.1 명세 대비 검증

```
/sc:analyze --validate-spec

.specify/specs/ 폴더의 모든 spec.md와
실제 구현을 비교하여 검증해주세요.

**검증 항목**
1. Acceptance Criteria 100% 충족 여부
2. 비기능 요구사항 충족 (성능, 보안, 확장성)
3. 데이터 모델 일치 여부
4. API 명세 일치 여부
5. UI/UX 디자인 반영 여부

**검증 결과**
- ✅ 충족 항목
- ⚠️ 부분 충족 항목 (개선 필요)
- ❌ 미충족 항목 (우선 수정)
```

### 7.2 품질 게이트 체크

```
/sc:analyze --quality-gates

다음 품질 기준을 검증해주세요:

**코드 품질**
- TypeScript strict mode 준수
- ESLint 에러 0개
- 테스트 커버리지 80% 이상

**성능**
- API 응답 시간 500ms 이내 (95 percentile)
- AI 응답 시간 3초 이내
- 앱 로딩 시간 3초 이내
- 앱 크래시율 0.5% 이하

**보안**
- OWASP Top 10 준수
- 민감 정보 암호화
- JWT 토큰 보안
- HTTPS 강제

**접근성**
- WCAG 2.1 AA 준수
- 스크린 리더 지원
- 다크 모드 지원
- 폰트 크기 조절

**문서화**
- README.md 완성
- API 문서 (Swagger)
- 개발 가이드
- 배포 가이드
```

---

## 8. 문서화 및 완료

### 8.1 최종 문서화

```
/sc:document

다음 문서들을 생성해주세요:

1. **README.md**
   - 프로젝트 소개
   - 기능 목록
   - 기술 스택
   - 설치 및 실행 방법
   - 환경 변수 설정
   - 라이선스

2. **API 문서**
   - Swagger/OpenAPI 스펙
   - 엔드포인트 목록
   - 요청/응답 예시
   - 에러 코드

3. **개발 가이드**
   - 프로젝트 구조
   - 코딩 컨벤션
   - Git 워크플로우
   - 테스트 작성법

4. **배포 가이드**
   - AWS 인프라 설정
   - CI/CD 파이프라인
   - 환경별 설정 (dev, staging, prod)
   - 모니터링 및 로깅

5. **사용자 가이드**
   - 앱 사용법
   - FAQ
   - 트러블슈팅
```

### 8.2 세션 저장 및 완료

```
/sc:save

Study Quest MVP Must Have 기능 구현 완료

**구현 완료 항목**
- ✅ F1: 사용자 온보딩 및 목표 설정
- ✅ F2: AI 기반 자동 목표 분해
- ✅ F3: AI 캐릭터 동반자 (3종)
- ✅ F4: 일일 퀘스트 제공 및 진도 추적
- ✅ F5: 푸시 알림
- ✅ F6: 사용자 인증 및 프로필 관리

**품질 메트릭**
- 테스트 커버리지: 85%
- API 응답 시간: 평균 320ms
- AI 응답 시간: 평균 2.1초
- 앱 크래시율: 0.3%

**다음 단계**
- 베타 테스트 (100명)
- 피드백 수집 및 개선
- 정식 런칭 (2026년 4월)
```

---

## 9. 추가 유용한 명령어

### 9.1 문제 해결

```
# 에러 분석 및 디버깅
/sc:troubleshoot --introspect

# 코드 리뷰
/sc:analyze --code-review

# 성능 최적화
/sc:improve --focus performance

# 보안 감사
/sc:analyze --focus security
```

### 9.2 반복 작업

```
# 모든 spec.md 재검토
for spec in .specify/specs/*/spec.md; do
  /speckit.clarify --file "$spec"
done

# 모든 plan.md 기반 tasks.md 재생성
for plan in .specify/specs/*/plan.md; do
  /speckit.tasks --file "$plan"
done
```

### 9.3 리팩토링

```
# 코드 품질 개선
/sc:improve --agent refactoring-expert

# 기술 부채 제거
/sc:cleanup --technical-debt

# 테스트 커버리지 향상
/sc:test --increase-coverage
```

---

## 10. 체크리스트

### 10.1 프로젝트 준비 완료 체크리스트

- [ ] Spec-Kit 프로젝트 초기화
- [ ] SuperClaude 세션 로드
- [ ] PRD 파일 복사
- [ ] 디자인 파일 복사
- [ ] Constitution 작성 완료

### 10.2 SPECIFY 단계 완료 체크리스트

- [ ] F1 명세 작성 완료
- [ ] F2 명세 작성 완료
- [ ] F3 명세 작성 완료
- [ ] F4 명세 작성 완료
- [ ] F5 명세 작성 완료
- [ ] F6 명세 작성 완료
- [ ] 각 명세 명확화 완료

### 10.3 PLAN 단계 완료 체크리스트

- [ ] 시스템 아키텍처 설계 완료
- [ ] 기술 스택 결정 완료
- [ ] F1-F6 각 기능별 구현 계획 작성
- [ ] 데이터베이스 스키마 설계 완료
- [ ] API 설계 완료

### 10.4 TASKS 단계 완료 체크리스트

- [ ] 전체 작업 분해 완료
- [ ] 작업 우선순위 정의
- [ ] 작업 일정 수립
- [ ] 의존성 관계 정리
- [ ] 리스크 식별

### 10.5 IMPLEMENT 단계 완료 체크리스트

- [ ] 프로젝트 초기 셋업 완료
- [ ] F1 구현 완료 (프론트 + 백엔드)
- [ ] F2 구현 완료 (AI 통합)
- [ ] F3 구현 완료 (AI 캐릭터)
- [ ] F4 구현 완료 (퀘스트 + 진도)
- [ ] F5 구현 완료 (푸시 알림)
- [ ] F6 구현 완료 (인증)
- [ ] 통합 테스트 완료

### 10.6 검증 및 완료 체크리스트

- [ ] 명세 대비 검증 완료
- [ ] 품질 게이트 통과
- [ ] 문서화 완료
- [ ] 세션 저장 완료

---

## 11. 참고 사항

### 11.1 주요 원칙

1. **Complete Implementation**: 선택한 기능은 100% 완성
2. **Test-Driven**: 모든 코드는 테스트 작성 필수
3. **Spec-Driven**: 명세 없는 기능 추가 금지
4. **Documentation**: 모든 주요 기능 문서화

### 11.2 금지사항

- ❌ TODO 코멘트로 구현 미루기
- ❌ Mock 데이터로 기능 대체
- ❌ 테스트 없는 코드 커밋
- ❌ 명세 없는 기능 추가

### 11.3 권장사항

- ✅ 병렬 작업 최대 활용 (TodoWrite)
- ✅ MCP 서버 적극 활용 (Magic, Context7, Playwright)
- ✅ SuperClaude 에이전트 활용
- ✅ 진행 상황 정기 저장 (/sc:save)

---

**작성 완료일**: 2025-11-17
**예상 MVP 완료일**: 2026-01-31 (2개월)
**다음 단계**: 베타 테스트 (2026년 2월-3월)
