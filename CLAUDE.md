# Promnive

AI 프롬프트를 공유하고 배우는 사이트.
기획 → 디자인(Figma) → 개발 → 배포까지 1인으로 진행한다. 목표: 2027-01-29 정식 출시.

## 기술 스택

- **Vite + React 19**, **JavaScript**
  - TypeScript는 출시 후에 도입한다 → [ADR 001](docs/decisions/001-typescript-after-launch.md)
- 배포: Vercel
- 새 라이브러리는 **필요해질 때**, 이유를 정리하고 합의한 뒤에 추가한다. "혹시 몰라서" 미리 깔지 않는다.

## 자주 쓰는 명령어

```bash
npm run dev      # 개발 서버 (http://localhost:5173)
npm run build    # 배포용 빌드 (dist/)
npm run preview  # 빌드 결과 미리보기
npm run lint     # ESLint 검사
```

## 폴더 구조

```
src/
  main.jsx   # 시작점: index.html의 #root에 <App />을 렌더
  App.jsx    # 최상위 컴포넌트
docs/
  decisions/ # 기술 결정 기록 (ADR)
.github/     # 이슈·PR 템플릿
```

기능이 생기면 이 구조를 함께 갱신한다.

## 작업 흐름 (GitHub Flow)

1. **Issue** 만들기 (양식: 작업 / 버그)
2. main에서 최신을 받고 브랜치 만들기
   ```bash
   git switch main
   git pull
   git switch -c type/이슈번호-설명
   ```
3. 작업 → 커밋 (한 커밋 = 한 의도)
4. `git push -u origin 브랜치이름`
5. **PR** 만들기 (템플릿 사용, 본문에 `Closes #이슈번호`)
6. **Squash and merge**
7. 브랜치 삭제 → main으로 돌아와 `git pull`

- **main에 직접 push 금지.** GitHub Ruleset으로 막혀 있다. main은 PR로만 바뀐다.

## 이름 규칙

| 대상 | 형식 | 예시 |
|---|---|---|
| 이슈 · PR 제목 | `type: 설명` | `docs: 프로젝트 셋업 문서 추가` |
| 브랜치 | `type/이슈번호-설명` (영어 소문자, 하이픈) | `feat/3-prompt-card` |
| 커밋 | `type(scope): 설명` (설명은 한국어) | `feat(card): 복사 버튼 추가` |

- 커밋은 [Conventional Commits 1.0](https://www.conventionalcommits.org/ko/v1.0.0/)을 따른다. scope는 생략할 수 있다.
- Squash merge를 쓰므로 **PR 제목이 그대로 main의 커밋 메시지가 된다.** PR 제목도 같은 형식으로 쓴다.

| type | 언제 |
|---|---|
| `feat` | 사용자가 느끼는 새 기능 |
| `fix` | 버그 수정 |
| `docs` | 문서만 변경 |
| `style` | 코드 서식만 변경 (동작·화면 그대로) |
| `refactor` | 동작은 그대로, 구조만 변경 |
| `chore` | 설정, 패키지 같은 잡일 |

## AI(Claude)와 일하는 규칙

- **코드는 내가 직접 쓴다.** Claude는 설명 · 리뷰 · 문서를 맡는다.
- 코드를 바꾸기 전에 **계획을 먼저** 보여준다. 동의하면 작고 되돌릴 수 있는 단위로 진행한다.
- 터미널 · git 명령은 Claude가 **뜻을 설명하고, 내가 직접 입력**한다.
- 기능을 만들 때마다 **DevTools로 확인하는 방법**(Console · Elements · Network · React DevTools)을 함께 안내한다.
- 동작(비즈니스 로직)을 임의로 바꾸지 않는다. 바꿔야 하면 먼저 묻는다.
- 과한 추상화 금지. 같은 코드가 3번 반복되기 전에는 헬퍼를 만들지 않는다.
- 모르는 것(백엔드 스펙 등)은 추측해서 채우지 않는다. mock 데이터와 `TODO`로 자리만 만든다.
- 설명과 커밋 메시지는 **한국어**로 쓴다.

## 결정 기록 (ADR)

중요한 기술 결정은 `docs/decisions/`에 번호를 붙여 남긴다. "무엇을, 왜 골랐고, 무엇을 포기했는지"를 적는다.
