---
layout: section
---

# Projects

End-to-End AI Systems

---
layout: default
class: px-14 pt-10
---

## Project 1. TEP 화학공정 이상 감지 · 복구 시스템

<div class="text-sm text-slate-500 mb-4">
UNITEF AI Application Proficiency Program · 2025 Summer · <b>4인 팀 · Team Lead</b><br/>
<a href="https://github.com/gyumin4726/Team-3---AI-Career-Path">github.com/gyumin4726/Team-3---AI-Career-Path</a>
</div>

### Problem

Tennessee Eastman Process(TEP) — **52개 센서**(공정 측정 22 / 분석 19 / 제어 11)로 모니터링되는 화학 공정에서
**13종의 fault** 를 실시간 감지하고, 제어 변수를 조정하여 **정상 상태로 자율 복구**하는 시스템 구축.
산업 데이터 특유의 시계열 비선형성과 fault 별 패턴 다양성이 핵심 난점.

### Architecture — 4-Stage Closed-Loop Pipeline

<div class="grid grid-cols-4 gap-3 pt-3">

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 1</div>
<div class="font-semibold text-slate-900 mt-1">GAN Detector</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">LSTM Generator + CNN1D2D Discriminator로 fault 감지 · 13종 분류</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 2</div>
<div class="font-semibold text-slate-900 mt-1">KNN Corrector</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">정상 상태 데이터와 매칭하여 제어 변수(11차원) 보정값 산출</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 3</div>
<div class="font-semibold text-slate-900 mt-1">TCN-Seq2Seq</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">보정된 제어 입력으로부터 응답 변수(41차원) 시계열 예측</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 4</div>
<div class="font-semibold text-slate-900 mt-1">Validation</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">Stage 1 재적용으로 정상 여부 재판정</div>
</div>

</div>

<div class="text-[13px] leading-relaxed text-slate-500 pt-4">
Closed-loop 구조 — Stage 4에서 fault가 남아 있으면 <b>Stage 2~4를 최대 3회 반복</b>하여 점진 보정. Stage 1이 처음부터 정상으로 판정하면 조기 종료.<br/>
Sliding window (length 50, step 10) 로 960 timestep을 4,600+ 학습 샘플로 확장. PyTorch · Streamlit UI · Gemini API 기반 LLM 설명층 포함.
</div>

---
layout: default
class: px-14 pt-10
---

## Project 1. Role · Outcome

<div class="grid grid-cols-2 gap-10">

<div>

### My Role — **Team Lead**

**팀의 리더**로 시스템 아키텍처 설계와 4단계 파이프라인 통합을 주도.
핵심 모델 구현부터 설명 가능한 LLM 결합, 데모 인터페이스 구축까지 기술 영역 전반을 직접 수행.

<div class="pt-2 text-sm">

- 전체 **파이프라인 아키텍처 설계** 및 4단계 통합
- **GAN Detector (Stage 1)** 설계 및 학습
- **TCN-Seq2Seq (Stage 3)** 모델링
- **Validation Loop (Stage 4)** 반복 보정 로직 구현
- **LLM 설명층** 통합 — 운영자용 자연어 리포트
- **Streamlit UI** 및 데모 구성

</div>

</div>

<div>

### Outcome

<div class="p-5 rounded-lg border border-blue-200 bg-blue-50 mb-4">
<div class="text-xs uppercase tracking-wider text-blue-700 font-semibold">최우수상 수상</div>
<div class="text-lg font-bold text-slate-900 mt-1">UNITEF AI Application<br/>Proficiency Program</div>
</div>

<div class="p-5 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-600 font-semibold">수상 혜택</div>
<div class="text-lg font-bold text-slate-900 mt-1">싱가포르 견학</div>
<div class="text-sm text-slate-600 mt-1">우승팀 대상 단기 해외 연수</div>
</div>

</div>

</div>

### Reflection

이질적인 네 모델을 하나의 closed-loop으로 엮어내는 과정에서, 시스템 신뢰도는 *"어떤 모델이 더 정확한가"* 가 아니라
*"모듈을 어떻게 잇고, 실패에서 어떻게 회복시키는가"* 에서 갈린다는 걸 직접 마주함.
**모델 단위에서 파이프라인 단위로 시각이 옮겨간 프로젝트**이자, 정확도 추격에서 시스템 흐름 설계로 사고의 무게중심이 옮겨간 시간.
