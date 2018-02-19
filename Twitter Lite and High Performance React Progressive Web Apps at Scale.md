[Twitter Lite and High Performance React Progressive Web Apps at Scale](https://medium.com/@paularmstrong/twitter-lite-and-high-performance-react-progressive-web-apps-at-scale-d28a00e780a3)


- Use Route-Based Code Splitting
  - split code vendor, manifest Webpack  CommonsChunkPlugin 

- Avoid Functions that Cause Jank
  - Jank?
  - VirtualScroller

- Use Smaller Images
  - we’ve reduced the size of our images 
  - best image size : about 16.667ms (1 frame)

- Optimizing React
  - Make use of the shouldComponentUpdate method
  - Defer Unnecessary Work until componentDidMount
    - By deferring non-essential code paths from `componentWillMount` to `componentDidMount`, we saved a lot of time to render Things.
    - https://gist.github.com/paularmstrong/cc2ead7e2a0dec37d8b2096fc8d85759#file-defercomponentrender-js
  - Avoid dangerouslySetInnerHTML
  - Defer Rendering When Mounting & Unmounting Many Components

- Optimizing Redux
  - Avoid Storing State Too Often
    - By removing the draft Tweet state from updating the main Redux state on every keypress and keeping things local in the React component’s state, we were able to reduce the overhead by over 50% (above, right).

  - Batch Actions into a Single Dispatch
    - https://github.com/paularmstrong/normalizr
    - https://www.npmjs.com/package/redux-batch-enhancer
- Service Workers
  - Pre-Cache Assets
  - Delay ServiceWorker Registration
