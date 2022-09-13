# new INFER features in TypeScript 4.8!

- https://www.youtube.com/watch?v=4eszSJK2LxA&list=WL&index=12

## Improved Inference for infer Types in Template String Types

- https://devblogs.microsoft.com/typescript/announcing-typescript-4-8/#improved-inference-for-infer-types-in-template-string-types

```ts
// TS 4.6
type OnlyStringReturnType1<T> = T extends (...args: any[]) => infer R ? R extends string ? R : never : never;

type A1 = OnlyStringReturnType2<() => "one" | "two">;
type B1 = OnlyStringReturnType2<() => Promise<string>>;


// TS 4.7
type OnlyStringReturnType2<T> = T extends (...args: any[]) => (infer R extends string) ? R : never;


type OnlyStringReturnType3<T> = T extends (...args: any[]) => infer R ? R extends Promise<infer U> ? U extends Array<infer S> ? S extends string ? S : never : never : never : never;

type X = OnlyStringReturnType3<() => Promise<Array<"email" | "sms">>>;


// TS 4.8
// specific한 타입을 추출해낼 수 있다.
type Multipler<T> = T extends `${infer U extends number}x` ? U : never;

type M = Multipler<'2x' | '3x' | '4x'>;

type NYAreacode = 934 | 680 | 332 | 838;

type NYPhoneNumber<T> = T extends `${infer P1 extends NYAreacode}-${infer P2 extends number}-${infer P3 extends number}` ? [P1, P2, P3] : never;

type X = NYPhoneNumber<'680-456-7890'>;

// 4.7일 경우, [NYAreacode, number, number]
// 4.8일 경우, [680, 456, 7890]

```
