# FECONF 2022 [B2] 일백개 패키지 모노레포 우아하게 운영하기
- 모노레포란 *잘정의된 관계*를 가진, 여러개의 독립적인 프로젝트들이 있는 하나의 레포지토리이다.

## 왜 모노레포를 사용해야할까요?
- Polyrepo 멀티레포
 - 멀티레포의 문제점
  - Project A와 비슷한 형태의 Project B가 새로 추가되는 상황
  - ex) 
	  - 1. 새로운 B레포 추가 
	  - 2. ci/cd, lint, test, ts설정 추가
	  - 3. A에서 재사용 코드들 Lib A레포를 새로 만듦
	  - 4. 2반복
  - 생성 비용 증가
  - 프로젝트간 코드 공유 어려움
  - 같은 이슈 수정하기위해 레포 커밋 필요
  - 히스토리 관리 어려움
  - 제각각인 툴링 개발자 경험 일관적이지 않음
- Monorepo
 - 모노레포
  - 새 프로젝트 생성비용 작음
  - 코드 공유 쉬움
  - Atomic Commits
  - 히스토리 관리 쉬움
  - 공통되니 툴링 일관적인 개발자 경험 제공

## Monorepo Features
- 속도
 - Local computation caching
 - Local task orchestration
 - Distributed computation caching
 - Detecting affected projects / packages
- 관리
 - Source code sharing
 - Code generation
 - Project constraints and visibility

## 우아하게 운영하기
- 잘 정의된 관계
해당 모노레포 관계를 잘 이해하고 있어야한다.
### Toss Frontend Libraries
- 토스 프론트엔드 챕터에서 공통으로 사용하는 내부 라이브러리 모노레포, 서비스 개발을 편하게 할 수 있도록 도와주는 크고 작은 100개 가량의 라이브러리들로 구성

- Library Only Monorepo, Service Monorepo

## 라이브러리 모노레포의 특징
- 토스에서 사용하는 모노레포의 종류

### Library Only Monorepo
- 커밋수 적고 영향범위 큼, NPM 배포
### Service Monorepo
- 커밋수 많고 영향범위 한정적, 내부 인프라 배포

## Library Only Monorepo이기에 더 중요하게 생각하는것
- 1) 의존성, 2) 버젼, 3) 코드 품질, 4) 문서화

- 1) 의존성
 - node_modules의 문제점
 - 유형 의존성 (Phantom Dependency)
  - 호이스팅 기법으로 명시되지 않은 라이브러리를 사용할 수 있다., 최악은 런타임에서 에러가 발생할 수 있다.
    - 이에 해결방법은 Yarn Berry + PnP
    - Yarn cach퐅더로 의존성을 갖게하여 관리한다.
    - .pnp.cjs를 통한 엄격한 의존성 관리
    - + Zero install + 빠른 의존성 검색
 - What is Peer dependency?
 	- Peer dependencies are inherited dependencies - the consumer of your package will be tasked to provide them.
 	- 상속된 디펜던시로 패키지를 사용하는 곳에서 제공해야하는 디펜던시입니다.
 	- Peer Dependency는 전파된다.
 	- 따라서 꼭 싱글턴으로 존재해야하는 패키지일때만 Peer Dependency로 명시해주자
 	 - ex) React, Next 버져닝
- 2) 버젼관리
 - What is Semver?
  - Semantic Versioning or SemVer contain a set of rules and requirements that dictate how version numbers are assigned and incremented.
 - 배포 및 버젼관리
  - ex) 4(Major).7(Minor).6(Patches)
  - lerna version
- 3) 코드 품질 관리
 - RFC (Request For Comments)
  - 아이디어만으로 RFC를 올리면 보시는것과같이 설계에 대한 리뷰와 피드백을 받을 수 있습니다.
  - 이러한 과정을 통해 라이브러리 설계가 탄탄, 코드품질 올라가게 됩니다.
 - Pull Request
  - PR 올리기전 라이브러리 오너의 코드리뷰를 받는다.
  - PR 올리기 전 체크리스트
  ```
  - 새 기능을 추가한 경우, 요약 섹션을 작성
  - 추가된 파일에 대해 *.md 형식으로 문서를 작성
  - 추가되거나 변경된 동작을 검증할 수 있는 테스트를 최대한 작성
  ```
- 4) 문서화


## My Opinion
- 모노레포에 대한 내용보단 라이브러리 관리 방법에 대한 내용에 집중되어있는 느낌을 받았다.
- 라이브러리 관리에 대한 내용으로선 유익한 영상인듯하다?
- 모노레포 내용은 정의랑 문서를 보면 나오는 수준의 내용들
