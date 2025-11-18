# Study Quest - 빠른 시작 가이드

**해커톤 심사위원을 위한 빠른 실행 가이드**

---

## ⚡ 3가지 방법으로 확인 가능

### 방법 1: 라이브 데모 확인 (가장 빠름! ⚡)

```
📱 데모 앱 링크: [Expo Go 링크 또는 웹 데모 URL]

QR 코드로 바로 접속:
[QR 코드 이미지]

테스트 계정:
- 이메일: demo@studyquest.com
- 비밀번호: Demo1234!
```

---

### 방법 2: 데모 영상 시청 (2번째로 빠름)

```
📺 YouTube 데모 영상: [YouTube 링크]

- 길이: 3분
- 내용: 전체 기능 시연
- 자막: 한글/영문
```

---

### 방법 3: 로컬 실행 (개발자용)

#### 사전 요구사항
- Node.js 18.x
- PostgreSQL 13+
- React Native CLI (모바일 앱 실행 시)

#### 빠른 설치 (5분)

```bash
# 1. 저장소 클론
git clone https://github.com/Aithor-organization/HACK-SeSAC-.git
cd HACK-SeSAC-

# 2. 백엔드 실행
cd src/backend
npm install
cp .env.example .env
# .env 파일 편집: DATABASE_URL, OPENAI_API_KEY 설정
npx prisma migrate dev
npm run dev
# ✅ 서버 실행: http://localhost:3000

# 3. 프론트엔드 실행 (새 터미널)
cd src/frontend
npm install
npx react-native run-ios
# 또는
npx react-native run-android
```

---

## 📂 주요 문서 위치

### 필수 문서
- **프로젝트 개요**: [docs/PROJECT_OVERVIEW.md](docs/PROJECT_OVERVIEW.md)
- **PRD**: [docs/PRD.md](docs/PRD.md)
- **아키텍처**: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
- **AI 전략**: [docs/AI_STRATEGY.md](docs/AI_STRATEGY.md)

### 시연 자료
- **데모 스크립트**: [demo/DEMO_SCRIPT.md](demo/DEMO_SCRIPT.md)
- **피칭 자료**: [demo/PITCH_DECK.pdf](demo/PITCH_DECK.pdf)
- **스크린샷**: [demo/screenshots/](demo/screenshots/)

---

## 🎯 MVP 핵심 기능 (5개)

1. ✅ **온보딩**: 5단계 (기본정보 → 성적 → 목표 → D-Day → 캐릭터)
2. ✅ **AI 목표 분해**: "수학 70→90점" → Phase별 계획 + 일일 퀘스트
3. ✅ **홈 화면**: 오늘의 퀘스트 3개 + 체크박스 완료
4. ✅ **AI 대화**: 3종 캐릭터와 채팅
5. ✅ **인증**: Guest 모드 (간단한 로그인)

---

## 📊 개발 현황

### 완료 ✅
- [x] 프로젝트 기획 (PRD, 아키텍처)
- [x] 디자인 (와이어프레임 12개)
- [x] AI 프롬프트 엔지니어링

### 진행 중 🔄
- [ ] 프론트엔드 개발 (60%)
- [ ] 백엔드 API 개발 (70%)
- [ ] AI 통합 (80%)

### 예정 ⏳
- [ ] E2E 테스트
- [ ] AWS 배포
- [ ] 베타 테스트 (100명)

---

## 🏆 차별화 포인트

| 항목 | 기존 앱 | Study Quest |
|------|---------|-------------|
| 목표 분해 | 수동 | **AI 자동** ⭐ |
| 멘탈 관리 | 없음 | **AI 캐릭터** ⭐ |
| 비용 | 무료 or 월 3만원 | **월 1.5만원** |
| 개인 맞춤 | 낮음 | **매우 높음** |

---

## 📞 문의

- **이메일**: team@studyquest.com
- **GitHub Issues**: [이슈 등록](https://github.com/Aithor-organization/HACK-SeSAC-/issues)
- **데모 요청**: demo@studyquest.com

---

**해커톤**: HACK-SeSAC
**버전**: MVP 1.0
**업데이트**: 2025-11-17
