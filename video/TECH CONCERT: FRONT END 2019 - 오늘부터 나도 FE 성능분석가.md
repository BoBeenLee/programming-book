# TECH CONCERT: FRONT END 2019 - 오늘부터 나도 FE 성능분석가

- https://www.youtube.com/watch?v=cpE1dwJgS4c&list=WL&index=2

## 개선 프로세스

- 측정
- 분석
- 최적화
  ...rotation

## 언제까지?

- 목표에 도달할때까지 (초기 로딩 속도 3초?)
  - 네이버는 모바일: 1.5, PC: 2

## 개선해야할 포인트

- 로딩 속도
- 인터렉션
  에라이

## 로딩 속도 측정 / 분석하기

- 핵심은 Waterfall 차트를 어떻게 개선할것인지가 주요 포커스이다.
- Waterfall 차트 높이를 줄이고, 폭을 줄이고, 간격을 땡긴다.
- 마지막으로 총체적으로 점검

## 로딩 속도 개선할 수 있는 간단한 방법

- JS, CSS Merge
  - Combine External JS and CSS
- CSS Sprite
  - 여러 이미지를 하나의 Request로!
- Data URI
  - 캐싱되지 않아도 될 이미지를 HTML요청에 포함시켜서

### 가장 효과적인 방법

- 초기 로딩 시 불필요 없는 자원은 삭제하거나 뒤로(Lazy)
  - 실수로 요청한 자원들
  - 초기 로딩시 필요 없는 JS
    - ex) prefetch, gtag, analytics ...
  - _뷰 포트 바깥에 있는 이미지_
    - 뷰포트 바깥에 있는 이미지를 lazy load하여 나중에 자원 로드
      - ex) carousel
- 브라우저는 호스트당 동시에 연결 할 수 있는 개수가 정해져 있다.
  - request수를 줄어야하는 이유는 도메인 호스트당 커넥션 수가 정해져 있기떄문에 대기하는 상황이 생기게된다.
    - 그러기에 CSS Sprite로 묶어서 이미지 요청을 로드하거나, Data URI로 html 포함시켜서 request를 보내지 않게 하면 성능 개선할 수 있다.
- 폭 줄이기: Request 시간 줄이기
  - Connection, TTFB, Content Download
  - TTFB 중요한 정보
  - Initial Connection
    - HTTP프로토콜마다 Connection활용 방법이 다르다.
      - 웹브라우저 기술로 효과적으로 하기엔 방법이 없다.
        - HTTP2가 정답
  - _Time to First Byte (TTFB)_
    - TTFB가 오래걸린다는 것은 서버 비즈니스 로직이 느리다는것
  - Content Download
    - Content Download가 오래 걸린다는 것은 네트워크 속도가 낮거나, 컨텐츠의 크기가 큰 경우.
      - minify, obfuscation(변수명 변경), gzip
      - gzip적용 (content-encoding: gzip)시 전체 데이터량의 30% 정도 감소
      - _큰이미지 줄이기_
        - 크기에 맞는 사이즈로 가져오기
        - 이미지 포맷(png, webP, jpeg,...), 이미지 메타정보 날리기
      - 하지만, 매의눈을 가진 디자이너가 원하는 이미니는 레티나 (device-ratio: 2)이상
        - picture, source, srcset태그를 사용
        - 레티나 비율에 따라 설정, 현실적
- 간격 땡기기: Request 계단 간격 땡기기
  - TTFB 한바이트받으면 스트리밍을 받으면서 파싱하면서 화면을 그리게된다.
    - HTML, CSS, JS 화면그리기 용도로 만든다. DOM, CSSOM를 조합해서 렌더트리로 구성되면 렌더레이어를 위치를 계산하는것 Layout, Paint
  - head 태그에 포한된 자원은 _병렬로 다운로드_
    - 단점은 병렬로 받을때 모두 받을떄까지 화면이 하예진다.
      - async, defer 속성 설정을 해야함
  - head 태그에 포한된 자원은 모두 실행
  - body태그부터 그리기 시작
  - DOM 구성이 완료되면 DOMContentLoaded이벤트 발생
  - 모든 자원이 로딩완료되면 load이벤트 발생
- 성능 격언
  - head태그에는 CSS와 필수 JS만 넣어라.
  - JS는 body태그 마지막에 넣어라. 중간 중간에 JS를 넣지 마라.
- async, defer
  - DOM제어와 관련이 있는 스크립트는 defer를 이용
  - 의존성이 없는 스크립트는 async
    - ex) google analytics 삽입할때 async로
- CSS가 불러진 다음에 CSS에서 사용하는 폰트, 이미지가 로딩
  - 이를 해결하는 방법으로는 Preload!
    - CSS와 함께 폰트, 이미지가 로딩
  - _Preload로하여 받는것도 아까우기에 HTTP2 Server Push기능을 통해 HTML과 함께 JS, CSS, 이미지 로딩_
    - HTML 다운받을때 HTML, JS, CSS, 이미지를 같이 밀어넣을 수 있다.
    - 왼쪽으로 땡겨서 꽤효과가 있다.
- 이와 같이 했다면 튜닝 1차완료 -> 총제적으로 점검하기
  - 다만 아까같은 과정중 오류에 빠지는 경우가 생긴다.
    - 자원만 땡기면 속도만 올리는거지 사용자에게 가치가 있는것을 제공하지 못한다.
- 체감속도 높이기
  - 중요한 과정 3가지
  - _First Paint(FP): Head태그 종료 후_
    - 흰화면을 얼마나 보느냐
  - First Meaningful Paint(FMP), like LCP: Hero엘리먼트가 보이는 시기
- 서비스 노출될때 어떤 정보를 빠르게 보여주고 노출되지 않게하는것도 가장 중요한포인트다.
- Waterfall _균형감 찾기_
  - 각각의 Request를 균등한 크기로 맞추기
  - 튀는 놈 없애기 (ex) 지나치게 큰 CSS, JS)

## 인터렉션 속도

- 어렵지만 난해한 부분 case by case!
  - 브라우저 Main Thread 괴롭히지 말기
- 문제는 바로 동적 언어인 JS가 DOM을 건들면 기본적으로 Main Thread에 의해 Rendering Pipeline이 동작!

### Redering Pipline 이해하기 (Critical Rendering Path)

JS > Style > Layout > Paint > Composite

- ex) JS로 DOM 변경

1. Style recalculate: DOM의 최종 스타일을 계산
2. Layout: DOM의 배치와 크기 계산
3. Paint: 화면에 그리기
4. Composite: 레이어 조합하기 (Help me GPU!)

Composite는 비용이 작다.

#### Layout발생하는 속성 건드리지 않기

- csstriggers.com
- ex) top이 아닌 transform으로 애니메이션 동작

#### GPU 도움 받기

- CPU(Main Thread)가 아닌 GPU의 도움 받기

- composite
  - 웹페이지는 하나의 거대한 레이어로 구성되어있다.
  - GPU는 각각의 레이어를 합치는 작업을 한다.
  - 이미 그려진것을 통해 레이어를 겹치는데 비용이 굉장히 적은데 이렇기 위해선 각각을 레이어로 구성하는 작업을 해야한다.
    - GPU의 도음을 받기 위해 레이어 만들기
    - 브라우저 *규칙*에 따라 레이어를 구성
    - _명시적으로_ 레이어를 구성하기
      - translate3d, scale3d, matrix3d, will-change,...
- GPU의 Side Effect
  - 레이어를 초기 구성하기 작업은 CPU(Main Thread)가 진행
  - 레이어에 원래 비트맵 정보를 복사하기 때문에 메모리가 2배로 필요하다.
    - 꼭 필요한 부분만 레이어로 만든다.
    - 초기에 부하가 크다.
    - 똑같은걸 복사하기에 메모리 2배가 필요하다.
      - 대표적인 부분은 애니메이션
- 60FPS (Frame Per Seconds) 보장하기
  - 렌더링 파이프가 계속해서 발생하는 경우
  - 1Frame은 16ms내에 완료되어야한다.
- 자바스크립트로 비동기를할때 setTimeout으로하는데 그걸로 했을경우 밀리게 된다.
  - 애니메이션을 위해서는 requestAnimationFrame으로 16ms 주기를 보장.
    - 애니메이션 주기에 대한 성능개선은 requestAnimationFrame으로 한다.
- DOM을 건드리지 않는 JS코드 실행 시간도 동일하게 16ms로 유지한다.
  - 서비스 Biz로직이 대다수...
  - _서비스 개발자가 가장 잘 고칠 수 있다._
- 성능 상식에 대한 회고
  - 어떻게 접근해야하는거 얘기했었는데 발표를 듣고 회고하는 시간
  - 성능 개선은 빠를 수록 좋다.
    - 목표를 정해야한다.
  - 로딩 속도는 수치적으로 빠르면 빠를 수록 좋다.
    - 수치가 높은 것보다는 사용자에게 보여줄 Hero컨텐츠를 빠르게 보여주는게 더 좋다.
  - 특정 부분의 성능을 개선하면 개선한 만큼 성능 향상이 된다.
    - 전체 관점에서 가장많이 사용하는 페이지를 살펴보아야한다. 워터폴 차트의 경우 전체 폭이 줄어줄 수 있도록 필요한 부분을 개선해야한다.
  - 서비스 성능 이슈는 개발자의 무지에서 나온다.
    - 사실 바빠서 신경을 못써서 나온다. 무지는 다른 이야기다.
  - 성능 전문가는 서비스의 성능 개선 포인트를 찾고 개선할 수 있다.
    - 성능개선사항을 누구 보다 잘아는 사람은 서비스를 개발한 담당자이다. 성능 전문가는 찾을 수는 있지만 개선할 수는 없다.
    - 스냅샷, 프로파일링해서 볼순 있지만 발생한 것들의 내용에 대한 코드를 이해하고 수정하는것은 쉬운것이 아니다. 비즈니스로직을 알아야한다.
  - 서비스 성능 개선은 전문성을 갖춘 영역이기에 아무나 할 수 없다.
    - 오늘 강의만으로도 여러분은 충분히 할 수 있다. _노력과 관심이 중요하다._

### QA

- 250kb까지는 js파일, css파일 번들링할때 다운로드할때 이슈가 거의 없다.
  - 정해진것이 아니라 튜닝 과정을 통해 거쳐야한다.
- body 뒤, defer 성능차이는 없다. 상관없다. 다만 defer쓰는게 더 낫다.

## My Opinion

- 성능 상식 회고를 통해 항상 빠른게 좋은건 아니고 목표를 정하고 사용자가 보여줄 콘텐츠를 빠르게 보여주는게 가장 좋은 성능 최적화라는걸 다시금 알게 되었던 영상이었다.
- Waterfall 균형감 찾기, HTTP2 Server Push기능, head 태그에 포한된 자원은 *병렬로 다운로드*에 대해 알게 되었고 HTTP2 Server Push는 한번 보면 좋을듯 싶다.
  - 당근마켓 성능 측정할때 HTTP2 Server Push기능을 쓴듯 싶은 부분이 있었긴했다. 그때 당시 어떻게 HTML다운로드하면서 js, css가 같이 다운?, 밀어넣을 수 있는지 몰랐었지만
