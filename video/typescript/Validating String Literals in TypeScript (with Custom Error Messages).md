# Validating String Literals in TypeScript (with Custom Error Messages)

- https://www.youtube.com/watch?v=EUU_FsWDGpA

타입스크립트 문자열 유효성 검사 & 타입 에러 메시지 표기 방법

```
type NoEmptyString = "Metric names should not be and empty string"

type DisallowedChars = '\n' | ' ' | '"' | "'" | '-';
type MetricName<T extends string> =
T extends `${string}${DisallowedChars}${string}` ? never :
   T extends Lowercase<T> ? T extends "" ? NoEmptyString : T : never;

function incrementMetric<T extends string>(_metric: MetricName<T>) { }

incrementMetric("hello")
incrementMetric("Hello")
incrementMetric("He'llo")
incrementMetric("He llo")
incrementMetric("")
```
