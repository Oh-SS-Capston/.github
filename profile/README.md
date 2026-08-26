# Oh! SS

> **정적 분석과 로컬 오픈웨이트 LLM을 결합하여 오픈소스 Repository의 구조·Public API·개발 규칙·라이선스와 근거를 자동 분석하는 개발자 온보딩 플랫폼**

Oh! SS는 GitHub Repository를 분석하여 **Repository 구조, 클래스 및 코드 관계, Public API, 개발 규칙, 라이선스 정보와 Evidence**를 구조화하고 시각화합니다.

Oh! SS는 Repository 전체를 LLM에게 직접 전달하여 추측하도록 하지 않습니다. 먼저 **JavaParser·ASM 기반 정적 분석과 Graph 분석을 통해 코드에서 확인 가능한 사실 정보를 추출하고**, 구조화된 분석 결과를 **로컬 Ollama 기반 Qwen3.5 9B**가 개발자가 이해하기 쉬운 설명으로 변환합니다.

🌐 **Demonstration video:** https://youtu.be/IeMdvZ4GfUI?si=mKXN8fdu1FQaGOI3

<p align="center">
  <img src="./assets/example.png" alt="Oh! SS Full screen" width="1000">
</p>

---

## Why Oh! SS?

새로운 오픈소스 프로젝트에 참여하는 개발자는 코드를 수정하기 전에 다음 정보를 직접 파악해야 합니다.

* Repository 및 디렉터리 구조
* 주요 Package·Class·Method
* 클래스 및 코드 요소 사이의 관계
* 외부에 노출되는 Public API
* 프로젝트 내부 개발 규칙
* 적용된 오픈소스 라이선스
* 분석 결과를 뒷받침하는 실제 코드 및 문서 근거

Repository 규모가 커질수록 이러한 정보를 여러 소스 파일과 문서에서 직접 파악하는 데 많은 시간이 필요합니다.

Oh! SS는 이러한 초기 탐색 과정을 자동화하여 **Repository의 구조와 개발 맥락을 정형화된 분석 산출물로 생성하고, 사용자가 이를 웹에서 탐색할 수 있도록 지원합니다.**

---

# 주요 기능

## 1. Repository 분석

GitHub Repository URL 또는 `owner/repository` 형식으로 분석을 실행합니다.

* Repository 분석 실행
* 분석 단계별 상태 확인
* 최근 분석 내역 조회
* 기존 Repository 재분석
* 분석 산출물 조회

---

## 2. 코드 구조 탐색

분석된 Repository의 구조를 계층적으로 제공합니다.

* Repository 기본 정보
* Directory
* Package
* Class
* Method
* 코드 요소 간 관계

---

## 3. 클래스 관계 및 서브시스템 분석

추출된 코드 관계를 Graph로 구성하여 클래스 및 서브시스템 구조를 탐색할 수 있도록 합니다.

* Class Diagram
* Class Map
* 코드 요소 간 Relationship
* Subsystem 단위 구조 탐색

Graph 기반 구조 분석에는 Leiden Network Analysis를 활용합니다.

---

## 4. Public API 분석

Repository의 Public API 정보를 분석합니다.

* Public API 탐색
* 관련 Class / Method
* API 관련 코드 정보
* 관련 Evidence 조회

---

## 5. Rule & Evidence 분석

프로젝트에서 확인되는 개발 규칙과 관련 근거를 분석합니다.

Oh! SS는 단순한 생성 결과뿐 아니라 가능한 경우 해당 판단과 연결되는 실제 코드 또는 문서 정보를 함께 제공합니다.

```text
Analysis Result
      │
      └── Evidence
            ├── Source File
            ├── Code Location
            └── Related Document
```

---

## 6. AI 기반 분석 설명

Oh! SS의 기본 LLM Provider는 **Ollama**이며, 기본 모델은 **Qwen3.5 9B**입니다.

분석 과정은 다음과 같습니다.

```text
Repository
    ↓
Static Analysis
    ↓
Structured Result
    ↓
Evidence
    ↓
Qwen3.5 9B
    ↓
Developer-oriented Explanation
```

LLM은 Repository 구조를 임의로 생성하는 것이 아니라, 앞선 분석 Pipeline에서 생성된 구조화 정보를 기반으로 설명을 생성합니다.

LLM Scenario 생성에서는 서버가 분석 결과를 기반으로 Scenario의 골격을 먼저 구성하고, 모델은 해당 구조의 설명 필드를 생성하도록 제한하여 분석 근거와 생성 결과의 연결을 유지합니다.

---

## 7. 라이선스 분석

Repository의 오픈소스 라이선스 관련 정보를 분석합니다.

* License 식별
* 주요 License Metric
* Evidence 조회
* Evidence 검색 및 출처 필터
* Review Checklist
* Markdown / JSON Report

> Oh! SS의 라이선스 분석 결과는 법률 자문이 아니며, 개발자의 오픈소스 라이선스 검토를 지원하기 위한 정보입니다.

---

## 8. GitHub Repository 통계

GitHub Repository의 활동 정보를 시각화합니다.

* Star 변화
* Issue 활동
* Release 정보
* Repository 주요 지표

---

# Analysis Architecture

```text
GitHub Repository
        │
        ▼
Repository Collection
        │
        ▼
Source / Build Analysis
        │
        ▼
Static Analysis
(JavaParser / ASM)
        │
        ▼
Symbol & Relationship Extraction
        │
        ▼
Graph Construction
        │
        ▼
Structure Analysis
        │
        ├── Directory Structure
        ├── Class Relationships
        ├── Public API
        ├── Rules & Evidence
        └── License Information
        │
        ▼
Structured Analysis Artifacts
        │
        ▼
Ollama
(Qwen3.5 9B)
        │
        ▼
LLM-generated Documentation
        │
        ▼
Oh! SS Web Interface
```

<p align="center">
  <img src="./assets/architecture.png" alt="Oh! SS Architecture" width="1000">
</p>

---

# 핵심 기술적 접근

## Static Analysis First

Oh! SS는 LLM 분석 전에 코드에서 확인 가능한 정보를 먼저 추출합니다.

Java Repository 분석에는 다음 기술을 활용합니다.

* JavaParser Symbol Solver
* ASM

이를 통해 Source 및 Bytecode 수준에서 코드 구조와 관계 정보를 분석합니다.

---

## Graph-based Structure Analysis

추출된 Symbol과 Relationship을 Graph 형태로 구성하고 Repository의 구조적 관계 분석에 활용합니다.

Graph 분석 결과는 Class Map 및 Subsystem 분석 등의 기반 데이터로 사용됩니다.

---

## Evidence-grounded Analysis

분석 결과가 어떤 Source 또는 문서 정보에서 도출되었는지 확인할 수 있도록 Evidence 정보를 연결합니다.

이는 LLM이 생성한 설명의 기반 데이터를 사용자가 다시 원본 Repository에서 확인할 수 있도록 하기 위한 구조입니다.

---

## Local Open-weight LLM

Oh! SS의 기본 LLM 실행 환경은 외부 상용 API가 아니라 **Ollama 기반 로컬 모델 실행**입니다.

기본 모델:

```text
Qwen3.5 9B
```

Docker Compose 환경에서는 Ollama 서비스와 모델 초기화 서비스가 함께 구성되며, 최초 실행 시 모델을 내려받은 뒤 Backend가 실행됩니다.

Qwen3.5 9B는 Apache License 2.0으로 공개된 모델입니다.

---

## Reproducible LLM Generation

LLM 생성 설정에서는 고정 Seed를 지원하여 동일 입력에 대한 모델 출력 변동을 줄일 수 있도록 구성합니다.

또한 Scenario 생성은 전체 내용을 모델에게 자유 생성시키지 않고, Backend가 먼저 Scenario 골격을 생성한 후 모델이 설명 필드를 보완하는 방식으로 구성합니다.

---

# 기술 스택

## Frontend

| 영역                  | 기술                  |
| ------------------- | ------------------- |
| Framework           | React 19            |
| Routing             | React Router DOM 7  |
| Build               | Vite 7              |
| Styling             | Tailwind CSS 4      |
| Graph Visualization | React Flow          |
| Graph Layout        | Dagre               |
| Icons               | Lucide React        |
| Payment             | PortOne Browser SDK |

## Backend

| 영역                | 기술                             |
| ----------------- | ------------------------------ |
| Language          | Java 21                        |
| Framework         | Spring Boot 4                  |
| Database          | PostgreSQL                     |
| ORM               | Spring Data JPA                |
| Query             | QueryDSL                       |
| Static Analysis   | JavaParser Symbol Solver       |
| Bytecode Analysis | ASM                            |
| Graph Analysis    | Leiden Network Analysis        |
| Cache             | Redis                          |
| Storage           | AWS S3                         |
| API Documentation | SpringDoc OpenAPI              |
| Authentication    | Spring Security / OAuth2 / JWT |

## AI

| 영역                | 기술         |
| ----------------- | ---------- |
| Local LLM Runtime | Ollama     |
| Default Model     | Qwen3.5 9B |
| Model License     | Apache-2.0 |
| Optional Provider | Claude     |

## Infrastructure

* Docker
* Docker Compose
* GitHub Actions
* AWS

---

# Repository

## Frontend

https://github.com/Oh-SS-Capston/FE

사용자 인터페이스와 분석 결과 탐색 및 시각화를 담당합니다.

## Backend / Analysis Engine

https://github.com/Oh-SS-Capston/BE

Repository 분석 Pipeline, LLM Pipeline 및 Backend API를 담당합니다.

---

# Local Development

## Frontend

```bash
git clone https://github.com/Oh-SS-Capston/FE.git
cd FE

npm install
npm run dev
```

기본 Backend 주소:

```text
http://localhost:8080
```

필요한 경우:

```env
VITE_API_BASE_URL=http://localhost:8080
```

Production Build:

```bash
npm run build
```

---

## Backend

### Requirements

* Java 21
* PostgreSQL
* Docker / Docker Compose 권장

Repository Clone:

```bash
git clone https://github.com/Oh-SS-Capston/BE.git
cd BE
```

### Docker Compose

* Backend Application
* Redis
* Ollama
* Qwen3.5 9B model initialization

```bash
docker compose up --build
```

기본 Application 주소:

```text
http://localhost:8080
```

Swagger UI:

```text
http://localhost:8080/swagger-ui/index.html
```

> PostgreSQL 연결과 Google OAuth, AWS 등의 환경 변수는 별도로 설정해야 합니다.

### Direct Run

Windows:

```powershell
.\gradlew.bat bootRun
```

macOS / Linux:

```bash
./gradlew bootRun
```

### Test

Windows:

```powershell
.\gradlew.bat clean test
```

macOS / Linux:

```bash
./gradlew clean test
```

---

# Known Limitations

현재 구현에서 확인된 주요 제약은 다음과 같습니다.

* 로컬 Qwen3.5 9B 기반 LLM 단계는 CPU/실행 환경에 따라 상당한 시간이 필요할 수 있습니다.
* LLM 실행 중 단일 Worker가 장시간 점유되어 후속 Job이 대기할 수 있습니다.
* 일부 Scenario Evidence에서 내부 Evidence ID가 표시되지 않을 수 있습니다.
* Qwen3.5 9B 실행을 위해 충분한 Memory가 필요합니다.

이러한 항목은 분석 결과의 정확성과 Repository 구조 분석 자체에는 영향을 주지 않는 범위에서 향후 개선할 예정입니다.

---

# Open Source & License

Oh! SS 자체 Source Code는 **Apache License 2.0**으로 배포합니다.

주요 오픈소스 구성 요소와 모델은 각 원 저작자의 라이선스를 따릅니다.

주요 AI 구성:

| Component  | Role              | License        |
| ---------- | ----------------- | -------------- |
| Ollama     | Local LLM Runtime | 해당 프로젝트 원 라이선스 |
| Qwen3.5 9B | Default LLM       | Apache-2.0     |

세부 외부 의존성 정보는 각 Repository의 `THIRD_PARTY_LICENSES.md`에서 관리합니다.

---

# Contributing

```text
Issue
  ↓
Feature / Fix Branch
  ↓
Implementation
  ↓
Test
  ↓
Pull Request
  ↓
develop
```

---

# License

Oh! SS source code is licensed under the **Apache License 2.0**.

Third-party libraries, runtimes, and AI models remain subject to their respective licenses.

For details, see the `LICENSE` and `THIRD_PARTY_LICENSES.md` files in the Frontend and Backend repositories.

