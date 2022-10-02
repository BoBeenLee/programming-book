# Webpack Module Federation 도입 전에 알아야 할 것들

- https://fe-developers.kakaoent.com/2022/220623-webpack-module-federation/?fbclid=IwAR2KiuO3LIOM9gst6dNH3Tl-ShA1fhlJy1akzsQWjcNc9q1xXWkkk54QhGA

## 정의

- Module Federation은 단일 Webpack 빌드에 포함된 모듈뿐만 아니라 여러 서버에 배포되어 있는 원격 모듈을 하나의 애플리케이션에서 로딩할 수 있는 기능
- Module Federation을 정의하면, 리모트 앱이 노출(Expose)한 원격 모듈을 호스트 앱에서 비동기 로딩하여 사용할 수 있는 도구

- examples
  - https://github.com/module-federation/module-federation-examples

## 용어 정리

- 로컬 모듈은 단일 Webpack 빌드에 포함되는 모듈이다. 서로 다른 Webpack 빌드의 결과물은 서로 다른 로컬 모듈이다. 로컬 모듈은 단일 빌드 안에서만 로딩할 수 있다.
- 원격 모듈은 다른 Webpack 빌드에서 만든 모듈을 대상으로 런타임에 로딩할 수 있는 모듈을 말한다. 즉 A 빌드와 B 빌드의 결과물은 서로 원격 모듈이 될 수 있다. 각 빌드는 개별 서버에 배포될 수 있으며 런타임에 Dynamic Imports하듯이 원격 모듈을 로딩할 수 있다.
- 컨테이너(Container) 는 각각의 빌드를 말하며 하나의 빌드가 하나의 웹 애플리케이션을 나타낸다. A 컨테이너는 B 컨테이너의 원격 모듈을 로딩할 수 있으며 B에서 A 방향으로도 로딩할 수 있다.
  - Expose는 컨테이너가 외부에 노출한 원격 모듈의 목록을 나타내는 설정이다. 간단하게는 내보낼 모듈이름: 로컬 모듈 경로로 표현할 수 있으며 Webpack 설정의 일부를 보면 이해가 빠를 것이다.
  - 공유 모듈은 여러 컨테이너에서 같이 사용하는 모듈을 말하며 런타임에 한 번만 로딩된다. 예를 들어 여러 컨테이너에서 react를 사용한다면, react 모듈을 여러 번 로딩할 필요는 없다.
- 리모트 앱은 모듈을 Expose하는 컨테이너이고, 호스트 앱은 원격 모듈을 사용하는 컨테이너이다.

## 왜 필요한가?

- 서비스 규모가 커질수록 작은 변경에도 영향 범위가 커질 수 있으며 영향 범위 예측도 점점 복잡하고 어려워진다. Module Federation은 컨테이너 빌드를 따로 하므로 빌드 시간, 영향 범위, 로딩 시간 측면에서 유리하다.
  - 변경된 컨테이너만 빌드하고 변경 영향이 있는 컨테이너에만 테스팅하며 해당 컨테이너만 새로 로딩해야할때
  - 즉 독립적인 빌드하여 결합도를 낮출 수 있는 상황일 경우

## Module Federation의 동작 원리

- 호스트 앱(app1)의 Webpack 설정

```
new ModuleFederationPlugin({
  name: "app1",
  remotes: {
    app2: `app2@http://localhost:3002/remoteEntry.js`,
  },
}),
```

- 호스트 앱에서 원격 모듈 사용

```
// "app2"라는 이름으로 원격 모듈임을 나타낸다.
const RemoteButton = React.lazy(() => import("app2/Button"));
```

- 정리하면 호스트 앱이 리모트 앱의 remoteEntry.js를 로딩하고 app2와 같이 리모트 앱의 컨테이너 이름을 파악한다. 그러면 비동기 로컬 모듈처럼 원격 모듈을 로딩할 수 있다.

## 단점

- 원격 모듈의 타입을 알기 어렵다.
  - monorepo로 구성했을 경우 tsconfig reference설정이나 package.json, webpack config 설정을 통해 해결할 수 있다.
  - monorepo가 아닐 경우 @module-federation/typescript 라이브러리를 이용하여 타입을 자동으로 생성이 가능하다.
- 배포 시 remoteEntry.js 경로 처리
  - 빌드 및 배포할 때 리모트 앱의 remoteEntry.js 파일 경로를 목적별 서버(예> local, dev, alpha, stage, real 등)에 맞게 작성해야 한다.
    - 해당 부분은 크게 어려운 부분은 아닌듯함.

## 요약

- 웹 애플리케이션의 규모가 점점 커짐에 따라 빌드 속도와 배포 속도, 변경에 대한 영향 범위를 제한하고 검증하는 것이 중요해지고 있다. Module Federation은 (다른 도구를 사용하지 않고)Webpack만으로 마이크로 프런트엔드를 구현할 수 있게 해주었고, 여러 컨테이너를 독립적으로 빌드, 검증, 배포할 수 있으므로 속도와 영향 범위 측면에서 큰 장점을 제공한다.

## My Opinion

- monorepo와 module federation의 결합으로 독립적인 빌드, 테스트 환경을 구축할 수 있고 원격 모듈 타입까지 체킹이 가능하여 규모가 큰 서비스에선 큰 이점을 발휘할 수 있을것으로 보입니다.
- nextjs의 유사한? feature부분으로는 [url-imports](https://nextjs.org/docs/api-reference/next.config.js/url-imports)가 있습니다.
