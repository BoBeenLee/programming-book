# GitFlow vs Trunk-based 협업방식

- https://www.youtube.com/watch?v=EV3FZ3cWBp8

- GitFlow / Github Flow / Trunk-based / Gitlab Flow

## GitFlow

1. main, 2. develop, 3. feature, 4. release, 5. hotfix

### Normal

```
main v0.9
|
develop
| |
| feature/guild
| |
merge
|
release
|
each merge
| |
| |
develop main v1.0
```

### Hotfix

```
main v1.0
|
hotfix
|
 each merge
| |
| |
develop main v1.0.1
```

- 안정적으로 버젼별 배포 가능
- CI/CD 이런거하는곳은 안좋아함?

## Trunk-based

- "브랜치 하나만 잘 관리하자"

```
main
|
feature1
|
merge
|
main
```

- 많은 테스트해야함
- 테스트 자동화 필수
