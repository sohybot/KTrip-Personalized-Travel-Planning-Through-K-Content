# KTrip: AI 기반 K-Culture 여행 큐레이션 플랫폼

"화면 속 동경이 현실의 여정이 되는 곳, 개인화 AI 여행 비서 KTrip"

KTrip은 사용자의 취향을 분석하여 최적의 K-콘텐츠 촬영지 여행 경로를 추천하고,
여행 중 마주치는 복잡한 한국 메뉴판을 OCR과 LLM을 결합한 기술로 분석해
외국인 관광객도 현지인처럼 여행할 수 있도록 돕는 AI 기반 여행 서비스입니다.

### 소개영상

[![KTrip Demo Video](https://img.youtube.com/vi/HGWrB3Ykbjk/hqdefault.jpg)](https://youtu.be/HGWrB3Ykbjk)

> Click the image to watch the full demo video.

---

## 기획 배경

- K-POP, 드라마, 예능, 영화 등 K-미디어의 글로벌 확산
- 한류 콘텐츠가 실제 방한 관광 수요로 전환
- 외국인 관광객의 개별 자유여행(FIT) 증가
- 여행 과정에서 발생하는 언어 장벽과 정보 탐색 비용 문제

단순한 정보 제공이 아닌,
콘텐츠 취향을 이해하고 기술로 장벽을 해결하는 맞춤형 여행 가이드가 필요하다고 판단했습니다.

---

## 서비스 핵심 가치

- 콘텐츠 중심 여행: 장소가 아닌 스토리와 취향 중심
- 언어·문화 장벽 최소화
- 여행 로그 기반 데이터 선순환 구조

---

## 주요 기능

### 기능구현현영상 

[![Feature Implementation Video](https://img.youtube.com/vi/hYW3b9-TB9M/hqdefault.jpg)](https://youtu.be/hYW3b9-TB9M)
> Click the image to watch the full demo video.
> 
### 1. 지능형 메뉴판 분석 (OCR + LLM)

- Azure Document Intelligence를 활용한 메뉴판 OCR 및 좌표 데이터 추출
- GPT 계열 모델을 활용해 파편화된 텍스트를 의미 단위로 재구성
- 단순 번역을 넘어 재료 설명, 맵기 정보 등 부가 정보 자동 생성

 <img width="208" height="786" alt="image" src="https://github.com/user-attachments/assets/d3fecd56-02f9-4917-80d0-7e26084e85de" />

---

### 2. RAG 기반 맞춤 여행 경로 추천

- 사용자 설문을 통한 취향 분석
- K-콘텐츠 촬영지, 맛집, 관광지 데이터베이스 활용
- RAG 4단계 파이프라인
  1. 키워드 추출
  2. DB 검색
  3. 관련도 점수 계산 및 정렬
  4. JSON 형식 일정 생성

<img width="237" height="574" alt="image" src="https://github.com/user-attachments/assets/73e1fc4e-aa04-4b40-ae49-72ee55417938" />
<img width="234" height="574" alt="스크린샷 2025-12-24 180705" src="https://github.com/user-attachments/assets/c6be9161-731b-44ba-afcb-d9b099d2df07" />
<img width="242" height="525" alt="image" src="https://github.com/user-attachments/assets/1d161a5b-f3d4-464a-8250-5c87aeb90a69" />
<img width="234" height="269" alt="image" src="https://github.com/user-attachments/assets/9af49f1e-f1d1-4afe-8340-ec11e8e8492c" />


---

### 3. 여행 로그 및 소셜 포스터 생성

- 방문 장소 및 이동 경로 자동 기록
- 한국적인 감성의 디자인 템플릿 제공
- SNS 공유용 여행 포스터 자동 생성

<img width="206" height="620" alt="image" src="https://github.com/user-attachments/assets/9cdd70da-464f-463e-9bec-4bdd1f9bbd65" />
<img width="206" height="620" alt="image" src="https://github.com/user-attachments/assets/8fee3cf0-d4aa-45fc-a17b-4a1d7126d85b" />
<img width="206" height="620" alt="image" src="https://github.com/user-attachments/assets/68b5c70b-2707-436c-8989-0393c3faf434" />
<img width="206" height="620" alt="image" src="https://github.com/user-attachments/assets/fa2c19f5-8d6f-4de2-905e-cd019deebba1" />

---

## 기술적 챌린지 및 해결

### OCR 자간 문제 해결

문제:
- 메뉴판 디자인 특성상 OCR이 "우  동", "김 치"처럼 단어를 분리 인식
- 이로 인해 번역 품질 및 메뉴 인식 정확도 저하

해결:
- 텍스트의 Y좌표 근접도를 활용해 같은 행의 글자를 병합
- 공간 좌표 정보를 LLM 프롬프트에 주입하여 의미 단위로 재구성
<img width="503" height="557" alt="image" src="https://github.com/user-attachments/assets/dd9bd48f-d3cc-47ff-95b1-9aa6b2f5fc65" />


---

### RAG 컨텍스트 구조화

문제:
- 초기에는 단순 텍스트 형태로 장소 정보를 전달
- LLM이 위치 정보나 콘텐츠 연관성을 정확히 파악하지 못함

해결:
- 장소명, 관련 콘텐츠, 좌표, 특징을 Key-Value 기반의 구조화된 컨텍스트로 변환
- LLM이 정확한 정보 기반으로 동선을 설계하도록 개선
<img width="700" height="230" alt="image" src="https://github.com/user-attachments/assets/3a6a49da-510f-4f66-9ec3-8fb58dd507f2" />



---

### 4-Tier 시스템 아키텍처

- Client / Backend / AI Service / Storage 계층 분리
- 대용량 이미지 데이터는 Blob Storage
- 정형 텍스트 데이터는 SQLite에 저장

<img width="1638" height="480" alt="image" src="https://github.com/user-attachments/assets/8981660e-c830-4285-89fb-c6b6f25e54d9" />


---

## LLM 모델 비교 및 선택

### 비교 기준

- 비용
- 응답 속도
- 답변 품질
- 토큰 효율성

### 모델 비교

| 모델 | 장점 | 단점 | 채택 여부 |
|---|---|---|---|
| GPT-4 | 최고 수준의 응답 품질 | 높은 비용, 느린 속도 | 미채택 |
| GPT-5-mini | 매우 빠른 응답 | 토큰 사용량이 많아 비용 증가 | 미채택 |
| GPT-4o-mini | 비용 대비 안정적인 품질, 토큰 효율 우수 | 최고급 품질은 아님 | 채택 |

KTrip은 비용, 속도, 품질의 균형이 가장 적절한 GPT-4o-mini를 메인 모델로 선택했습니다.

이미지 삽입 위치:
- LLM 모델 비교 그래프
<img width="840" height="661" alt="image" src="https://github.com/user-attachments/assets/a47b108f-9f36-4c3b-bcd8-d77e12437587" />

---

## 기술 스택

| 영역 | 기술 |
|---|---|
| Frontend | Vanilla JS, MediaDevices API |
| Backend | FastAPI, Uvicorn, SQLAlchemy |
| AI | Azure OpenAI (GPT-4o-mini), Azure Document Intelligence |
| Infra | Azure App Service, Azure Blob Storage |
| Database | SQLite |
<img width="885" height="333" alt="image" src="https://github.com/user-attachments/assets/26156e7c-6ab0-401d-9f33-591cfaa073c1" />

---

## 프로젝트 구조

```bash
KTrip/
├── backend/
│   └── app/
│       ├── main.py      # API 컨트롤 타워
│       ├── ocr.py       # OCR 처리 로직
│       └── llm.py       # LLM 정제 및 추천 로직
├── frontend/
└── data/                # K-콘텐츠 장소 데이터
```
<img width="886" height="391" alt="project-structure" src="https://github.com/user-attachments/assets/fa95a337-f68b-4352-acf9-b49157680d83" />
