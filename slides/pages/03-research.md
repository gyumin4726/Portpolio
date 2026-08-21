---
layout: section
---

# Research

ECCV 2026 Submission · Under Review

---
layout: default
class: px-14 pt-10
---

## Selective Scanning with Mixture-of-Experts <br/> for Few-Shot Class-Incremental Learning

<div class="text-sm text-slate-500 mb-5">
Park G, Yoon S — ECCV 2026 (Under Review) · HCI Lab, Kookmin University<br/>
Advisor: Prof. Sangmin Yoon
</div>

### Problem

Few-Shot Class-Incremental Learning(FSCIL)에서 모델은 적은 데이터로 새 클래스를 점진적으로 학습해야 하지만,
기존에 학습된 표현이 무너지는 **catastrophic forgetting** 이 발생한다.
기존 접근은 prompt pool 확장이나 memory buffer 증대 등 **모델 복잡도를 키우는 방향**으로 문제를 우회해 왔다.

### Approach — SS-MoE

단일 고정 아키텍처 내에서 **선택적 적응(selective adaptation)** 을 수행하는 FSCIL 프레임워크.

<div class="grid grid-cols-3 gap-4 pt-4">

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900">VMamba Backbone</div>
<div class="text-sm text-slate-600 mt-1">선형 시간 복잡도의 state-space 시각 인코더. Attention의 quadratic cost 회피.</div>
</div>

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900">Spatial Router</div>
<div class="text-sm text-slate-600 mt-1">2D feature map의 공간 위치별 라우팅 신호 집계 — Linear Router 대비 우수.</div>
</div>

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900">SS2D Experts</div>
<div class="text-sm text-slate-600 mt-1">입력 의존적(state-dependent) 업데이트를 수행하는 4개의 전문가 모듈.</div>
</div>

</div>


---
layout: default
class: px-14 pt-8
---

## State-of-the-Art Comparison — CUB-200

<div class="text-sm text-slate-500 mb-3">
주요 카테고리별 최고 성능 방법과 비교. Average Accuracy (AA) 기준.
</div>

<div class="text-sm">

| Category | Method | Venue | Backbone | AA |
|---|---|---|---|---|
| Backbone tuning | LDC | TPAMI '23 | ResNet-18 | 68.32 |
| Prototype tuning | SAVC | CVPR '23 | ResNet-18 | 69.35 |
| Dynamic structure | DSN | TPAMI '22 | ResNet-18 | 71.02 |
| PEFT (ViT) | ASP | ECCV '23 | ViT-B/16 | 83.83 |
| **PEFT (ViT) — prior SOTA** | **SEC-Prompt** | **CVPR '25** | **ViT-B/16** | **84.87** |
| **Ours — New SOTA** | **SS-MoE** | **ECCV '26 (UR)** | **VMamba-B** | **84.97** |

</div>

<div class="grid grid-cols-3 gap-4 pt-6">

<div class="p-4 rounded-lg border border-blue-200 bg-blue-50">
<div class="text-xs uppercase tracking-wider text-blue-700 font-semibold">New SOTA</div>
<div class="text-2xl font-bold text-slate-900 mt-1">84.97 AA</div>
<div class="text-xs text-slate-600">CUB-200, VMamba-B</div>
</div>

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-600 font-semibold">vs SEC-Prompt</div>
<div class="text-2xl font-bold text-slate-900 mt-1">+0.10 AA</div>
<div class="text-xs text-slate-600">선형 복잡도 백본 활용</div>
</div>

<div class="p-4 rounded-lg border border-slate-200 bg-slate-50">
<div class="text-xs uppercase tracking-wider text-slate-600 font-semibold">vs ResNet SOTA</div>
<div class="text-2xl font-bold text-slate-900 mt-1">+15.62 AA</div>
<div class="text-xs text-slate-600">vs SAVC (69.35)</div>
</div>

</div>

---
layout: default
class: px-14 pt-10
---

## Ablation & Key Contribution

### Component-wise Ablation (CUB-200)

각 구성요소가 정확도(AA) 와 성능 하락폭(PD) 에 미치는 영향을 분리 검증.

| Configuration | AA ↑ | PD ↓ |
|---|---|---|
| VMamba + ETF (no router, no experts) | 76.56 | 13.00 |
| + 1 SS2D expert (no routing) | 82.88 | 8.06 |
| **+ Spatial Router + 4 Experts (Full SS-MoE)** | **84.97** | **6.97** |

<div class="text-sm text-slate-500 pt-1">
백본만 사용했을 때 76.56 AA → 제안 구성요소 결합 시 <b>+8.41 AA</b>. 성능 향상이 백본이 아닌 설계에서 비롯됨을 입증.
</div>

### Key Contributions

<div class="grid grid-cols-3 gap-3 pt-2">

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900 text-sm">Backbone-Agnostic</div>
<div class="text-[12px] leading-snug text-slate-600 mt-1">특정 아키텍처 계열에 묶이지 않는 설계 — ResNet · ViT · VMamba 어디에든 동일하게 적용 가능</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900 text-sm">Fixed Capacity</div>
<div class="text-[12px] leading-snug text-slate-600 mt-1">세션·데이터셋이 늘어나도 아키텍처를 확장하지 않음 — 4 experts 고정으로 일관</div>
</div>

<div class="p-3 rounded-lg border border-slate-200 bg-slate-50">
<div class="font-semibold text-slate-900 text-sm">Efficiency</div>
<div class="text-[12px] leading-snug text-slate-600 mt-1">선형 시간 복잡도 state-space 백본으로 ViT attention의 quadratic cost 회피</div>
</div>

</div>
