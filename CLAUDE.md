# CLAUDE.md - AI Assistant Guide for Co-Plan

> This document provides essential context and guidelines for AI assistants working on the Co-Plan codebase.

## Project Overview

**Co-Plan** is an AI-powered learning management platform designed for Korean college exam repeaters (N수생 - students retaking the SUNEUNG/Korean SAT). The platform transforms vague learning goals into actionable daily quests using SMART principles through AI conversation.

### Core Value Proposition
- **Problem**: N수생 struggle with overwhelming 8-month study plans, motivation loss, and expensive tutoring ($2,500/month)
- **Solution**: AI companion that breaks down goals into daily quests + personalized coaching at 1/167th the cost

### Project Status
- **Stage**: Hackathon MVP Development (새싹 해커톤 2025)
- **Team**: 에이아이터 (Aithor) - 2 members
- **Current State**: Documentation complete, implementation pending

---

## Repository Structure

```
HACK-SeSAC-/
├── CLAUDE.md                    # This file - AI assistant guide
├── README.md                    # Project overview and documentation
├── HACKATHON_STRUCTURE.md       # Hackathon submission structure guide
├── Implementation_Commands.md   # Detailed implementation commands
├── .gitignore                   # Git ignore configuration
│
├── docs/                        # [PLANNED] Project documentation
│   ├── PROJECT_OVERVIEW.md
│   ├── PRD.md                   # Product Requirements Document
│   ├── ARCHITECTURE.md          # System architecture
│   ├── API_SPECIFICATION.md     # API specs
│   ├── DATABASE_SCHEMA.md       # Database design
│   └── AI_STRATEGY.md           # AI/ML strategy
│
├── design/                      # [PLANNED] Design assets
│   ├── wireframes/              # UI wireframes
│   └── user-flow.md             # User flow documentation
│
├── src/                         # [PLANNED] Source code
│   ├── frontend/                # React Native mobile app
│   │   ├── screens/             # Screen components
│   │   ├── components/          # Reusable components
│   │   ├── services/            # API services
│   │   └── utils/               # Utilities
│   ├── backend/                 # Node.js Express API
│   │   ├── routes/              # API routes
│   │   ├── controllers/         # Business logic
│   │   ├── services/            # Services (AI, DB)
│   │   ├── models/              # Data models
│   │   └── middleware/          # Express middleware
│   └── shared/                  # Shared types/utilities
│
├── tests/                       # [PLANNED] Test suites
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── deployment/                  # [PLANNED] Deployment configs
│   ├── docker-compose.yml
│   └── DEPLOYMENT_GUIDE.md
│
└── demo/                        # [PLANNED] Demo materials
    ├── PITCH_DECK.pdf
    ├── DEMO_SCRIPT.md
    └── screenshots/
```

---

## Technology Stack

### Frontend (Mobile)
| Technology | Version | Purpose |
|------------|---------|---------|
| React Native | 0.72+ | Cross-platform mobile framework |
| TypeScript | 5.x | Type safety |
| React Navigation | 6.x | Navigation |
| Zustand | 4.x | State management |
| React Native Paper | 5.x | UI components |
| react-native-chart-kit | - | Progress charts |

### Backend (API)
| Technology | Version | Purpose |
|------------|---------|---------|
| Node.js | 18.x | Runtime |
| Express | 4.x | Web framework |
| TypeScript | 5.x | Type safety |
| Zod | 3.x | Validation |
| JWT | - | Authentication |

### Database & Services
| Service | Purpose |
|---------|---------|
| Firebase Firestore | User data, study plans |
| Firebase Auth | Authentication |
| Redis | AI response caching |

### AI Integration
| Service | Purpose |
|---------|---------|
| Claude Sonnet 4.5 | SMART goal decomposition + AI characters |
| RAGFlow | SUNEUNG exam data retrieval |

### Cloud Infrastructure
| Service | Purpose |
|---------|---------|
| AWS EC2 | API hosting |
| AWS S3 | File storage |
| Firebase Cloud Messaging | Push notifications |
| APNs | iOS push notifications |

---

## Key Features (MVP)

### F1: User Onboarding (5 Steps)
- Basic info input
- Current grades per subject
- Target scores and university
- D-Day calculation
- AI character selection (3 types)

### F2: AI SMART Goal Decomposition (Core Differentiator)
- Natural language goal input → AI decomposition
- Phase-based roadmap (Concept → Types → Practice)
- Daily quest auto-generation
- Response time: < 5 seconds

### F3: AI Character Companions (3 Types)
| Type | Persona | Style |
|------|---------|-------|
| A | 30s Consultant | Data-driven, strict mentor |
| B | 20s Successful Repeater | Empathetic friend |
| C | 25s University Student | Hybrid - friendly but firm |

### F4: Daily Quest System
- 3-5 quests per day displayed on home
- Checkbox completion with animations
- Daily/weekly/overall progress visualization

### F5: Push Notifications
- 8 AM: "Check today's quests"
- 9 PM: "Review today's progress"
- 3-day inactive: Motivational re-engagement

### F6: Authentication
- Email + password
- Social login (Google, Apple, Kakao)
- Guest mode for MVP
- JWT-based (Access: 15min, Refresh: 7 days)

---

## Development Guidelines

### Code Quality Standards
- **TypeScript**: Strict mode required
- **Test Coverage**: 80% minimum target
- **API Response**: < 500ms (95th percentile)
- **AI Response**: < 3 seconds
- **App Crash Rate**: < 0.5%

### Naming Conventions
```typescript
// Components: PascalCase
QuestCard.tsx
ProgressChart.tsx

// Files: kebab-case for non-components
api-service.ts
auth-middleware.ts

// Variables/Functions: camelCase
const dailyQuests = [];
function calculateProgress() {}

// Constants: SCREAMING_SNAKE_CASE
const MAX_DAILY_QUESTS = 5;
const API_TIMEOUT_MS = 5000;
```

### Directory Structure Conventions
```
components/
├── ComponentName/
│   ├── index.tsx           # Main component
│   ├── ComponentName.styles.ts  # Styles
│   ├── ComponentName.types.ts   # Types
│   └── ComponentName.test.tsx   # Tests
```

### API Design
- RESTful endpoints
- Base URL: `/api/v1/`
- Authentication: Bearer token in headers
- Response format:
```json
{
  "success": true,
  "data": {},
  "error": null
}
```

### Git Workflow
- Branch naming: `feature/feature-name`, `fix/bug-description`
- Commit messages: Conventional commits (feat:, fix:, docs:, etc.)
- PR required for merging to main

---

## AI Integration Patterns

### Claude API Usage
```typescript
// System prompt structure for goal decomposition
const systemPrompt = `
당신은 재수생/N수생 전문 학습 플래너입니다.
사용자의 목표를 SMART 원칙에 따라 분해합니다:
- Specific (구체적)
- Measurable (측정 가능)
- Achievable (달성 가능)
- Realistic (현실적)
- Time-bound (기한 명확)
`;

// Character-specific prompts
const characterPrompts = {
  A: "엄근진 멘토형: 데이터 기반 조언, 단호한 어조",
  B: "공감 친구형: 따뜻한 격려, 공감적 대화",
  C: "하이브리드형: 친근하면서도 명확한 피드백"
};
```

### RAGFlow Integration
- SUNEUNG exam frequency data (2020-2024)
- Subject-to-grade required unit mapping
- Average study time per unit
- N수생 success case studies

### Cost Optimization
- Redis caching for repeated queries
- Rate limiting: 10 req/min per user
- Target cost: $3/user/month

---

## Database Schema (Key Tables)

### Users
```sql
users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE,
  password_hash VARCHAR(255),
  name VARCHAR(100),
  grade VARCHAR(20),  -- 재수, 삼수, etc.
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)
```

### Study Plans
```sql
study_plans (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  goal_text TEXT,
  target_score INT,
  current_score INT,
  subject VARCHAR(50),
  created_at TIMESTAMP
)
```

### Daily Quests
```sql
daily_quests (
  id UUID PRIMARY KEY,
  study_plan_id UUID REFERENCES study_plans(id),
  title VARCHAR(255),
  description TEXT,
  estimated_minutes INT,
  scheduled_date DATE,
  completed BOOLEAN DEFAULT FALSE,
  completed_at TIMESTAMP
)
```

---

## Common Tasks

### Setting Up Local Development
```bash
# Clone repository
git clone https://github.com/Aithor-organization/HACK-SeSAC-.git
cd HACK-SeSAC-

# Backend setup
cd src/backend
cp .env.example .env  # Configure environment variables
npm install
npm run dev

# Frontend setup
cd src/frontend
npm install
npx react-native run-ios  # or run-android
```

### Environment Variables
```bash
# Backend .env
FIREBASE_CONFIG=<firebase-config-json>
CLAUDE_API_KEY=<anthropic-api-key>
JWT_SECRET=<jwt-secret>
RAGFLOW_API_ENDPOINT=<ragflow-endpoint>
REDIS_URL=<redis-connection-string>
```

### Running Tests
```bash
# Unit tests
npm run test

# Integration tests
npm run test:integration

# E2E tests
npm run test:e2e
```

---

## Important Considerations

### Security
- Never commit API keys or secrets
- Use environment variables for sensitive data
- Implement rate limiting on all endpoints
- Validate all user inputs with Zod
- GDPR compliance for data deletion

### Performance
- Implement pagination for list endpoints
- Use Redis caching for AI responses
- Optimize images before upload
- Lazy load components where appropriate

### Accessibility
- Support screen readers
- Maintain sufficient color contrast
- Allow font size adjustment
- Support dark mode

### Localization
- Primary language: Korean
- UI text should be externalized
- Date/time in Korean timezone (KST)

---

## Troubleshooting

### Common Issues

**Firebase Connection Issues**
- Verify Firebase config in environment
- Check network permissions in app manifest

**AI Response Timeouts**
- Check Claude API rate limits
- Verify Redis cache is running
- Review prompt length (shorter = faster)

**Build Failures**
- Clear node_modules and reinstall
- For iOS: `cd ios && pod install`
- For Android: Clean gradle cache

---

## Resources

### Documentation
- [React Native Docs](https://reactnative.dev/)
- [Claude API Docs](https://docs.anthropic.com/)
- [Firebase Docs](https://firebase.google.com/docs)
- [Express.js Guide](https://expressjs.com/)

### Internal References
- `README.md` - Project overview
- `HACKATHON_STRUCTURE.md` - Submission structure
- `Implementation_Commands.md` - Detailed implementation guide

---

## Contact & Support

**Team Aithor (에이아이터)**
- PM/Lead: 서현
- Full-stack Developer: 서훈

**Repository**: https://github.com/Aithor-organization/HACK-SeSAC-

---

*Last Updated: 2025-11-25*
*Project Version: MVP 1.0 (In Development)*
