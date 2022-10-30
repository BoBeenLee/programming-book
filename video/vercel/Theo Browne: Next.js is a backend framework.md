# Theo Browne: Next.js is a backend framework
- https://www.youtube.com/watch?v=W4UhNo3HAMw

## Backends do a lot
- Send emails
- Handle requests
	- Return data
	- Return HTML
	- Return nothing
- Process events
- Process non-events
- Read data from database
- Write data to database
- And so much more

## Database -> User
- DB Accessed
- Request Processed
- Request Authorized
- HTML Sent To User
- React runs updates

## Nextjs Does a lot too
- Generates HTML
	- getServerSideProps (on request)
	- getStaticProps (on build)
- Handles requests and responses
	- /pages/api
- Redirects, middleware and more

## How much compute can you block on?

## Serverless Ready
- Page requests
- GraphQL endpoints
- Authentication
- Webhooks
- API calls

## Not Serverless Ready
### Things That scare Theo
- Websockets
- CRON jobs
- Event queues
- Large file storage

### 위 scaring한 부분은 어떻게 nextjs 환경에서 컨트롤할 수 있는가?
- Websockets
	- Pusher, Liveblocks, Ably, Pubsub
- CRON Jobs
	- Github Actions, Zeplo, Upstash
- Event queues
	- SQS, Zeplo, Upstash
- Large file storage
	- S3 presigned URLs

## NextJS is where your users and your servers meet
- 왜 해당 부분이 특별하냐면 Nextjs는 Backend Framework이기에 

## My Opinion
- Nextjs를 이용한다면 어느정도 익숙?한 내용들이였고 간단명료하게 Workflow를 잘설명해준 영상
    - 처음 입문하는 분들께 좋은 영향을 주지 않을까 싶다.
- Nextjs에서 지원하지 않는 환경에 대한 컨트롤, 고민을 대체할 수 있는 서비스들을 제안해주어 일부 유익?한듯 싶은 영상이었다.