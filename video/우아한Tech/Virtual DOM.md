# Virtual DOM
- https://www.youtube.com/watch?v=PN_WmsgbQCo

## Virtual DOM의 등장
- 0) 페이지를 서버가 아닌 브라우저에서 관리
- 1) DOM tree를 즉각적으로 많이 변경할 일이 생김
- 2) 전체 페이지를 서버가 아닌 브라우저단에서 자바스크립트가 관리하기 때문에 DOM 조작을 더욱 효율적으로 할 수 있게끔

### QA
- React 18의 React Server Component도 Virtual DOM 목적, 배경에 충족하는가?
	- 굳이 Virtual DOM이 아니어도 되지 않을까?
	- 이유는 Server Component이기에 브라우저에서 관리가 아닌 서버에서 관리하고 내려주기에 
		- 서버에서 관리하고 내려준다하여도 해당 RSC를 받은 브라우저단 자바스크립트에서 렌더링하고 관리하기 때문에 동일하게 Virtual DOM은 필요할것으로 보임.
- Server Side 렌더링도 동일한 목적, 배경을 갖는가?
	- 처음 서버에서 렌더링시엔 연관없으나 Document를 브라우저에 전달한 시점엔 브라우저 단에서 관리하기 때문.

## Virtual DOM이란
- HTML DOM의 추상화 버젼
State Change -> Compute Diff -> Rerender



