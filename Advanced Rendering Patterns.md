Advanced Rendering Patterns: Lydia Hallie
- https://www.youtube.com/watch?v=PN1HgvAOmi8&list=WL&index=1

A revolutionary -> Develop -> Ship -> Impressed users -> Change the world

Using the right rendering patterns
SSG ISR SSR Streaming SSR
Edge Rendering Statis Rendering RSC

## Core Web Vitals
- Time to First Byte
Time it takes for a client to receive the first byte of page content

- First Contentful Paint
Time it takes the browser to render the first place of content after navigation

- Largest Contentful Paint
Time it takes to load and render the page's main content

- Time to interactive
Time from when the page starts loading to when it's reliably responding to user input quickly

- Cumulative Layout Shift
Measures visual stability to avoid unexpected layout shift

- First Input Delay
Time from when the user interacts with the page to the time when the event handlers are able to run

## Developer Experience
- Fast build times
The project should build fast for **quick iteration and deployment**

- Low server costs
The website should **limit and optimize the server execution time** to reduce execution costs

- Dynamic content
The page should be able to **load dynamic content performantly**

- Easy rollbacks
A project's deployment can **easily be reverted** to a previous version


- Reliable uptime
Users should **always be able to visit your website** through operational servers

- Scalable infrastructure
Your project can **easily grow or shrink** without running into performance issues

### Static Rendering
- HTML gets generated at build time
- Easily cacheable by CDN/Vercel Edge Network

Best for pages that:
- do **not contain request-based data**

#### Plain Static Rendering
Best for pages that:
- do **not contain dynamic data**
- do **not require request-based data**
- are **not user-specific**
- can be **cached globally**

**Step By Step**<br/>
Step1 - Client requests HTML from server<br/>
Step2 - Server returns HTML, Edge caches response<br/>
Step3 - Browser parses and renders content<br/>
Step4 - Client requests JS bundle from server<br/>
Step5 - Browser hydrates elements

#### Static with Client-Side fetch
Best for pages that:
- contain **data that should refresh on every page load**
- contain **stable placeholder components**

#### Static with getStaticProps

Best for pages that:
- contain **data that is available at build time**
- are **not user-specific**
- can be **cached globally**

#### Incremental Static Regeneration
- Generate some pages at build time, others on-demand
- Easily cacheable by CDN
- Automatically invalidate cache/regenerate pages
- Reduce build times

Best for pages that:
- should be **regenerated on a certain interval** or **on-demand**
- are **not user-specific**
- can be **cached globally**

#### On-demand Incremental Static Regeneration
- Generate some pages at build time, others on-demand
- Easily cacheable by CDN
- invalidate cache/regenerate pages on-demand
- Reduce build times

Best for pages that:
- should be **regenerated based on certain events**
- are **not user-specific**
- can be **cached globally**

### Server-Side Rendering
- HTML page is generated on every request
- getServerSideProps runs on every reqeust
- Returned content is always unique

Best for pages that:
- contain **highly personalized content**
- use **request-based data**, such as cookies
- should be **render-blocking**

### Optimizing SSR Performance
- Avoid long getServerSideProps execution
- Deploy serverless functions in a region close to your database
- Add Cache-Control headers (if you really can't use ISR)
  - Incremental Static Regeneration can:
    - Persist pages between deployments
    - Automatically take care of cache invalidation
    - Share the recomputed page globally across the edge
    - Always serve page from cache, even when database/API is down
  - Server-Side Rendering can:
    - Generate page based on request data
    - Always serve unique page
- Upgrade server hardware

### Streaming SSR + React Server Components
- Zero client-side Javascript needed
- Render React component on the server
- Combine a static page with dynamic components

Best for components that:
- use large dependencies
- require request-based data
