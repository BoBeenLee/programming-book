# Component testing in Storybook with play functions

- https://www.youtube.com/watch?v=dcuzwCHI940&list=WL&index=5

## Interaction Testing을 이용한 컴포넌트 스토리 만들기

ex) 검색 리스트 컴포넌트 - 컴포넌트 Stories - 기본 검색 리스트 화면 - Only Show Products in stock 버튼을 클릭했을 시 - 검색 입력창에 fruit를 검색했을 시

- 위 예시처럼 상태에 따른 스토리를 play function을 통해 다양한 유저 시나리오를 실제 e2e테스트와 함께 스토리북으로 같이 볼 수 있다.

## Storybook Jest

- play function 내에 jest expect를 통해 성공 테스트 결과를 정의할 수 있다.
  ex) 검색 결과 리스트 아이템 length가 0이어야합니다.

```
expect(await canvas.getAllByRole('row').length).toBe(0);
```
