# CLAUDE.md — KUNWON AI HUB

## 프로젝트 개요

건원(KUNWON) 건축설계사무소 내부용 AI 툴 카탈로그. 사내에서 개발 중인 80+ 개의 AI 앱을 상태(완성/베타/개발중/초안/아이디어)별, 카테고리별로 탐색하고 바로 실행할 수 있는 단일 HTML 대시보드.

- **제작자**: 설계사업6본부1소 김정현 (junghyun@kunwon.com)
- **배포**: GitHub Pages (`https://github.com/DaDaDiRaRa/kw-ai-hub`)
- **운영·전략 문서**: `kunwon-ops` (private) — 앱별 벤치마킹, 정리 계획, 접기 판단 기준.
  이 레포는 Pages 배포 때문에 Public 이라 그런 문서를 둘 수 없다
- **아키텍처**: 단일 정적 HTML 파일 (`index.html`) — 빌드 도구, 패키지 매니저, 프레임워크 없음

---

## 파일 구조

```
kw-ai-hub/
└── index.html   ← 전체 앱 (HTML + CSS + JS 모두 포함)
```

빌드 없음. `index.html` 하나가 전부다.

---

## 앱 데이터 구조

`index.html` 내부 `const APPS = [...]` 배열이 핵심 데이터다.

```javascript
{
  name: "앱 이름",           // 한국어
  desc: "카드에 표시되는 짧은 설명",
  detail: "모달에서 보이는 상세 설명 (선택)",
  url: "https://...run.app", // live/beta는 실제 URL, 나머지는 "---------"
  icon: "🏛️",
  tags: ["법규", "FastAPI", "Claude", "유료"],
  color: "#6366f1",          // 카드 상단 그라디언트 색
  type: "external",          // "external" | "local" | "python" | "html"
  status: "live",            // "live" | "beta" | "building" | "draft" | "idea"
  category: "법규",          // "법규" | "도면" | "3D" | "렌더" | "문서" | "관리" | "공모"
}
```

### status 의미
| status | 표시 | 의미 |
|--------|------|------|
| `live` | 🟢 완성 | 배포 완료, 운영 중 |
| `beta` | 🟡 베타 | 배포됐지만 테스트 단계 |
| `building` | 🔵 개발중 | 현재 개발 진행 중 |
| `draft` | ⚪ 초안 | 기획 완료, 개발 전 |
| `idea` | 💡 아이디어 | 아이디어 단계 |

### 카드 정렬 순서
`live → beta → building → draft → idea` 순서, 동일 status 내에서는 한국어 이름 가나다순.

---

## 주요 기능 (JavaScript)

| 기능 | 설명 |
|------|------|
| 검색 | `name`, `desc`, `tags` 대상 실시간 필터 |
| Status 필터 | 상단 chip으로 단일 선택 |
| Category 필터 | 상단 chip으로 단일 선택 |
| 다크/라이트 테마 | CSS 변수 + `data-theme` 속성 토글 |
| 앱 카드 클릭 | URL 있으면 새 탭으로 열기, 없으면 상세 모달 |
| 모달 | 상세 설명, 기술 태그, 상태 안내 |

---

## 스타일 규칙

- CSS 변수: `--bg`, `--surface`, `--border`, `--text`, `--muted`, `--accent` (#6366f1 인디고)
- 다크 테마가 기본값 (`:root`에 정의). 라이트는 `[data-theme="light"]` 오버라이드
- 폰트: Pretendard / 시스템 폰트 폴백
- 카드 그리드: `auto-fill, minmax(300px, 1fr)`

---

## 앱 추가 방법

`index.html`의 `APPS` 배열에 객체를 추가한다. 순서는 정렬 함수가 자동 처리하므로 위치 무관.

```javascript
{
  name: "새 앱 이름",
  desc: "한 줄 설명",
  url: "---------",           // 아이디어 단계면 이렇게
  icon: "🔧",
  tags: ["태그1", "태그2"],
  color: "#색상코드",
  type: "external",
  status: "idea",
  category: "문서",
}
```

---

## 배포

변경 후 git push → GitHub Pages 자동 배포.

```bash
git add index.html
git commit -m "YYMMDD_HHMM"   # 팀 커밋 메시지 컨벤션
git push
```

---

## 개별 AI 앱 배포 환경

각 앱은 별개 서비스로 Google Cloud Run에 배포됨 (`*.asia-northeast3.run.app`).  
이 허브는 링크만 가지고 있으며, 앱 자체 코드는 이 레포에 없다.

**주로 쓰이는 스택 (앱별)**:
- Backend: FastAPI (Python)
- Frontend: React
- AI: Claude API, Gemini API, GPT-4o
- 외부 API: 토지이음, 세움터, 브이월드, KOSIS, 법제처, DeepL
- 특수 라이브러리: ezdxf, IfcOpenShell, shapely, geopandas, rhino3dm
