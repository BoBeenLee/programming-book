[Practical Performance - Yedidya Kennard](https://www.youtube.com/watch?v=0K4rFogLviw&t=904s)

- React Native can be fast... But it's up to us to help it
- Measure!
- Without measuring you don't know if you're improving the things that really matter
- Performance problems only show up when things get complicated
- Single thread means problems pile up!
- And then it's really hard

- What can we measure?
  - JS Bundle Size
  - App loading time
  - Unnecessary renders
  - JS thread time
  - Frame rate - JS + Native
  - Render time
  - Android overdraw
  - HTTP requests


- PureComponent
- But what if the data is dynamic?
- Pass individual props || pass the full object
- shouldComponentUpdate

What tools do we have?
- console
- Chrome Dev Tools
- systrace
- Detox Instruments
- react-native-js-profiler
- ...


