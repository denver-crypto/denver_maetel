# Tennis Match Generator

This project is a React-based web app that automatically generates doubles match schedules for tennis clubs. It balances teams based on NTRP scores, leave times, gender rules, and avoids consecutive matches.

---

# 🎾 신나용테니스 대진표 생성기

React 기반의 웹 앱으로, **테니스 클럽 복식 경기 대진표**를 자동으로 생성해줍니다.  
NTRP 점수, 퇴장 시간, 경기 시간, 성별 규칙 등을 고려하여 **공정하고 현실적인 매칭**을 지원합니다.

<p align="center">
  <img src="docs/demo.png" alt="대진표 생성기 화면 예시" width="720"/>
</p>

---

## 🚀 배포

- **GitHub Pages**: [https://<YOUR_ORG>.github.io/<YOUR_REPO>/](https://<YOUR_ORG>.github.io/<YOUR_REPO>/)  
- **Vercel**: [https://<YOUR_REPO>.vercel.app](https://<YOUR_REPO>.vercel.app)

---

## ✨ 주요 기능

- **자동 매칭 알고리즘**
  - NTRP 합산 점수 기반 밸런싱
  - 퇴장 시간(leaveBy) + 경기시간 고려
  - 연속 경기 금지 옵션
  - NTRP 팀합 차이 상한
  - 혼복(M+F) 강제, 옵션으로 잡복 완화 허용

- **대진표 UI**
  - 코트/시간별로 팀A vs 팀B 표시
  - 팀 합산 점수, 밸런스(점수 차) 표시
  - 빈 칸은 배정 불가 → 제약 조정 후 재생성

- **수동 편집 (Drag & Drop)**
  - 자동 생성된 대진표를 직접 수정 가능
  - 선수 칩을 끌어다 슬롯에 배치/스왑
  - 실시간 유효성 검사: 중복/성별 규칙/퇴장 금지 체크

- **내보내기**
  - CSV (UTF-8 BOM, 엑셀 호환)
  - XLSX (SheetJS 동적 로드)

- **테스트 내장**
  - CSV 줄바꿈/혼복 규칙/퇴장 조건/연속 금지/NTRP cap 동작 검증

---

## 🛠 설치 및 실행

### 1. 클론 & 의존성 설치
```bash
git clone https://github.com/<YOUR_ORG>/<YOUR_REPO>.git
cd <YOUR_REPO>
npm install
2. 로컬 실행
npm start

3. 정적 빌드
npm run build


→ dist/ 또는 build/ 디렉토리를 GitHub Pages / Vercel / Netlify 등에 배포

4. GitHub Pages 배포
npm run build
git subtree push --prefix build origin gh-pages

5. Vercel 배포

Vercel
에서 New Project → 해당 GitHub 리포 연결

루트 경로 또는 build/ 경로 지정 후 배포

⚙️ 주요 옵션
옵션	설명	기본값
경기 시간(분)	퇴장시간 계산에 사용	30
NTRP 차 상한	두 팀 합산 점수 차 ≤ cap 이어야 매칭	0.5
퇴장 이후 금지	(시작+경기시간) ≤ leaveBy 조건 만족 시 배정	✅
연속 경기 금지	같은 선수가 연속 타임에 출전 불가	✅
혼복 완화	혼복(M+F) 실패 시 잡복 허용	❌
📝 사용 방법

선수 등록

이름, 성별(M/F), NTRP(1.0~5.0, 0.5 단위), 퇴장 시간(optional)

설정

시간 범위, 코트 수, 경기 인터벌(분), 경기 타입 패턴 입력

대진표 생성

[재생성] 버튼 클릭 → 자동 편성

수동 편집

[수동 편집] 모드 켜기 → 드래그 앤 드롭으로 팀 교체/스왑

내보내기

[CSV], [XLSX] 버튼으로 다운로드

📦 기술 스택

React (CRA/Vite/Next.js 호환)

TailwindCSS

SheetJS (xlsx) — XLSX 내보내기용 (CDN 동적 로드)

✅ TODO (향후 확장)

최소 휴식 시간(n분) 옵션

팀합 목표값 기반 매칭 (리그 표준화)

동일 페어 상한 (ex. 최대 1회)

세션 저장/불러오기 (LocalStorage)

## 📱 PWA 템플릿

- `manifest.webmanifest`: 앱 이름, 아이콘, 테마 색상 등을 정의합니다.
- `sw.js`: 설치/활성화 이벤트만 처리하는 간단한 서비스 워커 예제입니다.

React/Vite 환경에서는 `index.html`에 다음 링크를 추가하고, `main.tsx`에서 서비스 워커를 등록하세요.

```html
<link rel="manifest" href="/manifest.webmanifest">
```

```ts
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js');
}
```

Next.js(App Router)에서는 `app/manifest.webmanifest` 파일을 두고 `public` 디렉터리에 `sw.js`를 넣은 뒤 `layout.tsx`에서 `<link rel="manifest" href="/manifest.webmanifest" />`를 추가하면 됩니다.

👨‍💻 개발 메모

runTests() 내장으로 주요 제약사항 자동 검증

코드 업데이트 시 반드시 테스트 통과 후 배포

📜 라이선스

MIT License © 2025 신나용테니스
