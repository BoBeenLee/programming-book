# How Core Web Vitals Will Impact Google Rankings in 2021

- https://vercel.com/blog/core-web-vitals#largest-contentful-paint

## What to expect from this talk.

- Background and Introduction
- Core Web Vitals & SEO
- Improving Performance
- Measuring Performance

## Background & Introduction

- Why should you care about web performance?

### 100ms(latency) = 1%(fewer sales) Amazon(2009)

### 100ms(less latency) = 1%(more revenue) Walmart(2012)

## Better perfomance, better SEO

- Beginning this June, Google will add Core Web Vitals to its Page Experience ranking signal. Google announced last year that changes were coming to the way its algorithm ranks pages that went beyond how quickly pages were loaded, safe-browsing, HTTPS, and their mobile-friendliness.

## Core Web Vitals

- How can we measure the actual user experience?

### LCP (Largest Contentful Paint)

- (Loading)
- 2.5~4.0

### FID (First Input Delay)

- (Interativity)
- 100ms ~ 300ms

### CLS (Cumulative Layout Shift)

- (Visual Stability)
- 0.1 ~ 0.25

## Improving Performance

- What are some practical strategies to improve your Core Web Vitals?

### Pre-rendering

- Generate HTML in advance for each page, on the server
- Static Generation or Server-Rendering
- Allow Google to index your content immediately
- "Automatic Static Optimization"
  - if i'm not making any blocking data fetches from my page, we can automatically optimize that to html
    ex) font, inline css

### Optimize Images

- Use width and height to prevent layout shift
- Lazy-load images as they enter the viewport
- Use modern image formats (WebP, AVIF)
- Server correctly sized images using srcset
- Provide blur-up placeholders
- TMI: image optimization을 할때 web assembly를 통해 최적화한다.

### Optimize Fonts

- Use a variable font
- Preload your font file
- Self-host instead of Google Fonts
- Use font-diplay: optional to prevent layout shift

```
<link rel="preload" href="..." as="font" type="font/woff2" crossOrigin="anonymous" />

@font-face {
	font-family: 'Inter';
	font-style: normal;
	font-weight: 100 900;
	font-diplay: optional;
	src: url(/...) format(...);
	...
}
```

## Measuring Performance

- How do we know we improved performance for real users?

## Zeit

ex) https://www.webpagetest.org/result/220710_BiDc0J_3J3/1/details/#waterfall_view_step1
