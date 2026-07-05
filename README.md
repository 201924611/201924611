<h1 align="center">안녕하세요, 허진수입니다 👋</h1>

<p align="center">
  풀스택으로 서비스를 만들어 <b>실제 배포·운영</b>까지 이어가는 개발자입니다.<br/>
  Java/Spring 백엔드와 React 프론트엔드를 함께 다루며,<br/>
  최근에는 <b>딥러닝·LLM 기반 AI 프로젝트</b>와 팀 단위 협업에 집중하고 있습니다.
</p>

<p align="center">
  <a href="mailto:hu349401@gmail.com"><img src="https://img.shields.io/badge/Email-hu349401@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white"/></a>
</p>

---

## 🛠 기술 스택

**Backend**
![Java](https://img.shields.io/badge/Java-007396?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![JPA](https://img.shields.io/badge/JPA-59666C?style=flat-square&logo=hibernate&logoColor=white)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)

**Frontend**
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)

**AI / ML**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat-square&logo=keras&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)

**Cloud / Etc.**
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Azure Functions](https://img.shields.io/badge/Azure_Functions-0062AD?style=flat-square&logo=azurefunctions&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

---

## 🌊 대표 서비스 — OceanKeeper

### [OceanKeeper — 바다살리기네트워크](https://github.com/201924611/oceankeeper)
> 해양 정화 봉사활동을 연결하는 웹 플랫폼 · **팀 프로젝트(5인)** · 🔗 **[oceankeeper.org](https://oceankeeper.org) 배포 운영 중**

- **풀스택** — Next.js 프론트엔드 + Spring Boot 백엔드 (FE ~56 · BE ~36 커밋)
- 🔧 **낙관적 업로드 + 비동기 압축 파이프라인 설계** — 원본 즉시 업로드(바로 확인) → Azure Functions 비동기 압축 → 압축 완료 후 Function이 DB 경로 교체 → 처리 체감 **6~7초 → 0.2~0.3초**, 용량 **2.6MB → 344KB(~8배↓)**
- 인증/권한(Spring Security·JWT + NextAuth), 커뮤니티·마이페이지, 통계 시각화(Nivo/ECharts), PWA 오프라인 캐시 담당
- `Next.js 16` · `NextAuth` · `Spring Boot 3.5` · `Spring Security/JWT` · `JPA` · `PostgreSQL` · `Azure Functions` · `Azure Blob`

<p align="center">
  <img src="https://raw.githubusercontent.com/201924611/oceankeeper/master/docs/screenshots/desktop-landing.png" alt="OceanKeeper 메인 랜딩" width="49%"/>
  <img src="https://raw.githubusercontent.com/201924611/oceankeeper/master/docs/screenshots/desktop-map.png" alt="OceanKeeper 활동 지도" width="49%"/>
</p>

---

## ⚡ 백엔드 성능 최적화 (실무)

### 모니터링 통계 쿼리 최적화 — 45초 → 1초 미만 (97%↓)
> 운영 불가 수준(45초)이던 대용량 통계 조회 쿼리를 실행계획 분석 기반으로 재구성

- **병목:** 1:N 상세 테이블 2종을 사전집계 없이 직접 JOIN → **N×M 팬아웃(카티션 곱)** + 필터가 조인 이후에 걸리는 뒤늦은 필터링
- **해결:** 공통 필터(연도·구역)로 대상 키만 뽑는 `base` CTE로 **조기 필터링(Early Filtering)** → 상세 테이블을 **각자 사전집계 후 INNER JOIN**으로 재구성해 팬아웃 원천 차단
- **결과:** 응답 **45초 → 1초 미만 (약 97%↓)** · 기능·결과값 동일, 옵티마이저 처리량만 감소
- `PostgreSQL` · `MyBatis` · `CTE` · `Query Optimization`

---

## 🤖 AI / 딥러닝

### [3D 뇌종양 MRI Segmentation](https://github.com/pnucse-capstone-2024/Capstone-2024-team-01) · 대학 졸업과제
> BraTS 데이터셋 기반 3D 뇌종양 분할 딥러닝 모델 + 웹 연동 시스템 · **팀 프로젝트(부산대 CSE 2024 캡스톤 팀1)**

- **U-Net** 구조로 3D MRI 뇌종양 영역을 정밀 Segmentation, Dice coefficient·cross entropy loss로 성능 최적화
- 모델 추론(Flask) → 게이트웨이(Node.js) → 업로드·시각화(React)로 이어지는 **웹 연동 파이프라인** 구축
- `Python` · `TensorFlow` · `Keras` · `React` · `Node.js` · `Flask`

### meisllm — 사내 RAG 챗봇 에이전트 *(private)*
> Gemma 3/4 기반 사내 지식 챗봇 에이전트 · **개인 프로젝트**

- **Gemma 3/4 QLoRA 파인튜닝** + **ChromaDB 벡터 RAG**로 사내 문서 질의응답 구성
- `FastAPI` + `SSE` 스트리밍 응답 서빙
- `Python` · `QLoRA` · `ChromaDB` · `FastAPI` · `SSE`
- 🔒 비공개 저장소 — 코드 대신 구성만 소개

### [agent-core — 자율 오케스트레이터](https://github.com/201924611/agent-core)
> HTTP로 목표(goal)를 받아 24시간 자율 수행하는 중앙 오케스트레이터 · **개인 프로젝트 · MIT 오픈소스**

- 하위 에이전트 동적 생성·위임, 계획가→실행가→평가가 반복 빌드 루프, 실행 trace/eval 자동 기록
- 내장 웹 채팅 UI · Telegram 채널 · 데스크톱 앱(.exe) 패키징까지 구현
- `Python` · `FastAPI` · LLM 에이전트 오케스트레이션

---

## 🧑‍🤝‍🧑 팀 / 공모전

### [AI 기반 통합 공항시설 관리 시스템](https://github.com/airport-ai-facility-monitoring) · 팀 프로젝트
> 지방공항용 저비용·고효율 AI 시설 관리 솔루션 — 이상 탐지 · 수리비용/기간 예측 · **보고서 자동 생성** 올인원 시스템

- AI 리포트 생성(`ai-report`, `ai-report-maintenance`)과 프론트/백엔드 워크스페이스로 구성된 **멀티 레포 팀 프로젝트**
- `Java` · `Spring Boot` · `JavaScript` · `Vue` · `AI 리포트 자동화`

### [Bilive — 밴드 합주실 예약 플랫폼](https://github.com/PROFITLAB-HACKATHON-2025/bilive_frontend) · 해커톤
> 밴드 합주실 검색·예약·커뮤니티를 하나로 묶은 모바일 웹앱 · **2025 PROFITLAB 해커톤 출품작 (팀 프로젝트)**

- 지도 기반 합주실 검색과 필터 UI 중심의 모바일 웹앱 MVP 구축
- `React` · `TypeScript` · `Zustand` · `React Query` · `styled-components` · `Vite`
- 프론트엔드 공개 · 백엔드 비공개

### [DAIC — ToTime 문서 일정 자동화](https://github.com/2024-PNU-SW-StudyGroup/DAIC-naggedenaum) · 문서 AI 공모전
> 문서에서 일정·마감일을 추출해 워크시트를 자동 생성하는 플랫폼 · **PNU × Upstage Document AI Challenge 2025 (팀 '내께더나음')**

- Upstage **Document Parse**로 PDF/PPT/이미지 문서에서 시간 데이터 추출, **Solar Embedding** 기반 중요도 정렬
- Notion·Google Calendar 연동으로 실무 적용까지 고려
- `Python` · `Upstage API` · `Document Parse` · `Solar Embedding`

---

## 📚 기타

### [algorithm](https://github.com/201924611/algorithm)
> 백준(BOJ) 문제 풀이 자동 업로드 · 꾸준한 알고리즘 학습 기록 · `Java`

### [anti-theft-blanket](https://github.com/embeded-07/anti-theft-blanket)
> 부산대 임베디드시스템설계및실험 과목 프로젝트 · **팀 프로젝트** · `C`

---

## 📊 GitHub

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=201924611&show_icons=true&hide_border=true&count_private=true" height="160"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=201924611&layout=compact&hide_border=true&langs_count=8" height="160"/>
</p>

<p align="center"><sub>📫 <a href="mailto:hu349401@gmail.com">hu349401@gmail.com</a></sub></p>
