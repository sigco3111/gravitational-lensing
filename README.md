# 🌌 Gravitational Lensing

> Three.js + WebGL fragment shader로 구현한 Schwarzschild 블랙홀 중력 렌즈 시뮬레이터

슈바르츠실트 블랙홀 주변에서 별빛이 휘어지는 아인슈타인 링(Einstein ring), 광자 구체(photon sphere), 그림자(black hole shadow)를 실시간 fragment shader로 ray-tracing하여 렌더링합니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모

> **👉 [https://gravitational-lensing-flax.vercel.app/](https://gravitational-lensing-flax.vercel.app/)** — 브라우저에서 바로 실행 (WebGL 필요)

| | |
|---|---|
| ![Live](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Fgravitational--lensing-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/gravitational-lensing) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Three.js%20%2B%20WebGL-000000?style=flat-square&logo=three.js&logoColor=white) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-1_CDN-9CA3AF?style=flat-square) |

### ⚡ 빠른 사용법
1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기
2. **드래그** — 카메라 궤도 회전
3. **스크롤** — 줌 인/아웃
4. **슬라이더 4개** — 슈바르츠실트 반경 / 카메라 거리 / 별 밀도 / 렌즈 강도 조절
5. **한 / EN 버튼** — UI 한국어 ↔ English 토글

---

## 🤖 생성 정보

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/gravitational-lensing`](https://github.com/sigco3111/gravitational-lensing) |
| **라이선스** | MIT |
| **의존성** | 1개 (Three.js 0.160.0 — unpkg CDN ES module) |

### 📝 사용된 프롬프트 (원문)

```
태양 질량의 10배 정도 되는 슈바르츠실트 블랙홀 주위에서 별빛이 휘어지는
아인슈타인 링, 광자 구체, 블랙홀 그림자가 보이는 인터랙티브 중력 렌즈
시뮬레이터를 만들어줘. 화면에는 슬라이더로 Schwarzschild 반경, 별 밀도,
카메라 거리를 조절할 수 있게 하고, 마우스 드래그로 카메라 궤도를 돌릴
수 있게 해줘.

Implementation Advice: Use Three.js + WebGL fragment shader for real-time
photon ray-marching through Schwarzschild metric. Compute critical impact
parameter bc = (3√3/2)·rs in GLSL for photon sphere. 모든 의존관계의
코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## ✨ 주요 특징

- 🌀 **Schwarzschild 광선 추적** — fragment shader에서 Schwarzschild 메트릭으로 광자 경로 실시간 적분
- 🎯 **아인슈타인 링 / 광자 구체** — 임계 충격 계수 `bc = (3√3)/2 ≈ 2.598` 정확 계산
- 🌑 **블랙홀 그림자** — 이벤트 지평선 + 광자 포획 영역 시각화
- 🎛️ **4개 라이브 슬라이더** — `r_s` / 카메라 거리 / 별 밀도 / 렌즈 강도
- 🌍 **은하 배경** — FBM noise로 procedural은하 + 안개(nebula) 색상 블렌딩
- 🌐 **빌트인 한/영 토글** — UI 라벨 즉시 전환 + localStorage 저장
- 📦 **단일 HTML** — 35KB ES module + Three.js CDN

---

## 🚀 실행 방법

### 방법 1: 그냥 브라우저로 열기 (WebGL 활성화 필요)
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 2: 로컬 서버 (권장 — ES module CORS 회피)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

### 방법 3: 라이브 데모
위 Vercel alias URL에서 바로 확인 가능합니다.

---

## 🎮 조작법

| 입력 | 효과 |
|---|---|
| **드래그** | 카메라 궤도 회전 |
| **스크롤** | 줌 인/아웃 |
| **터치 드래그** | 모바일에서도 동일 |
| **R 키** | 시점 리셋 (`θ=0.3, φ=0.25, dist=5.0, r_s=0.5`) |
| **r_s 슬라이더** | 슈바르츠실트 반경 조절 (이벤트 지평선 크기) |
| **카메라 거리 슬라이더** | 카메라 ↔ 블랙홀 거리 |
| **별 밀도 슬라이더** | 배경 별 개수 / 분포 |
| **렌즈 강도 슬라이더** | 광선 굴절 강도 (배율) |
| **한 / EN 버튼** | UI 언어 토글 |

---

## 🛠️ 기술 스택

| 영역 | 사용 기술 |
|---|---|
| **렌더링** | Three.js 0.160.0 + WebGL fragment shader |
| **물리** | Schwarzschild 메트릭 광선 추적 (ray-marching) |
| **셰이더** | GLSL FBM noise + Schwarzschild 적분 |
| **카메라** | 구면 좌표 (`θ`, `φ`, `distance`) |
| **정밀도** | `CRITICAL_IMPACT_FACTOR.toFixed(8)` (소수점 8자리) |
| **의존성** | 1개 (Three.js, unpkg CDN) |

### 핵심 사양

| 상수 | 값 | 의미 |
|---|---|---|
| `BH_CENTER` | `(0, 0, 0)` | 블랙홀 위치 (원점) |
| `CRITICAL_IMPACT_FACTOR` | `(3√3)/2 ≈ 2.598076211` | 광자 포획 임계 충격 계수 |
| `state.rs` (default) | `0.5` | 슈바르츠실트 반경 |
| `state.cameraDistance` (default) | `5.0` | 카메라 거리 |
| `state.lensingStrength` (default) | `1.0×` | 렌즈 강도 배율 |
| `state.cameraTheta / Phi` (default) | `0.3 / 0.25` | 초기 시점 각도 |

---

## 📂 프로젝트 구조

```
gravitational-lensing/
├── index.html      # 단일 HTML (모든 코드 포함, ~35KB)
├── README.md       # 한국어 (기본)
├── README.en.md    # English
└── LICENSE         # MIT
```

---

## 🎨 디자인 결정

브레인스토밍 단계에서 내린 결정 5가지:

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **렌더링** | GPU fragment shader ray-marching | CPU 적분 대비 60fps 안정 |
| **광선 적분** | Schwarzschild 메트릭 직접 계산 | Einstein ring + photon sphere 정확 재현 |
| **임계 계수** | `(3√3)/2`를 `.toFixed(8)`로 GLSL 주입 | JS IEEE 754 오차 회피, 셰이더에서 고정밀도 |
| **은하 배경** | GLSL FBM noise + nebula color blend | 별/먼지 procedural 생성, 텍스처 의존 X |
| **i18n** | 빌트인 토글 + localStorage | 한/EN 즉시 전환, 새로고침 후에도 유지 |

### 직접 커스터마이즈하고 싶다면

`index.html`의 `i18n` 객체와 shader 상수를 조정하면 시각 효과와 라벨을 바꿀 수 있어요:

```js
// 상단 i18n 객체에서 라벨 변경
const i18n = {
  ko: { pageTitle: '중력 렌즈 — 슈바르츠실트 블랙홀', /* ... */ },
  en: { pageTitle: 'Gravitational Lensing — Schwarzschild Black Hole', /* ... */ }
};

// Schwarzschild 상수
const CRITICAL_IMPACT_FACTOR = (3.0 * Math.sqrt(3.0)) / 2.0;  // 광자 포획 임계
```

고급 사용자용: GLSL fragment shader의 `vec3 bg`, `galNormal`, nebula color 상수를 수정하면 우주 배경 색감을 바꿀 수 있습니다.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 [MiniMax](https://example.com) 의 MiniMax-M3 모델과 OpenCode CLI 환경에서 생성되었습니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행했습니다.