# Breaking words with wbr and &shy;

- https://www.youtube.com/shorts/HsCOhsqzimg

- 반응형으로 화면을 구현할 경우 원하는 기준에서 개행하고 싶은 경우가 필요해진다.
  - ex) 데스크탑, 테블릿, 모바일에서 개행하는 위치가 word단위가 아닌 단락 그룹 단위로 개행하고 싶거나 하는 경우가 종종 생기곤합니다.
- 피그마, 제플린 화면과 동일하게 개행하여 표기하고 싶은 니즈가 가끔씩 생기곤한다.
  - 콘텐츠 스타일을 유지하기위해 개행을 원하는 위치에 하고 싶은 니즈

## wbr tag

- https://www.geeksforgeeks.org/html-5-wbr-tag/#:~:text=The%20tag%20in%20HTML,place%20for%20fitting%20the%20text.

## example

- ./wbr-shy.html

## My Opinion

- 예전에 홈페이지 만들때 template literals로 개행 포함하여 모바일, 데스크탑 문구를 따로 두어 처리를 했었습니다.
- wbr, &shy태그를 잘 활용하면은 피그마 구현과 동일하게 문구단락 표현을 유지한채 진행할 수 있을거같습니다.
  - 다만 약간의 요령이 필요해보임.
