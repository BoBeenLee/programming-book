# What even is "the edge"? Edge networks/functions/compute explained

- https://www.youtube.com/watch?v=PBgFgMFQ55E&list=WL&index=7&t=7s

## Waht event is the Edge?

- History - why are we here?
  - Server
  - Cloud -> AWS
    - i don't wanna manage server
  - Cloud Native
  - Serverless - Only pay for what you use - scale to zero - 2015
    - AWS Lambda Function
  - Serverless 1.0
    - Stateless vs stateful
    - Solve Black friday / ecommerce
    - Server-side rendering (getServerSideProps)
    - Request -> spinning up compute HTML
    - 50mb lambda function
    - "cold start" -> 200ms - 1s / 50mb 2-3s
      - regionality / customer located
  - Serverless 2.0 / Edge
- Edge Network vs. CDN
  - Content Delivery Network -> cache assets close to your customer
  - Read-only (Html, JS, CSS)
  - Run code -> dynamically compute
- Edge "Compute"?
  - Some code you can run
  - **Global**
- Edge Middleware

  - Personalization
  - A/B testing
  - Feature flags
  - i18n / localization

- Edge API Routes / Edge SSR
- Edge vs. Serverless
- Ecosystem
  - Storage
    - cache storage (key/value)
    - persisted storage (database, SQL)
- Pros and cons
- Regional vs global
- edge runtime vs node runtime

- draw
  - https://drive.google.com/file/d/1A85Xo7lPGC2wK5vXBSzHmJ-JzCErDSe5/view?usp=sharing

ex) edge location

- https://react-on-the-edge.vercel.app/
