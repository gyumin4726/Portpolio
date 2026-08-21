---
layout: default
class: px-14 pt-10
---

## Project 2. QKD 운용 파라미터 최적화 · SKR 예측

<div class="text-sm text-slate-500 mb-4">
ICT 학점연계 인턴십 · ㈜큐심플러스 (QSimPlus) SW 개발팀 · 2025 Fall · <b>Intern Researcher </b><br/>
<a href="https://github.com/gyumin4726/QKD_OPT">github.com/gyumin4726/QKD_OPT</a>
</div>

### Problem

양자 키 분배(QKD) 시스템의 **보안 키 생성률(SKR)** 은 신호·디코이 강도, 선택 확률 등
다수의 운용 파라미터에 민감하게 의존하며, **거리·채널 환경**이 변할 때마다 반복적인 최적화
계산이 요구됨. 이러한 연산 부담은 **실시간 운용**이나 **저전력·이동형 환경**으로의 확장에 큰 제약.

### Architecture — 4-Stage Pipeline

<div class="grid grid-cols-4 gap-3 pt-3">

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 1</div>
<div class="font-semibold text-slate-900 mt-1">SKR Simulator</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">Decoy-State BB84 유한 키 보안 분석 이론식을 코드로 직접 구현</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 2</div>
<div class="font-semibold text-slate-900 mt-1">GA Optimizer</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">거리별 운용 파라미터 최적화 · Optuna로 GA 하이퍼파라미터 자체도 튜닝</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 3</div>
<div class="font-semibold text-slate-900 mt-1">Dataset Builder</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">GA 최적화 결과를 환경 변수 → 최적 파라미터·SKR 매핑으로 정리한 학습 데이터 구축</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">Stage 4</div>
<div class="font-semibold text-slate-900 mt-1">FT-Transformer</div>
<div class="text-[11px] leading-snug text-slate-600 mt-1">환경 변수만으로 최적 운용 파라미터와 SKR을 직접 예측</div>
</div>

</div>

<div class="text-[13px] leading-relaxed text-slate-500 pt-4">
최적화 대상: 신호·디코이 강도(μ, ν), 상태 선택 확률(p<sub>μ</sub>, p<sub>ν</sub>, p<sub>vac</sub>), 기저 선택 확률(p<sub>X</sub>, q<sub>X</sub>) — 물리적·보안적 제약 조건을 GA·데이터셋·모델 단계 모두에 일관되게 반영. PyTorch · scikit-learn · Optuna.
</div>

---
layout: default
class: px-14 pt-10
---

## Project 2. Role · Outcome

<div class="grid grid-cols-2 gap-10">

<div>

### My Role — **Intern Researcher**

㈜큐심플러스 SW 개발팀의 인턴 연구원으로, 보안 이론 학습부터 시뮬레이터 구현,
최적화 설계, 데이터셋 구축, 딥러닝 모델링까지 **전 과정 수행**.

<div class="pt-2 text-sm">

- **Decoy-State BB84 보안 이론** 학습 및 SKR 계산 코드 직접 구현
- **GA 기반 운용 파라미터 최적화** · GA 자체 하이퍼파라미터 튜닝
- 물리적 제약(Σp = 1, vac ≈ 0 등) 코드 수준 적용 및 검증
- **학습 데이터셋 구축** — 환경 변수 → 최적 파라미터·SKR 매핑
- **다양한 모델** 비교 실험 및 최종 모델 채택
- 거리 조건별 모델 분리 학습 및 성능 분석

</div>

</div>

<div>

### Outcome

<div class="p-5 rounded-lg border border-blue-200 bg-blue-50 mb-4">
<div class="text-xs uppercase tracking-wider text-blue-700 font-semibold">SKR Prediction</div>
<div class="text-2xl font-bold text-slate-900 mt-1">평균 오차율 ~ 2%</div>
<div class="text-sm text-slate-600 mt-1">FT-Transformer · 약 2만 테스트 샘플</div>
</div>

<div class="p-5 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-600 font-semibold">Model Comparison</div>
<div class="text-base font-semibold text-slate-900 mt-1">FT-Transformer &gt; MLP</div>
<div class="text-sm text-slate-600 mt-1">변수 간 상호작용을 self-attention으로 학습 — 오차 분산도 더 안정적</div>
</div>

</div>

</div>

<h3 class="!mt-4">Reflection</h3>

AI를 **반복 최적화의 우회로**로 위치시킨 접근을 양자통신 도메인에서 검증한 프로젝트. AI-only 초기 모델의 한계를 대표님·팀원과 양자통신 이론·장비 특성을 주고받으며 풀어냈고, 모델 정확도보다 **도메인 전문가와의 소통 깊이**가 ML 시스템의 실사용 가치를 가른다는 점, 그리고 협업이 모델 설계만큼 핵심 역량이라는 사실을 분명하게 본 시간.
