# What’s the Difference Between Returning an Array and an Object?
- https://javascript.plainenglish.io/react-hooks-whats-the-difference-between-returning-an-array-and-an-object-34ccba62b71


- 작은 차이점은 사용성에 큰변화를 준다.

- 자신의 커스텀 훅을 object를 리턴해서 쓸것입니다.

- 다른 훅들을 보면 object destructuring을 사용하지 않습니다.
    - Array를 이용합니다.

- 차이점은 무엇인가?
    - 반환 방법의 두 변수는 동등하게 유효한 방법이고 경우에 따라 다르게 가집니다.

## {x}와 [x] 의 차이점
- [x] 배열을 반환한다면 반환된 배열은 너가 정의한 이름을 사용할것입니다.
- {x} 오브젝트를 반환한다면 너는 hooks에 의한 같은 변수이름을 사용할 것입니다.

- 다만 오브젝트를 반환해도 overwrite하여 이름을 다시 정의할 수 있지만 배열 반환보다 더많은 노력을 들여야할 것입니다.

## Use Cases
- 만일 한 컴포넌트에 하나의 훅 여러 객체를 사용한다면(ex) useState) 배열 반환이 적합합니다.
- 하나의 hook에 한개의 객체만 사용한다면 오브젝트 반환이 적합합니다. 