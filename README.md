# Gyumin Park — AI Research Engineer Portfolio

[Slidev](https://sli.dev) 기반 포트폴리오 슬라이드.

## 실행

```bash
cd slides
pnpm install
pnpm dev        # http://localhost:3030
```

## 빌드 · 내보내기

```bash
pnpm build      # 정적 사이트 → slides/dist
pnpm export     # PDF → slides/slides-export.pdf
```

## 구조

- `slides/slides.md` — 진입점 (표지 + 페이지 모듈 import)
- `slides/pages/` — 섹션별 슬라이드
- `slides/style.css` — 전역 스타일
