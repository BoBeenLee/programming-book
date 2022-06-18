
## Mediator-Middleware Pattern
- https://www.patterns.dev/posts/mediator-pattern/

- 중앙 중재자 개체를 사용하여 구성 요소 간의 통신을 처리합니다.
- 중재자 패턴을 사용하면 구성 요소가 중앙 지점인 중재자를 통해 서로 상호 작용할 수 있습니다. 중재자는 서로 직접 대화하는 대신 요청을 수신하고 전달합니다! JavaScript에서 중재자는 객체 리터럴이나 함수에 불과한 경우가 많습니다.

ex1) 이 패턴을 항공 교통 관제사와 조종사 간의 관계
- 항공 교통 관제사는 모든 항공기가 다른 항공기와 충돌하지 않고 안전하게 비행하는 데 필요한 정보를 수신할 수 있도록 합니다.

ex2) 채팅룸의 예시, 챗룸에서의 유저는 각유저에게 직접말하진 않는다. 대신에 챗룸이 유저간의 중재자로 제공한다.

## Case Study
- Express에서 사용하는 middleware 패턴입니다.
- request-response 사이클에서 next 콜백을 호출합니다.
- 모든 통신이 하나의 중심점(central point)을 통해 흐르도록 함으로써, 미들웨어 패턴은 객체간 다대다 관계를 단순화하여 쉽게 만들어줍니다.

## Usecase
- express와 유사하게 json rpc 통신에서도 미들웨어 패턴을 사용하여 처리합니다.
	- https://github.com/MetaMask/eth-json-rpc-middleware

