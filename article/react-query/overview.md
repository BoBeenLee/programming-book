# react-query
- https://react-query.tanstack.com/overview

- 누락된 데이터 호출 라이브러리로 설명되지만 서버 상태 업데이트, 캐싱, 동기화를 쉽게 만들어줍니다.

## Motivation

- 리액트는 데이터 호출, 업데이트에 대한 방법을 제대로 제공하지 않습니다.
  - 리액트는 렌더링 라이브러리이기에
- 컴포넌트 기반 상태와 함께 리액트 훅을 이용하여 저장하는 더 보편적인 상태관리 목적과 앱 내에 비동기 데이터방식을 제공합니다.

- 대부분의 전통적인 상태관리 라이브러리는 client상테와 함께 작동합니다.
- 그들은 async, server state 작동에는 좋지는 않습니다. 왜냐면 server state는 전적으로 다르기 떄문입니다. 처음 시작하는 사람을 위한 서버 상태란
  - 제어하거나 갖고 있지 않는 위치에 원격으로 유지합니다.
  - 가져오거나 업데이트를 위해 비동기 API가 필요합니다.
  - 공유 소유권을 가지며, 알게모르게 다른사람에 의해 (상태를) 변경할 수 있습니다.
  - 주의하지 않으면 당신의 앱은 오래된 상태가 될 수 있습니다.

- 서버 상태의 특성을 파악하면, 더 많은 챌린지가 너에게 다가올것입니다.
- 예를들면,
  - 캐싱
  - 하나의 API에서의 다수 요청에 대한 디커플링
  - 백그라운드시 데이터 만기에 대한 업데이팅
  - 데이터 업데이트는 최대한 빨리 반영
  - 페이지네이션, lazy loading데이터와 같은 퍼포먼스 최적화
  - 메모리 관리, 서버 상태 가비지 콜렉션
  - 구조적으로 공유를 통한 query 결과를 기억하는것
- React Query는 server state 관리를 위한 best libraries입니다.
- 구성 없이 즉시 사용 가능하고 놀라울 정도로 잘 작동하며 애플리케이션이 성장함에 따라 원하는 대로 사용자 정의할 수 있습니다.
- 컨트롤하기 전에 까다로운 문제와, 서버 상태의 허들, 앱 데이터를 컨트롤합니다.
- 다음과 같은 작업을 수행할 가능성이 높습니다.
  - 복잡한 많은 라인들을 제거하고 당신의 앱으로부터 이해 불가능한 부분에 도움을 줄수 있고 React Query 로직 라인이 다루기 힘든부분을 대체합니다.
  - 유지가능한 앱을 만들어주며 서버 상태의 결합없이 새로운 feature를 개발함에 손쉽게 만들어줍니다.
  - 빠른 체감과 전보다 더 좋은 반응성으로 엔드유저에게 직접 영향을 줍니다.
  - 잠재적으로 대역폭을 절약하고 메모리 성능을 높이는 데 도움이 됩니다. 

### Comparison
- https://react-query.tanstack.com/comparison

## QA
- SDK 호출에 대한 Promise 부분도 react-query 동작이 동일한가?