
# Tailwind CSS 사용기
- https://fe-developers.kakaoent.com/2022/220303-tailwind-tips/

- utility-first 특성과 장단점은 이미 많은 곳에서 소개가 되고 있고, 저희 팀에서도 장점이 더 많다고 판단하였습니다. 직접 Tailwind를 경험해본 바로는 개발 속도가 빨라지는 장점이 크게 와닿았습니다.
- 스타일 시트를 오가는 컨텍스트 스위칭도 없고, 클래스 이름을 시맨틱하게 정하기 위해 고민해야 하는 시간도 사라졌습니다.

### Arbitrary values 줄이기

### Preflight 처리
- 디자인 시스템을 따라 Tailwind를 적용하다 보면 브라우저에서 기본적으로 설정하는 스타일과 충돌이 발생할 수 있는데, 이를 피하고자 브라우저에서 기본적으로 설정하는 스타일을 무효화 혹은 백지화하는 것입니다.
- normalize.css과 동일한 기능을 의미하는듯함.

### 컴포넌트에 className으로 직접 스타일 설정하기

### 컴포넌트에 className props를 추가할 때 흔히 겪는 문제

#### Tailwind Class의 우선순위

### twin.macro 동작 원리

- 요약하면, className에 선언된 클래스의 CSS 속성을 key로 하여 key에 값을 덮어쓰는 원리입니다. className의 앞에 선언된 class부터 일종의 맵처럼 CSS 속성을 key로, 값을 value로 하여 Object에 덮어쓰는 과정을 반복합니다. 이 과정에서 key가 같아서 경합이 발생하면 뒤에 선언된 스타일이 앞에 선언된 스타일을 덮어씁니다.

- 같은 속성의 스타일을 하나의 요소에 중복으로 설정하더라도 결과를 명확히 예측할 수 있기 때문에 생산성 측면에도 도움이 됩니다.
ex) 
```
<div className="text-red-400 text-blue-400">Hello world</div>
```
