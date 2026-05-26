# KUNWON AI HUB

> 건원 건축설계사무소 AI 툴 카탈로그 — 사내 개발 AI 앱을 한 곳에서 탐색하고 실행합니다.

---

## 소개

**KUNWON AI HUB**는 건원 설계사업6본부1소에서 개발 중인 80개 이상의 AI 앱을 한눈에 볼 수 있는 내부 대시보드입니다.

건축 업무 전반에 걸쳐 반복되는 작업을 AI로 자동화하는 도구들을 상태별·카테고리별로 정리하고, 완성된 서비스는 바로 실행할 수 있습니다.

---

## 현재 운영 중인 앱

| 앱 | 설명 | 기술 |
|----|------|------|
| 🏛️ 건축 법규 자동 진단 | 주소 입력 → 용도지역·건폐율·용적률 자동 산출 | FastAPI · React · Claude |
| 🏆 현상 공모 비교분석 | 공모전 PDF → AI 분석 및 당선작 패턴 비교 | FastAPI · React · Claude |
| 🏗️ AI 조감도 렌더링 | 건축 스케치 → 실사 렌더링 자동 변환 | FastAPI · React · Gemini |
| 🏠 평면도 3D 시각화기 (베타) | 2D 평면도 → 아이소메트릭 4방향 3D 렌더링 | FastAPI · Gemini 2.5 Pro |

---

## 카테고리

| 카테고리 | 내용 |
|---------|------|
| 법규 | 건축법·용도지역 진단, BIM 법규 체크 |
| 도면 | DWG 교차검토, IFC 파싱, 도면 자동화 |
| 3D | 볼륨 최적화, Rhino/CesiumJS 시각화 |
| 렌더 | 스케치→렌더링, 평면도→3D, 조감도 생성 |
| 문서 | 계약서·기획서·보고서 AI 작성 |
| 관리 | 프로젝트 일정·공정·원가 관리 |
| 공모 | 공모전 분석, 제안서 생성 |

---

## 상태 표시

| 상태 | 의미 |
|------|------|
| 🟢 완성 | 운영 중, 바로 사용 가능 |
| 🟡 베타 | 배포됐지만 테스트 단계 |
| 🔵 개발중 | 현재 개발 진행 중 |
| ⚪ 초안 | 기획 완료, 개발 예정 |
| 💡 아이디어 | 검토 중인 기능 |

---

## 기술 스택

**허브 자체**: 순수 HTML · CSS · JavaScript (빌드 도구 없음)

**개별 앱 공통 스택**:
- Backend: FastAPI (Python)
- Frontend: React
- AI: Claude API · Gemini API · GPT-4o
- 외부 데이터: 토지이음 · 세움터 · 브이월드 · KOSIS · 법제처
- 특수 처리: ezdxf (CAD) · IfcOpenShell (BIM) · shapely · geopandas · rhino3dm
- 배포: Google Cloud Run (`asia-northeast3`)

---

## 앱 추가

`index.html`의 `APPS` 배열에 객체를 추가하면 됩니다. 자세한 데이터 구조는 [CLAUDE.md](CLAUDE.md) 참고.

---

## 제작

**설계사업6본부1소 김정현** · junghyun@kunwon.com  
KUNWON Engineering & Architects
