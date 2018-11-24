
Narendra Shetty - A/B testing with React Native
- https://www.youtube.com/watch?v=kD9o9MKbEbU&t=0s&list=WL&index=3

- Code push 체크
   - 업데이트 전 딱 한번만 그 이후엔 pass

Why A/B testing?
- We're most of the time, wrong about what we think is 'good'.

- We want our feature to be profitable.
- We want customer sentiment to drive product development.
- We want to make product decision based on fact.

Why not A/B testing?
- You don't have sufficient traffic
- Your success metrics are ill defined.

Process of A/B testing.
- Start with an hypothesis
   - Hypothesis !== idea
- Define a metric
   - Data you can measure to prove your hypothesis is right or wrong.
- Build
   - Design & Implement
- Analyze & Learn
   - Build, Measure, Learn

90% tests fail
- ...and sometimes you don't know why tests fail.

A/B Testing Process
- Web VS Native

Web
Ideas - Build - Deploy - Users (1 day)

Native
Ideas - Build - (1-2 weeks) - Submit - (2-3 days) - Review - (2-3 days) - Stable - Users (~3 weeks)

Mobile
Download Update - Splash Screen - Request experiment settings (Server)

"Drink water!" - Mom

Optimizely

Request experiment settings
Request variants

Common pitfalls
- Big shot AB testing
- Fringe AB testing
- Assumed Reproducibility

A/B testing when done right
- Test everything.
- Test atomically.
- Build tools you can trust.
- Question when you don't understand.
- Build a culture of data driven development.
