# 컨텍스트 인식형 건물 에너지 시뮬레이션 에이전트

> 스마트시티융합학과 석사과정 유도연 | Gachon University Smart City Lab

주변 건물 컨텍스트(IBE)를 자동으로 반영하는 LLM 기반 건물 에너지 시뮬레이션 에이전트 웹 서비스.

---

## 프로젝트 구조

```
.
├── planning/               # 연구 계획서
├── PPT/                    # 발표 자료
├── References/             # 참고 문헌
├── frontend/               # 정적 HTML 프로토타입 (참고용)
└── frontend-react/         # React 프론트엔드 (현재 개발 버전)
```

---

## Frontend React 실행 방법

### 환경

- Node.js 18+
- WSL2 (Ubuntu) — Windows `/mnt/d/...` 경로에서 개발

### WSL 제약 사항

`/mnt/d/` (Windows NTFS 파일시스템)에서는 npm이 `node_modules/.bin` 심볼릭 링크를 생성하지 못합니다.
따라서 **소스 코드는 Windows 경로에서 편집**하고, **npm 설치 및 실행은 Linux 홈 디렉토리**에서 진행합니다.

---

### 최초 설치 (한 번만)

```bash
# 1. Linux 홈 디렉토리에 작업 공간 생성
mkdir -p ~/ubem-react

# 2. 소스 파일 복사
rsync -av --exclude='node_modules' --exclude='dist' \
  "/mnt/d/gachon/대학원/Agentic AI in Smart City/frontend-react/" \
  ~/ubem-react/

# 3. 패키지 설치
cd ~/ubem-react
npm install
```

---

### 개발 서버 실행

```bash
cd ~/ubem-react
npx vite --host 0.0.0.0 --port 5173
```

브라우저에서 `http://localhost:5173` 접속.

---

### 소스 수정 후 동기화

VS Code 등에서 `/mnt/d/.../frontend-react/src/` 파일을 편집한 뒤, Linux 작업 공간에 동기화합니다.

```bash
# 소스만 동기화 (node_modules 제외)
rsync -av --exclude='node_modules' --exclude='dist' \
  "/mnt/d/gachon/대학원/Agentic AI in Smart City/frontend-react/" \
  ~/ubem-react/
```

또는 동기화 + 서버 실행을 한 번에:

```bash
bash ~/ubem-react/sync-and-dev.sh
```

> **Tip:** Vite HMR(Hot Module Replacement)은 Linux 파일시스템(`~/ubem-react`)을 감시합니다.
> Windows 경로에서 파일을 저장한 뒤 위 rsync 명령을 실행하면 브라우저가 자동으로 갱신됩니다.

---

### 프로덕션 빌드

```bash
cd ~/ubem-react
npm run build
# 결과물: ~/ubem-react/dist/
```

---

## 기술 스택 (Frontend)

| 항목 | 도구 |
|---|---|
| 프레임워크 | React 18 + TypeScript |
| 빌드 도구 | Vite 5 |
| 상태 관리 | Zustand |
| 차트 | Recharts |
| 스타일 | CSS Variables (커스텀 다크 테마) |

## 화면 구성 (PPT 기반)

| 탭 | 내용 |
|---|---|
| Main Building | 건물 3D 시각화, Agent 상태, Calibration 지표, 파이프라인 |
| With Contexts | 주변 건물 파라미터 설정, Top-View 맵, IBE 슬라이더 |
| Simul Result | 월별/시간별 에너지 차트, 시나리오 민감도 테이블 |
| Retrofit Report | Decision Shift 분석, Retrofit 우선순위, Radar 차트 |
| Chat Panel | 자연어 질의 응답 (Agent 시뮬레이션) |
