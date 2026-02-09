---
layout: post
title: "실무에서 쓰는 Git 워크플로우 팁"
date: 2026-02-01
categories: [개발]
---

Git을 매일 사용하지만 기본적인 커맨드만 쓰고 있지는 않으신가요? 실무에서 유용한 Git 팁들을 정리해보았습니다.

## 커밋 메시지 컨벤션

팀에서 일관된 커밋 메시지를 사용하면 히스토리를 읽기 훨씬 수월합니다.

```
feat: 사용자 로그인 기능 추가
fix: 이메일 유효성 검사 오류 수정
docs: API 문서 업데이트
refactor: 인증 모듈 리팩토링
test: 회원가입 단위 테스트 추가
chore: ESLint 설정 업데이트
```

## 유용한 Git 명령어

### git stash - 임시 저장

작업 중 급히 다른 브랜치로 이동해야 할 때 유용합니다.

```bash
# 현재 변경사항 임시 저장
git stash

# 임시 저장 목록 확인
git stash list

# 가장 최근 stash 복원
git stash pop

# 메시지와 함께 stash
git stash save "로그인 기능 작업 중"
```

### git rebase -  히스토리 정리

```bash
# 최근 3개 커밋 정리
git rebase -i HEAD~3

# main 브랜치의 최신 변경사항 가져오기
git rebase main
```

### git log 활용

```bash
# 한 줄로 보기
git log --oneline

# 그래프로 브랜치 시각화
git log --oneline --graph --all

# 특정 파일의 변경 히스토리
git log --follow -p -- filename.js
```

## 브랜치 전략

소규모 팀에서는 GitHub Flow가 간단하고 효과적입니다.

1. `main` 브랜치는 항상 배포 가능한 상태 유지
2. 새 작업은 `feature/기능명` 브랜치에서 진행
3. Pull Request로 코드 리뷰 후 병합
4. 병합 후 feature 브랜치 삭제

Git은 사용할수록 새로운 기능을 발견하게 됩니다. 기본기를 탄탄히 하고, 하나씩 새로운 명령어를 익혀보세요!
