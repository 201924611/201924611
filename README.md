<h1 align="center">안녕하세요, 허진수입니다 👋</h1>

<p align="center">
  풀스택으로 서비스를 만들어 <b>실제 배포·운영</b>까지 이어가는 개발자입니다.<br/>
  Java/Spring 백엔드와 React 프론트엔드를 함께 다루며,<br/>
  실서비스 이미지 처리 <b>6~7초 → 0.2~0.3초</b>, 통계 쿼리 <b>45초 → 1초</b> 등 성능 문제를 수치로 해결해왔습니다.
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
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)

**AI / ML**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=flat-square&logo=keras&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)

**Cloud / Etc.**
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Azure Functions](https://img.shields.io/badge/Azure_Functions-0062AD?style=flat-square&logo=azurefunctions&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

---

## 🌊 대표 서비스 — OceanKeeper

### [OceanKeeper — 바다살리기네트워크](https://github.com/201924611/oceankeeper)
> 해양 정화 봉사활동을 연결하는 웹 플랫폼 · **팀 프로젝트(5인)** · 🔗 **[oceankeeper.org](https://oceankeeper.org) 배포 운영 중**

- **풀스택** — Next.js 프론트엔드 + Spring Boot 백엔드 (FE ~56 · BE ~36 커밋)
- 🔧 **이미지 업로드 병목 해결 (발견 → 분석 → 해결)**
  - **발견:** 다중 이미지 업로드 시 **6~7초 대기** + 클라이언트 **CPU 점유율 100%** 확인
  - **분석:** 프론트가 업로드 전 **브라우저 CPU로 리사이징·압축을 동기 처리** → 메인 스레드 점유로 화면 정지
  - **해결:** 압축을 클라이언트에서 분리 — **원본 즉시 업로드**, **Azure Functions가 비동기 압축(WebP)** 후 DB 경로 교체
  - **결과:** 처리 체감 **6~7초 → 0.2~0.3초** · 용량 **2.6MB → 344KB(~8배↓)**
- 인증/권한(Spring Security·JWT + NextAuth), 커뮤니티·마이페이지, 통계 시각화(Nivo/ECharts), PWA 오프라인 캐시 담당
- `Next.js 16` · `NextAuth` · `Spring Boot 3.5` · `Spring Security/JWT` · `JPA` · `PostgreSQL` · `Azure Functions` · `Azure Blob`

<p align="center">
  <img src="https://raw.githubusercontent.com/201924611/oceankeeper/master/docs/screenshots/desktop-landing.png" alt="OceanKeeper 메인 랜딩" width="49%"/>
  <img src="https://raw.githubusercontent.com/201924611/oceankeeper/master/docs/screenshots/desktop-map.png" alt="OceanKeeper 활동 지도" width="49%"/>
</p>

---

## ⚡ 백엔드 성능 최적화 (실무)

### 해양 쓰레기 모니터링 통계 쿼리 최적화 — 45초 → 1초 미만 (97%↓)
> 해양 포털에 축적된 **10만 건 이상**의 해양 쓰레기 수거·모니터링 데이터 통계 조회 개선 (발견 → 분석 → 해결)

- **발견:** 연도·구역별 통계 화면 응답이 **45초** — 운영 불가 수준
- **분석:** 실행계획(EXPLAIN) 확인 — 1:N 상세 테이블 2종을 사전집계 없이 JOIN해 **N×M 팬아웃(카티션 곱)** 발생, 필터는 조인 이후에야 적용
- **해결:** 공통 필터로 대상 키만 뽑는 `base` CTE **조기 필터링** → 상세 테이블을 **각자 사전집계 후 INNER JOIN**으로 재구성
- **결과:** **45초 → 1초 미만(97%↓)** · 기능·결과값 동일
- `PostgreSQL` · `MyBatis` · `CTE` · `Query Optimization`

---

## 🤖 AI / 딥러닝

### [3D 뇌종양 MRI Segmentation](https://github.com/pnucse-capstone-2024/Capstone-2024-team-01) · 대학 졸업과제
> BraTS 데이터셋 기반 3D 뇌종양 분할 딥러닝 모델 + 웹 연동 시스템 · **팀 프로젝트(부산대 CSE 2024 캡스톤 팀1)**

- **U-Net** 구조로 3D MRI 뇌종양 영역을 정밀 Segmentation, Dice coefficient·cross entropy loss로 성능 최적화
- 모델 추론(Flask) → 게이트웨이(Node.js) → 업로드·시각화(React)로 이어지는 **웹 연동 파이프라인** 구축
- `Python` · `TensorFlow` · `Keras` · `React` · `Node.js` · `Flask`

### meisllm — 사내 업무용 RAG 챗봇 에이전트 *(private)*
> **실제 사내 업무(내부 문서 검색·질의응답)를 자동화하려고 직접 구축**한 챗봇 · **개인 프로젝트**

- 흩어진 사내 문서를 **ChromaDB 벡터 RAG**로 인덱싱해 업무 질문에 근거 기반 답변
- **Gemma 3/4 QLoRA 파인튜닝**으로 사내 도메인 응답 품질 개선, `FastAPI` + `SSE` 스트리밍 서빙
- `Python` · `QLoRA` · `ChromaDB` · `FastAPI` · `SSE`
- 🔒 비공개 저장소 — 코드 대신 구성만 소개

### [agent-core — 자율 오케스트레이터](https://github.com/201924611/agent-core)
> HTTP로 목표(goal)를 받아 24시간 자율 수행하는 중앙 오케스트레이터 · **개인 프로젝트 · MIT 오픈소스**

- **문제:** 일회성 LLM 대화는 컨텍스트가 휘발되고, 긴 작업이 턴 제한에서 끊기며, 결과 품질을 측정할 수 없음
- **해결:** 하위 에이전트 **동적 생성·위임** + 계획→실행→평가 **반복 빌드 루프**(최고점 라운드 자동 복원) + 턴 소진 시 **세션 자동 이어하기**
- **관측·평가:** 전 실행 trace 기록 + **LLM 자동 채점**·A/B 비교로 결과물 품질을 정량 추적
- **영속 기록 저장소:** 결과·의사결정을 위키(`knowledge/`)에 자동 축적 → 세션·PC가 바뀌어도 상태 승계
- 14개 모듈(~2,950 LOC) 단독 구현 · 웹 챗 UI·Telegram·데스크톱 앱 패키징 · 이 시스템으로 **30+ 산출물** 생성
- `Python` · `FastAPI` · `asyncio` · MCP 커스텀 툴

### [AI 면접관 Agent — RAG 기반 에이전트형 모의면접](https://github.com/201924611/ai-interviewer-agent) · KT AIVLE 미니프로젝트
> 이력서를 올리면 직무 맞춤 질문 생성 → 답변 평가 → 최종 보고서까지 진행하는 LangGraph 에이전트 · **개인과제(v1) → 팀과제(v2) 고도화**

- **LangGraph 상태 그래프** — Resume 분석·요약 → 질문 전략 수립 → 도입 질문 → 답변 평가(**reflection 노드**) → 인터뷰 진행 검토(종료/추가질문 판단) → 최종 평가 보고서
- **RAG** — 전략별 참조 질문을 **Vector DB**로 구성해 맥락 맞춤 질문 생성
- **Gradio 웹 UI** + **Google Drive 연동**(이력서 파일 입출력)
- `Python` · `LangGraph` · `LangChain` · `OpenAI API` · `RAG(Vector DB)` · `Gradio` · `PyDrive2`

---

## 🧑‍🤝‍🧑 팀 / 공모전

### [AI 기반 통합 공항시설 관리 시스템](https://github.com/201924611/airport) · 팀 프로젝트
> 지방공항용 저비용·고효율 AI 시설 관리 솔루션 — 활주로 균열/이물질(FOD) 탐지 · 수리비용/기간 예측 · **보고서 자동 생성** 올인원 시스템

- **이벤트 스토밍으로 도메인 분해** — 회원 · 알림 · 경보 · 활주로 균열 탐지 · 활주로 이물질(FOD) 탐지 · 장비 분석 · 장비 대시보드 **7개 마이크로서비스**
- **Kafka 이벤트 체인** — "손상 탐지 → 보고서 요청 → 보고서 생성"이 도메인 이벤트로 이어지는 구조, **서비스 간 동기 호출 없이** 느슨하게 결합
- **Spring Cloud Gateway 단일 진입점** — 경로 기반 라우팅으로 7개 서비스 + Vue 프론트 통합
- **서비스별 독립 배포** — 서비스마다 Dockerfile·K8s 매니페스트(헬스체크 probe 포함) 개별 구성, **AWS EKS** 배포
- **Istio 서비스 메시** — 사이드카 주입으로 코드 수정 없이 서비스 간 트래픽 제어·관측
- `Java` · `Spring Boot` · `Kafka` · `Istio` · `Kubernetes(EKS)` · `Docker` · `Vue`

### [Bilive — 밴드 합주실 예약 플랫폼](https://github.com/PROFITLAB-HACKATHON-2025/bilive_frontend) · 해커톤
> 밴드 합주실 검색·예약·커뮤니티를 하나로 묶은 모바일 웹앱 · **2025 PROFITLAB 해커톤 출품작 (팀 프로젝트)**

- 지도 기반 합주실 검색과 필터 UI 중심의 모바일 웹앱 MVP 구축
- `React` · `TypeScript`
- 프론트엔드 공개 · 백엔드 비공개

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
