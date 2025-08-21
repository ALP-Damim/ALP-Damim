# Mini AI Class Assistant

AI 기반 학습 보조 플랫폼 (데모 프로젝트)

## 프로젝트 소개 
교사와 학생을 대상으로 한 경량 학습 관리 및 AI 보조 시스템입니다.  
교사는 과제/퀴즈를 등록하고, 학생은 답안을 제출하면 AI가 RAG기반 피드백을 제공합니다.  
교사는 결과 및 통계를 확인하고 최종 점수를 확정할 수 있습니다.

## 주요 기능 
- **교사**
  - 수업/과제/퀴즈 CRUD
  - 학생 출결 체크
  - 제출 답안 피드백/통계 조회
  - 최종 점수 확정
- **학생**
  - 과제/퀴즈 답안 제출
  - AI 기반 피드백 및 점수 조회
- **AI 서비스**
  - LangChain RAG 기반 근거 검색

## 아키텍처  
- **User & Class Service**: 사용자/수업/등록/출결 관리
- **Assignment Service**: 과제 및 자료 관리
- **Submission & Grading Service**: 제출/점수 저장
- **AI Service**: LangChain RAG 
- **공통 인프라**: 
  - Azure PostgreSQL (DB)
  - Azure Storage (자료 업로드/첨부)
  - Azure Key Vault (비밀 관리)
  - Azure App Service / Container Apps (배포)

## 데이터 모델 (엔터티) 
- `users`  
- `classes`  
- `enrollments`  
- `assignments`  
- `submissions`  
- `feedbacks` (AI 피드백·근거)  
- `materials` (수업 자료 메타)

## 요구사항 (기능 명세 요약) 
| ID | 구분 | 설명 |
| --- | --- | --- |
| FR-A-001 | 인증 | 이메일/비밀번호 로그인 → JWT 발급 (미구현) |
| FR-B-001 | 수업 | 교사는 수업 생성/학생 등록 가능 |
| FR-B-002 | 수업 | 교사는 수업 시작전 알림 가능 |
| FR-C-001 | 과제 | 교사는 과제/퀴즈 수정 삭제 생성 조회 가능 |
| FR-C-002 | 과제 | 교사는 과제 여부 알림 가능 |
| FR-D-001 | 제출 | 학생은 답안 제출 가능 |
| FR-D-002 | AI 피드백 | 제출 시 AI 피드백 생성·저장 |
| FR-D-003 | 점수 조회| 교사는 실시간 및 최종 점수 조회가능|
| FR-E-001 | 결과 조회 | 교사/학생 결과 조회 가능 |

## 🚀 기술 스택
- **Backend**: Java Spring Boot 3, Gradle, JPA
- **AI**: LangChain 
- **Infra**: Azure App Service, PostgreSQL, Storage, Key Vault, Vercel , Azure Container Respository, Azure Container Registry (ACR)
- **Test**: HTTP Test 
- **Networking**: Azure VNet
## 비기능 요구사항 
- **트래픽 관리**: LLM 요청 과도화 억제(상태, 횟수,시간 데이터 기반)
- **보안**: HTTPS 전 구간, Key Vault로 비밀 관리
- **로깅**: Azure log, 주의 사항 slack webhook(미구현)

## 일정 (5일 / 3인)
- 요구사항/스키마/API 초안
- 리포지토리 세팅  
- User & Class, Assignment CRUD 구현  
- Submission + AI(RAG)  
- 화면 연동
- 테스트 ◀️ 현단계
- 성능 로그
- 최종 문서/영상   
- 기능 시연 및 발표 

## 제출물
- 기능 명세서
- API 명세 (OpenAPI/Swagger)
- 시연 영상 (1 cycle: 60~90초)
- 코드
- 최종 기획서

---
## .env
```
# Database (Azure PostgreSQL)
DB_HOST=<your-azure-db-host>
DB_PORT=5432
DB_NAME=<your-db-name>
DB_USER=<your-db-username>
DB_PASSWORD=<your-db-password>

# Azure AI Service (ex: OpenAI on Azure)
AI_ENDPOINT=<your-azure-ai-endpoint>
AI_KEY=<your-azure-ai-key>

```
---

## 실행 방법

### Backend (Spring Boot)
```bash
# 프로젝트 실행
./gradlew bootRun

# 빌드 후 실행
./gradlew build
java -jar build/libs/*.jar

# 기본 실행 포트
http://localhost:8080

# Swagger UI (API 확인)
http://localhost:8080/swagger-ui.html
```

### Frontend (Vite + Vercel)
```
# 의존성 설치
npm install

# 개발 서버 실행
npm run dev

# 기본 실행 포트
http://localhost:5173
```

### Vercel 배포
GitHub 리포지토리와 연동  
Vercel에서 프로젝트 Import  
Framework 선택: Vite  
Build Command: npm run build  
Output Directory: dist/  
배포 완료 후 제공된 URL에서 접근 가능
