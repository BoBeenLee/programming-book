
# Storybook 6.5 Insider Preview
- https://www.youtube.com/watch?v=h1S6vTR7hZ8&list=WL&index=18

## Component Encyclopedia

## Major update in 6.5
- Interaction testing (test runner & hooks)
- Perf updates for Webpack builder
- Vite builder updates
- Figma plugin to connect stories to variants


## What's worth testing?
- Visual test
- Interation
- Accessibility
- Composition
- User flows

## Anatomy of a test
- Setup <- provide mock props & data
- Execute <- render the component in isolation
	- Setup, Execute --> Story 
- Verify

## Stories are test cases for everything a component does

## Reuse stories in tests
- Write test cases as stories
- Import into Jest
- Script interactions with Testing Library
- Run assertions with Jest

## But, these tests still run in Node using JSDOM

## If a test fails, all you get is a blob of HTML to debug

## Intercation Testing
- Write tests in your stories file
- Powered by Testing Library & Jest
- Tests run in a real browser

## Debug with playback controls
- Interactions panel visualizes all steps
- Step through the interactions
- Debug tests in the browser

## Execute tests with test-runner
- Run tests in parallel via command line
- Powered by Playwright
- Convert Stories into tests
- Watch mode, filters, etc.

## Cross-browser testing
- It's powered by Playwright so you can run cross-browser tests in parallel.

## Click to debug
- Launch and inspect a failing test in the browser
- Works both locally and on CI

## Automate with Chromatic
- Chromatic will wait for play function to run before capturing the snapshot.

## Testing hooks (experimental)
- Customize or extend the tset runner.
- For example, capture snapshots or run accessiblity checks.

## Accessibility testing with hooks (experimental)
- Can inject axe-playwright into each story and run accessibility checks.

## Interaction testing tutorial
- Write tests in a stories file
- Debug using the interactions panel
- Reproduce error states via URLs
- Automate tests with continuous integration


## Storybook perf roadmap 6.5 Lazy Compilation
- Tools like Next.js defer assembling a page until you need it.
- Your app has many routes, but you'll only visit a few in a dev session, so why pay the cost of compiling all of them upfront?

- Storybook initially compiles only the code for the first story + the runtime.
- The rest of the stories are built progressively as you visit them.

## 파일 캐시, Lazy Compilation 캐시 기능은 Enable feature 설정하면 가능하다.
	- 대충 빌드, warm상태 일때도 속도가 빨라졌다는 의미

## Vite Builder 제공

## Designers have sticker sheets
### Design addon
- Embed Figma files in Storybook to make hand-off easier.

## Connect Storybook and Figma
- Link stories to component variants
- Compare implementation to the design
- Open Storybook from the sidebar

## Steamline Handoff

## Storybook Connect guide
- Setup private projects with access control
- Install plugin
- Link stories to component variants


## My Opinion
프로덕트 운영 개발자라면 해당 feature가 핵심이지 않을까 싶다.
- Interaction testing
- Connect Storybook and Figma
	- 이건 직접 세팅하고 경험해봐야 실제 프로덕트 레벨에서 적용하면 좋을 부분인지 봐야할듯


## Reference
- https://storybook.js.org/blog/interaction-testing-with-storybook/
- https://storybook.js.org/blog/interactive-stories-beta/
- https://testing-library.com/docs/queries/about/#manual-queries




