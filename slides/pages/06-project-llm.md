---
layout: default
class: px-14 pt-10
---

## Project 3. Imperfect Human-in-the-Loop 영향 분석 — LLM·DRL 자율주행

<div class="text-sm text-slate-500 mb-4">
R&Dix · PhysAI Team Project · 2025 · Experiment 4<br/>
<a href="https://github.com/gyumin4726/SAFE_RL">github.com/gyumin4726/SAFE_RL</a>
</div>

### Motivation & Problem

**RLHF**(Reinforcement Learning from Human Feedback) 와 **HITL**(Human-in-the-Loop) 은 현재 강화학습 분야의
가장 활발한 연구 주제 중 하나. 그러나 대부분의 기존 접근은 인간의 입력을 암묵적으로 *'정답(Ground Truth)'*
으로 간주해 왔으며, 실제 사용자는 판단 오류 · 무작위에 가까운 개입을 빈번하게 발생시킨다는 현실과는 거리가 있음.

본 실험의 목표는 **불완전한 인간 개입이 LLM · DRL 협력 시스템의 안전성과 학습 안정성에 미치는 영향**을 정량적으로
분석함으로써, 이러한 HITL 가정의 타당성을 재검토하는 것.

---
layout: default
class: px-14 pt-10
---

## Project 3. Setup — 두 의사결정 구조의 비교

### Why LLM in the Loop?

순수 RL은 고수준 상황 판단과 학습 효율에서 한계가 있고, HITL은 인간 개입의 정합성을 보장하기 어려움.
LLM은 다음 세 측면에서 두 구조의 약점을 보완.

<div class="grid grid-cols-3 gap-3 pt-2">

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900 text-sm">상황 추론 보조</div>
<div class="text-[12px] leading-snug text-slate-600 mt-1">차량 의도·도로 맥락 같은 고수준 판단을 LLM의 world knowledge로 보완</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900 text-sm">안전 추론 · 설명(XAI)</div>
<div class="text-[12px] leading-snug text-slate-600 mt-1">행동의 안전성 근거를 자연어로 제시 — 인간 신뢰성 확보의 기반</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900 text-sm">샘플 효율</div>
<div class="text-[12px] leading-snug text-slate-600 mt-1">LLM의 사전 지식이 RL 탐색 공간을 축소하여 학습 가속</div>
</div>

</div>

### 두 의사결정 구조

<div class="grid grid-cols-2 gap-4 pt-3">

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">System A</div>
<div class="font-semibold text-slate-900 mt-1">LLM + RL Agent</div>
<div class="text-[12px] leading-snug text-slate-600 mt-2">
LLM이 상황을 분석하여 안전한 행동을 제안 → RL 에이전트가 실제 제어 수행.
LLM과 에이전트의 협력만으로 자율주행 정책을 학습.
</div>
</div>

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-500">System B</div>
<div class="font-semibold text-slate-900 mt-1">LLM + RL Agent + Imperfect Human</div>
<div class="text-[12px] leading-snug text-slate-600 mt-2">
A의 구조에 <b>최적이 아닌(불완전한) 인간 개입</b>을 추가. 잘못된 판단·무작위 개입이
시스템 의사결정에 결합되는 하이브리드 구조의 성능을 분석.
</div>
</div>

</div>

<div class="text-[13px] leading-relaxed text-slate-500 pt-4">
Base framework: SafeHiL-RL (SAC + LLM Safety Explainer + FDPF 기반 권한 할당). Simulator: SMARTS highway scenario. 평가 지표: 평균 보상 · 성공률 · 충돌 · Off-Road. PyTorch.
</div>

---
layout: default
class: px-14 pt-10
---

## Project 3. Results · Reflection

### Results — Epoch 820 기준 비교

<div class="text-sm">

| System | Avg Reward | Avg Steps | Success | Collision | Off-Road |
|---|---|---|---|---|---|
| LLM + RL Agent | **+0.51** | 240.3 | **8 / 10** | 2 | **0** |
| LLM + RL Agent + Imperfect Human | −4.90 | 20.5 | 0 / 10 | 3 | 7 |

</div>

<div class="grid grid-cols-2 gap-6 pt-5">

<div>

### Key Findings

- **LLM + RL 협력 구조 자체는 안정적 정책 학습** — 후반 epoch에서 일관된 고성능 도달
- **불완전한 인간 개입이 추가될 경우 성능 급격히 저하** — 충돌 · Off-Road 빈도 증가
- 인간 개입이 곧 *'정답(Ground Truth)'* 이라는 전통적 HIL 가정의 한계를 정량적으로 확인

</div>

<div>

### Reflection

인간 개입을 무비판적으로 신뢰하는 HIL 설계가 오히려 시스템 안전성을 저해할 수 있음을 정량적으로 보인 실험.
인간을 **정답이 아닌 잠재적 노이즈 소스로 가정**하고, LLM의 판단으로 필터링하거나 권한 할당을 동적으로 조정하는
**검증 기반 HIL 설계 원칙**의 필요성을 체득.

</div>

</div>
