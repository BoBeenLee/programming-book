# 5 things you need to know to take your next app to the next level - Ankita Kulkarni

- https://www.youtube.com/watch?v=aZrTL1J25aQ&list=WL&index=7

- SEO with Next.js
- Loading and Redirects
- Incremental Static Regeneration (ISR)
- Image Optimization
- Caching

## SEO

- App is Deployed
- Bot crawls your page
- tries to understand what the page is about
- Rank your page
- Displays your page on Google

## Script Optimization

## Loading and Redirects

- 로그인 후 이동 처리 방법에 대한 예시
- routeChange - is not ideal solution
  - for checking for the loading state and all that, right?

```
 const [isLoading, setIsLoading] = useState(true);
  useEffect(() => {
    const handleComplete = () => {
      setIsLoading(false);
    }
    router.events.on("routerChangeComplete", handleComplete);
    router.events.on("routerChangeError", handleComplete);

    return () => {
      router.events.off("routerChangeComplete", handleComplete);
      router.events.off("routerChangeError", handleComplete);
    }
  }, [router]);

```

- adding the document.cookie value

```ts
<Head>
  <script
    dangerouslySetInnerHTML={{
      __html: `
if(document.cookie && document.cookie.includes("auth")) {
	window.location.href = "/";
}
`,
    }}
  />
</Head>
```

## Incremental Static Regeneration (ISR)

## Image Optimization

- Cache Images on CDN
- Using srcSet to define image sizes

## Caching

## My Opinion

- 심도 깊은 내용은 따로 없었던듯 싶다.
- Loading and Redirects 구현 방법 정도는 참고할법한듯 싶다.
