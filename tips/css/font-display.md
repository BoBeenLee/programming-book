# font-display

- https://css-tricks.com/almanac/properties/f/font-display/

- font-diplay는 폰트 파일을 어떻게 로드되는지를 정의하고 브라우저에 보여준다. 커스텀한 폰트 정의안에 font-face rule이 함축되어있다.

```
@font-face {
  font-family: 'MyWebFont'; /* Define the custom font name */
  src:  url('myfont.woff2') format('woff2'),
        url('myfont.woff') format('woff'); /* Define where the font can be downloaded */
  font-display: fallback; /* Define how the browser behaves during download */
}
```

## Values

- 5가지의 속성 값이 존재한다.
- auto (default): 브라우저는 로딩하는동안 기본적인 메소드를 사용하고 대부분 block 값과 유사하게 동작할 것입니다.
- block: 글꼴이 완전히 다운로드될 때까지 텍스트를 잠시 숨기도록 브라우저에 지시합니다. 더 정확하게 말하면 브라우저는 보이지 않는 자리 표시자로 텍스트를 그린 다음 로드되는 즉시 사용자 정의 글꼴로 교체합니다. 이것은 "보이지 않는 텍스트의 플래시" 또는 FOIT라고도 합니다.
- swap: 사용자 정의 글꼴이 완전히 다운로드될 때까지 대체 글꼴을 사용하여 텍스트를 표시하도록 브라우저에 지시합니다. 이것은 "스타일이 지정되지 않은 텍스트의 플래시" 또는 FOUT이라고도 합니다.
- fallback: auto와 swap 사이의 절충안의 값입니다. 브라우저는 100ms동안 텍스트를 숨기고 만일 다운로드가 다되지 않았을 경우, fallback 문자를 사용할것입니다. 다운로드 후 새 글꼴로 교체되지만 짧은 교체 기간(대략 3초) 동안에만 가능합니다. 이후엔 교체가 안됨.

- optional: 대체와 마찬가지로 이 값은 브라우저에 처음에 텍스트를 숨긴 다음 사용자 정의 글꼴을 사용할 수 있을 때까지 대체 글꼴로 전환하도록 지시합니다. 그러나 이 값을 사용하면 브라우저가 사용자의 연결 속도를 결정 요소로 사용하여 사용자 정의 글꼴이 사용되는지 여부도 결정할 수 있습니다.

## Why We Need font-display

- font-face 등장 이후로 어떻게 폰트는 다운로드하여 보여줄 것인지 선택할 수 있게 해줍니다.

## font-display 속성을 사용한 최적화

- 텍스트가 항상 보이게 하려면 FOUT와 동일하게 작동하는 swap 옵션을 사용한다. fallback 옵션과 optional 옵션을 사용하면 100ms 동안 텍스트가 보이지 않지만 매우 짧은 시간이어서 이 옵션들도 최적화에 사용할 수 있다.
  - https://d2.naver.com/helloworld/4969726
