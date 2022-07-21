# 실무에서 바로 쓰는 Frontend Clean Code

- https://www.youtube.com/watch?v=edWbHp_k_9Y&list=WL&index=4

## 실무에서 클린코드의 의의

- 지뢰코드
  - 흐름 파악이 어렵고
  - 도메인 맥락 표현이 안되어
  - 동료에게 물어봐야 알 수 있는 코드
- 실무에서 클린 코드의 의의 = 유지보수 시간의 단축
  - 코드파악 시간, 코드리뷰 시간, 디버깅 시간도 단축 시킬수 있다.
  - 시간 = 자원 = 돈
- '처음엔' 클린했지만 기존 코드에 기능을 추가하는 상황이라면?

## 안일한 코드 추가의 함정

- 기능 추가 요청이 들어왔을때
  - 질문 요청에서 전문가 질문 요청 구현이 추가되었을때 예시
- 클린코드 != 짧은 코드
  == 원하는 로직을 빠르게 찾을 수 있는 코드

### 원하는 로직을 빠르게 찾으려면?

- 하나의 목적을 가진 코드가 흩뿌려져 있어요 - 응집도
- 함수가 여러 가지 일을 하고 있어요 - 단일 책임
- 함수의 세부구현 단계가 제각각이에요 - 추상화

## 로직을 빠르게 찾을 수 있는 코드

- 응집도 - 같은 목적의 코드는 뭉쳐두자
  - 리팩토링 v1
    - custom hooks을 이용하여 useMyExpertPopup 추가
    - 어떤 내용의 팝업을 띄우는지, 어떤 액션을 하는지 숨겨져있기에 오히려 코드파악이 어려워졌다.
      - 훅의 대표적인 안티패턴
    - 뭉치면 쾌적한 영역 - 당장 몰라도 되는 디테일
    - 뭉치면 답답한 영역 - 코드 파악에 필수적인 핵심 정보
- 어떻게하면 읽기좋게 응집할 수 있을까?
  - 코드 응집 Tip: 핵심 데이터와 세부 구현 나누기
  - 리팩토링 v2
    - 핵심 데이터는 밖에서 전달 - 팝업 제목, 내용, 팝업 버튼 Action
    - 나머지는 뭉친다. - usePopup()
- 선언적 프로그래밍
  - 핵심 데이터만 전달받고 세부 구현은 뭉쳐 숨겨 두는 개발 스타일
  - "무엇을 해야할지만 알려줘, 세부 구현은 미리 해놨거든"

```ts
<Popup onSubmit={"질문전송"} onSuccess={"홈으로이동"} />
```

    	- '무엇'을 하는 함수인지 빠른 이해 가능
    	- 세부 구현은 내부에 뭉쳐두어 신경쓸 필요없다.
    	- '무엇'만 바꿔서 쉽게 재사용 가능

- 뭉치지 않았다면? 명령형 프로그래밍

```ts
<Popup>
  <button
    onClick={async () => {
      const res = await 회원가입();
      if (res.success) {
        프로필로이동();
      }
    }}
  >
    전송
  </button>
</Popup>
```

    - 세부 구현이 노출되어있어 커스텀이 쉽지만, 가독성이 어렵고 재사용성이 어렵다.

Q, 선언적인 코드가 무조건 좋은 건가요?
A, 두 방법 모두 유동적으로 사용하시면 됩니다.

- 단일책임 - 하나의 일을 하는 뚜렷한 이름의 함수를 만들자.

  - 함수 이름을 지어보자
    - 중요 포인트가 모두 담겨 있지 않은 함수명은 "위험"
  - 기능 추가 시 함수는 더욱 잡탕이 됩니다.
    - 지뢰코드 유발
  - 리팩토링 Tip1
    - 한가지 일만하는 명확한 이름의 함수로 정의
      - 이를 필요한 상황에서 따로따로 부르면된다. (선언적 프로그래밍을 이용하여 함수들을 쪼개서 호출하게 구현한다.)
  - 리팩토링 Tip2

    - 한가지 일만 하는, 기능성 컴포넌트
    - ex) 버튼 클릭시 서버에 로그를 찍는 기능

      - before 버튼 클릭 함수에 로그 찍는 함수 API들이 섞여있다.
        ```
        <button onClick={async () => {
        	log("제출 버튼 클릭");
        	await openConfirm();
        }} />
        ```
      - after 로그는 버튼을 감싼 컴포넌트에서 찍고, 버튼 클릭 함수에서는 API콜만 신경쓴다.
        ```
        <LogClick message="제출 버튼 클릭">
        	<button onClick={openConfirm} />
        </LogClick>
        ```

    - ex) impression 옵저버를 다는 코드 세부 구현과 API콜을 하는 코드가 섞여 있다.
      - before
      ```
      useEffect(() => {
      	const observer = new IntersectionObserver(
      		([{ isIntersecting }]) => {
      			if(isIntersecting) {
      				fetchCats(nextPage);
      			}
      		}
      	);
      	return () => {
      		observer.unobserve(targetRef.current);
      	};
      });
      ```
      - after - impression 옵저버 세부 구현은 감싼 컴포넌트에 숨겨 두고, 사용하는 입장에서는 impression시 API콜만 신경쓴다.
      ```
      <IntersectionArea onImpression={() => fetchCats(nextPage)}>
      	<div>더 보기</div>
      </IntersectionArea>
      ```

  - 리팩토링 Tip3
    - 조건이 많아지면 한글 이름도 유용해요

- 추상화 - 핵심 개념을 뽑아내자
  - 피카소의 '소' 추상화
    - 구체적인 소 -> 남기고 싶은 개념만!
    - 맵 -> 지하철 노선도의 추상화 (역이름, 역정보만 남긴다.)
  - 프론트엔드 코드의 추상화: 컴포넌트
    - before - 팝업 코드 제로부터 구현
    ```
    <div style={팝업스타일}>
    	<button onClick={async () => {
    		const res = await 회원가입();
    		if(res.success) {
    			프로필이동();
    		}
    	}}>전송</button>
    </div>
    ```
    - after - 중요 개념만 남기고 추상화 (제출 액션, 성공 액션만 남기고 나머지는 추상화)
    ```
    <Popup onSubmit={회원가입} onSuccess={프로필이동} />
    ```
  - 프론트엔드 코드의 추상화: 함수
    - before - 설계사 라벨을 얻는 코드 세부 구현
    ```
    const planner = await fetchPlanner(plannerId);
    const label = planner.new ? '새로운 상담사' : '연결중인 상담사';
    ```
    - after - 중요 개념을 함수 이름에 담아 추상화
    ```
    const label = await getPlannerLabel(plannerId);
    ```

### 얼마나 추상화할 것인가?

- Level 0

```
<Button onClick={showConfirm}>
	전송
</Button>
{isShowConfirm && (
	<Confirm onClick={() => { showMessage("성공"); }} />
)}
```

- Level 1

```
<ConfirmButton onConfirm={() => { showMessage("성공"); }} >
	전송
</ConfirmButton>
```

- Level 2

```
<ConfirmButton message="성공" >
	전송
</ConfirmButton>
```

- Level 3

```
<ConfirmButton />
```

답은 없습니다. 상황에 따라 필요한 만큼 추상화하면 됩니다.

## 추상화에서 유념하면 좋을점

- 추상화 수준이 섞여 있으면 코드 파악이 어려워요.

```
<Title>별점을 매겨주세요</Title> <-- 높은 추상화
<div> <-- 낮은 추상화
	{STARS.map(() => <Star />)}
</div>
<Reviews /> <-- 높은 추상화
{rating !== 0 && ( <-- 중간 추상화
	<>
		<Agreement />
		<Button rating={rating} />
	<>
)}

```

- 전체적인 코드가 어느 수준으로 구체적으로 기술된지 파악할 수 없다.
- 추상화 단계를 비슷하게 정리 추상화 수준이 높은 것끼리, 또 낮은 것끼리 모든다.

## 액션 아이템

- 담대하게 기존 코드 수정하기 - 두려워하지 말고 기존 코드를 씹고 뜯고 맛보고 즐기자.
  - Pull Request에 File Changes를 줄이고 싶다면 Mother branch를 따서 리팩토링한 PR을 추가로 만드는 방법을 사용하면 좋습니다.
- 큰 그림 보는 연습하기 - 그때는 맞고 지금은 틀리다. 기능 추가 자체는 클린해도, 전체적으로 어지러울 수 있다.
- 팀과 함께 공감대 형성하기 - 코드에 정답은 없습니다. 명시적으로 이야기를 하는 시간이 필요합니다.
- 문서로 적어 보기 - 글로 적어야 명확해집니다.
  - 향후 어떤 점에서 위험할 수 있는지
  - 어떻게 개선할 수 있는지

## My Opinion

- 실무적인 관점에서 내가 짠 코드를 한번더 생각하게 되었던 영상이었다.
- 기존 홈페이지부터 한번 훑어보고 적용하기
