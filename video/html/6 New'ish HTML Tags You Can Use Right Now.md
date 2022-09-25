# 6 New'ish HTML Tags You Can Use Right Now

- https://www.youtube.com/watch?v=CvwbinzWSgs&list=WL&index=1

## datalist -> autocomplete

- https://caniuse.com/?search=datalist

```
<form>
	<input type="text" placeholder="which username??" list="usernames" />

	<datalist id="usernames">
		<option value="jack" />
	</datalist>
</form>
```

## details -> accordian

- https://caniuse.com/?search=details
- IE 11이하 제공하지 않음

```
<details>
	<summary>How long are you open?</summary>
	<p>We are open 24 hours a day!</p>
</details>
```

## dialog -> modal

- https://caniuse.com/?search=dialog
- IE 11이하 제공하지 않음
- showModal() 함수를 이용하여 모달을 띄울 수 있다.
- https://github.com/alpinejs/alpine 를 활용한 예시

```
<style>
	dialog::backdrop {
		background: rgba(0,0,0,.6);
	}
</style>

<div x-data>
	<p>
		<button @click="$ref.dialog.showModal()">Proceed</button>
	</p>
	<dialog x-ref="dialog">
		<p>Are you sure about that?</p>
		<div>
			<button>Yes</button>
			<button @click="$ref.dialog.close()">No</button>
		</div>
	</dialog>
</div>
```

## figure, figcaption

- https://caniuse.com/?search=figure
- 블로그 게시글(이미지 캡션, 코드 포맷, 인용문구 등등)과 같은 부분에서 쓰인다.

```
<figure>
	<img src="https://picsum.photos/400/400" alt="" />
	<figcaption>Some random photo that I can't describe.</figcaption>
</figure>

<figure>
	<figcaption>example.php</figcaption>
	<pre>
		$name='jeff';
		echo $name;
	</pre>
</figure>

<figure>
	<figcaption>shakeshake</figcaption>
	<blockquote>
		To be or not to be...
	</blockquote>
</figure>
```

## picture

- https://caniuse.com/?search=picture
- IE 11이하 제공하지 않음
  - picture내 img태그를 넣어 default 설정으로 브라우저 호환성을 유지시킬수 있다.

```
<picture>
	<source media="(max-width: 720px)" srcset="https://picsum.photos/200/200" />
	<source media="(min-width: 1024px)" srcset="https://picsum.photos/400/400" />
	<img src="https://picsum.photos/100/100" alt="" />
</picture>
```

## My Opinion

- picture, figure는 현업에도 쓰일 수 있는 태그로 보여집니다.
- 나머지 datalist, details, dialog는 브라우저 호환성 기준만 잘 맞는다면 구현없이 해당 태그 선언으로 간단하게 기능 구현이 가능할 것입니다.
