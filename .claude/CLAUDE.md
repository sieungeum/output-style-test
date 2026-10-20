# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 실행 방법

빌드, 린트, 테스트 도구가 없습니다 (`package.json` 없음). HTML 파일을 브라우저로 직접 열어서 확인합니다.

```powershell
start counter.html
```

`counter`, `todo`, `stopwatch`는 `https://cdn.tailwindcss.com`을 불러오므로 확인할 때 인터넷 연결이 필요합니다.

## 구조

`counter.html`, `todo.html`, `stopwatch.html`, `calculator.html`은 각각 마크업, 스타일, `<script>`가 한 파일에 들어 있는 독립된 앱입니다. 파일 간 import나 공유 코드가 없으므로 한 앱을 고쳐도 다른 앱에는 영향이 없습니다.

모든 앱이 같은 패턴을 따릅니다.

- `<script>` 맨 위에서 `let` 변수로 상태를 두고, `document.getElementById('id')`로 요소를 미리 가져옵니다.
- `render()`가 상태를 화면에 반영합니다. 이벤트 핸들러는 상태를 바꾼 뒤 `render()`를 호출하고, 스크립트 끝에서 초기 `render()`를 한 번 호출합니다.

앱별 차이:

- **calculator**: Tailwind를 쓰지 않고 직접 작성한 `<style>`을 씁니다. `.buttons` 컨테이너 하나에 클릭을 위임하고 `keydown` 키보드 입력도 지원합니다.
- **todo**: `render()`가 목록 DOM을 직접 만들어 그립니다. `localStorage`를 쓰지 않아 새로고침하면 데이터가 사라집니다.
- **stopwatch**: `setInterval(render, 100)`으로 0.1초마다 화면을 갱신합니다.

UI 텍스트와 주석은 모두 한국어입니다. `counter`, `todo`, `stopwatch`에는 초보자용 설명 주석이 많으므로, 이 파일들을 수정할 때는 같은 밀도의 주석을 유지하세요.

## 저장소 특이사항

- `bug.md`, `bug1.md`, `dev1.md`, `dev2.md`, `git_test.md`, `signup.md`는 Git 브랜치 연습용 더미 파일이며 앱과 무관합니다. 브랜치는 `master`, `develop`, `hotfix`가 있습니다.
- `.claude/settings.json`은 `defaultMode: plan`과 출력 스타일 `Beginner Friendly`(`.claude/output-styles/beginner.md`)를 지정합니다.
- `.gitignore`는 `.claude/settings.local.json`을 제외하지만, 실제 파일명은 `.claude/setting.local.json`(오타)이라 무시되지 않고 Claude Code도 로컬 설정으로 인식하지 못할 가능성이 큽니다.

## 코드 스타일 주의

기존 HTML의 JavaScript는 세미콜론을 사용합니다. 전역 규칙(세미콜론 없음)과 다르므로, 기존 파일을 수정할 때는 해당 파일의 스타일을 따를지 먼저 확인하세요.
