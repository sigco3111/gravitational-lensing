# 🌀 Gravitational Lensing — WebGL Fragment Shader

> 아인슈타인 일반 상대성 이론 기반 Schwarzschild 블랙홀 주변의 중력 렌즈 효과를 WebGL 프래그먼트 쉐이더로 물리적으로 정확하게 렌더링합니다.

## 🤖 생성 정보 (Attribution)

- **도구**: [OpenCode CLI](https://github.com/snyk/snyk)
- **모델**: 미니맥스 M3 (MiniMax-M3)
- **저장소**: [sigco3111/gravitational-lensing](https://github.com/sigco3111/gravitational-lensing)
- **작업자**: [코드깎는노인](https://github.com/sigco3111)

### 사용된 프롬프트 (verbatim)

> 아인슈타인의 일반 상대성 이론에 기반하여 화면 중앙에 거대한 블랙홀을 배치하고, 블랙홀의 강력한 중력이 뒤편의 은하수 배경(Starfield) 빛을 휘게 만드는 중력 렌즈(Gravitational Lensing) 효과를 WebGL 쉐이더로 왜곡 없이 물리적으로 정확하게 계산하여 렌더링해줘.
>
> Implementation Advice: Use **Three.js** or **WebGL**. The visual core is a **Fragment Shader**. Pass the black hole position as a uniform and distort the UV coordinates of the background texture based on the distance from the black hole center. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.

## 📊 Status

- [x] **저장소 초기화** (gh repo create + .gitignore + README)
- [ ] **placeholder index.html** (OpenCode 작업 컨텍스트 echo)
- [ ] **index.html 구현** (WebGL fragment shader + Schwarzschild lensing)
- [ ] **Vercel 배포** (`https://gravitational-lensing.vercel.app/`)
- [ ] **README v1.0 다층화** (라이브 데모 + Design Choices + Key Constants)

## 🎬 라이브 데모

🚧 **Under construction** — OpenCode 작업 후 Vercel 배포 시 `https://gravitational-lensing.vercel.app/` URL이 활성화됩니다.

## ✨ 주요 특징

- **물리 기반 왜곡** — Schwarzschild metric에서 파생된 광선 편향각(α ≈ 4GM/(c²b))을 fragment shader로 구현
- **단일 HTML 구조** — Three.js (CDN ES module) 외 외부 의존성 없음, 모든 shader 코드 한 파일에 포함
- **은하수 배경** — 별 입자 (starfield) procedural noise로 생성된 procedural background, 빛이 블랙홀 주변에서 휘어지는 효과
- **블랙홀 실루엣** — event horizon (`r_s = 2GM/c²`) 내부는 완전 검정 (광부품파 불가능)
- **Einstein ring** — 광원이 정확히 정렬될 때 형성되는 특성 시각화 (uniform으로 제어)

## 🚀 실행 방법

```bash
git clone https://github.com/sigco3111/gravitational-lensing.git
cd gravitational-lensing

# Vercel CLI 배포
vercel --yes --prod

# 또는 로컬 정적 호스팅
python3 -m http.server 8000
# http://localhost:8000
```

## 🎮 조작법

🚧 구현 후 추가 예정 — 후보:
- 마우스 드래그 → 블랙홀 위치 이동 (lensing offset uniform)
- 휠 스크롤 → Schwarzschild 반지름(`r_s`) 조절
- 키보드 → 광원 정렬 상태 토글 (Einstein ring on/off)

## 🛠️ 기술 스택

- **Three.js** (CDN ES module, single HTML 임베드)
- **WebGL Fragment Shader** (GLSL ES 3.0)
- **순수 Vanilla JS** (외부 빌드 도구 없음)
- 별도 의존성 0 — 모든 shader 코드 단일 HTML 인라인

## 🎨 디자인 결정

### 1. 왜곡 없는 물리적 정확성?

단순 radial distortion (`uv += vec2(d)*factor`)은 시각적으로 비슷하지만 물리적 함의가 다름. 본 프로젝트는 **Schwarzschild metric**에서 파생:

```
편향각  α ≈ 4GM / (c²·b)
여기서  b = 충돌 매개변수 (광원-블랙홀 최단거리)
```

UV 좌표를 광선 트레이싱 역방향으로 왜곡 — fragment shader에서 `b`를 계산하고 원본 starfield 텍스처에서 `b - α` 위치의 빛을 샘플링.

### 2. Event Horizon 클리핑

`b < r_s = 2GM/c²` 영역은 sample 위치가 블랙홀 안으로 들어가므로 완전 검정 (`return vec3(0.0)`). 광이 탈출 불가능한 영역.

### 3. Procedural Starfield

외부 이미지 의존성을 없애기 위해 fragment shader에서 hash 함수 + 2D noise로 procedural 별 생성. 가우시안 분포로 별 밀도 균일화.

## 📜 License

MIT — see [LICENSE](./LICENSE)

## 🙏 Acknowledgments

- **OpenCode** + **미니맥스 M3** — 프롬프트 → 구현 변환
- **Three.js** — WebGL abstraction layer
- Schwarzschild metric — Karl Schwarzschild (1916)
- Einstein ring theory — Albert Einstein (1936)
- [코드깎는노인](https://github.com/sigco3111) — 컨셉 디자인
