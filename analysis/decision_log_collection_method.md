# Data Collection Method Decision Log

> **연구:** LLM-as-Participant  
> **일자:** 2026-03-09  
> **의사결정:** 파일럿 UI 수동 → 본 실험 API 자동화  
> **검증 방법:** 4개 LLM에 동일 질문을 던져 교차 검증 후 연구자가 최종 판단

---

## 쟁점

LLM synthetic persona 인터뷰 데이터를 수집할 때 두 가지 방식이 가능하다:

- **방식 A (UI 수동):** 각 모델의 채팅 UI에서 인코그니토/임시 채팅으로, 연구자가 14턴 질문을 한 턴씩 수동 복붙
- **방식 B (API 자동):** 각 모델의 API를 사용하여 동일 프롬프트 + 질문을 자동 전송, 로그 자동 저장

---

## 검토에 사용한 모델

| 모델 | 역할 |
|------|------|
| Claude Opus 4.6 (본 프로젝트 세션) | 초기 설계 논의 + 최종 종합 |
| Claude Opus 4.6 (별도 세션) | 독립 검토 |
| GPT-5.4 | 독립 검토 |
| Gemini 3.1 Pro | 독립 검토 |

동일한 연구 맥락 설명 + 6개 질문(동치성, 환경 차이, 대칭성, 재현성, 실용 권장, 하이브리드 접근)을 4모델에 제시하고 답변을 비교했다.

---

## 4모델 답변 종합

### 전원 일치 (4/4)

| 쟁점 | 합의 |
|------|------|
| UI vs API 동치성 | 동치가 아니다. 동일 텍스트를 넣어도 hidden system prompt, safety filter, temperature 등 실행 컨텍스트가 다르다. |
| 재현성 | API가 압도적으로 유리. 파라미터 고정, 로그 자동 저장, 코드 자체가 프로토콜 기록. |
| 본 실험 방식 | API 권장. |
| 파일럿 방식 | UI 수동 허용. 탐색적 단계이므로 ROI가 높다. |

### 다수 일치 (3/4)

| 쟁점 | Opus (×2) + GPT | Gemini |
|------|------------------|--------|
| 하이브리드 접근 (UI + API 병행) | 타당. API primary + UI robustness check가 방어력 최고 | 반려. 환경이 달라서 크로스체크 자체가 논리적 모순 |

### 주요 차이점

| 쟁점 | 모델별 차이 |
|------|------------|
| limitation 처리 충분성 | Opus/GPT: CHI LBW면 limitation으로 충분 / Gemini: limitation만으로는 리젝 위험 |
| 비교 조건 대칭성 | Opus/GPT: 프로토콜 대칭(동일 문항·순서·probe 규칙)으로 방어 가능 / Gemini: probing 없는 건 인터뷰가 아니라 설문지 |

---

## 연구자 판단

### Gemini의 반론에 대한 반박

**하이브리드 반려 주장:** "환경이 달라서 크로스체크가 성립 안 한다"는 건 과한 주장이다. 환경이 다른데도 pain point 수준에서 동일한 결과가 나온다면, 그 자체가 robustness의 증거가 된다. HCI 논문에서 실제로 쓰이는 패턴이다.

**"설문지 아니냐" 비판:** structured interview로 고정한 것은 의도된 설계다. probing을 넣으면 실제 유저 인터뷰의 probing과 LLM 인터뷰의 probing을 통제해야 하는 새로운 변수가 생긴다. 논문에서 "semi-structured가 아닌 structured interview를 채택한 이유"로 framing하면 방어 가능.

### GPT의 기여

**"primary target을 먼저 명시해라":** 이 연구가 "consumer-facing LLM products의 페르소나 연기"를 보는 건지, "모델 자체의 synthetic persona 능력"을 보는 건지에 따라 UI/API 선택의 정당화가 달라진다. 본 연구는 후자에 가까우므로 API primary가 논리적으로 맞다.

**"매체 대칭이 아니라 프로토콜 대칭으로 방어하라":** 동일 문항, 동일 순서, 동일 probe 규칙, 동일 종료 규칙을 명시하면 "사람 vs agent" 비판은 방어 가능. 이미 현재 설계에 반영되어 있다.

---

## 최종 결정

| 단계 | 방식 | 이유 |
|------|------|------|
| 파일럿 6세션 | UI 수동 (인코그니토/임시 채팅) | 프롬프트 디버깅 + 모델 선정 + 감각 파악. 6세션이라 수동이 더 빠름 |
| 파일럿 추가 1~2세션 | 선정 모델로 API도 실행 | UI vs API 차이 quick check. pain point 수준에서 유의미한 차이 있는지 확인 |
| 본 실험 8페르소나 | API 자동 (temperature/seed 고정 + full log) | 재현성 + 통제 + 효율. 논문 methodology의 핵심 근거 |

### 논문 framing 방향

- **프로토콜 대칭성:** "실제 유저와 LLM 페르소나 모두 동일한 structured interview protocol(14문항, 고정 순서, probing 금지)로 진행"
- **수집 환경:** "파일럿은 각 모델의 채팅 UI에서 수동 수행. 본 실험은 재현성 확보를 위해 API로 전환하였으며, 파라미터(model version, temperature, seed)를 명시적으로 고정"
- **UI vs API 차이:** "파일럿에서 UI/API 교차 실행을 통해 pain point 수준의 방향성 일치를 확인"
- **limitation:** "채팅 UI와 API의 hidden system prompt, safety filter 차이는 표현 방식(톤, 길이)에 영향을 줄 수 있으나, pain point 발견 여부에는 유의미한 차이가 없었음을 파일럿에서 확인"

---

## 메타 노트

이 의사결정 과정 자체가 본 연구의 주제("LLM을 어디까지 신뢰할 수 있는가")와 맥락적으로 일치한다. 4개 LLM의 답변을 비판적으로 교차 검증하여 연구자가 최종 판단을 내리는 프로세스는, LLM을 독립적 의사결정자가 아닌 "비판적으로 활용하는 연구 도구"로 포지셔닝하는 본 연구의 철학을 반영한다.
