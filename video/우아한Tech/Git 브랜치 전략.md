
# Git 브랜치 전략
- https://www.youtube.com/watch?v=jeaf8OXYO1g

## 자주 쓰이는 브랜치 전략
- git-flow: 5가지의 브랜치를 이용해 운영하는 브랜치 전략
- github-flow: master 브랜치와 Pull Request를 활용한 단순한 브랜치 전략

## git-flow
- 항상 유지되는 2개의 메인 브랜치와 역할을 완료하면 사라지는 3개의 보조 브랜치로 구성

- 메인 브랜치는 항상 유지
	- master
	- develop
- 보조 브랜치: merge되면 사라짐
	- feature
	- release
	- hotfix

## git-flow step1 (develop)
- develop 기준 개발 기능에 맞는 feature 브랜치 생성
- 기능 완성되면 리뷰 후 develop브랜치에 merge

## git-flow step2 (QA)
- develop브랜치에 모두 머지 됬다면 develop기준 release 브랜치 생성
- QA 끝나면 master 브랜치로 merge. 다만 이후에 bugfix가 있다면 master, develop에 merge?
	- QA 후에 대한 bugfix가 hotfix로 분류될것인지 or 다른 규칙이 있는건지 명확하게 설명이 안되어있음 

## git-flow step2 (hotfix)
- master 에서 버그가 발생하면 hotfix브랜치 생성
- develop, master 브랜치에 각각 merge

## github-flow
- 제품이 릴리즈되는 최신버젼 master브랜치만 존재

## github-flow 개발 프로세스
- 기능 개발, 버그 픽스 어떤 이유로든 branch 생성
	- 의도가 드러나게끔하는게 중요
- 의도 잘드러나게 branch 생성 -> 커밋 ->  PR 생성 -> 리뷰 -> 테스트환경 배포? -> master merge 후 자동 배포

## QA
- github-flow는 다시 찾아봐야될듯하다.