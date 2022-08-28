# Stop resizing your browser — Storybook viewport

- https://www.youtube.com/watch?v=uydF1ltw7-g&list=WL&index=5&t=1s

## INITIAL_VIEWPORTS을 이용한 각종 디바이스 컴포넌트 대응

```
import { INITIAL_VIEWPORTS } from '@storybook/addon-viewport';

INITIAL_VIEWPORTS
```

## 커스텀한 뷰포트 지원

```
const MY_VIEWPORTS = {
  md: {
    name: 'md-768px',
    styles: {
      width: '768px',
      height: '1080px',
    },
  },
  sm: {
    name: 'sm-640px',
    styles: {
      width: '640px',
      height: '1080px',
    },
  },
};

```

## defaultViewports, 스토리별 뷰포트 disabled, 새로운 뷰포트 설정

## My Opinion

- 단순하면서 강력한 메시지 전달 인상깊었습니다.
- 디폴트 뷰 설정은 모바일 컴포넌트일 경우, 모바일 스토리를 따로 보여줘야할 경우 유용하게 사용할 수 있을듯 싶습니다.
  - 홈페이지 모바일 컴포넌트 적용
