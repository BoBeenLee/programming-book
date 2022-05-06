[TypeScript tips and Tricks with Matt](https://www.youtube.com/watch?v=hBk4nV7q6-w&list=WL&index=12)

### generic typescript

```typescript
export cosnt getDeepValue = <TObj, 
TFirstKey extends TObj, 
TSecondKey extends TObj[TFirstKey]>(obj: TObj, firstKey: TFirstKey, secondKey: TSecondKey) => {
    return obj[firstKey][secondKey];
}

const obj = {
    foo: {
        a: true,
        b: 2,
    },
    bar: {
        c: "12",
        d: 10,
    },
};

const value = getDeepValue(obj, "foo", "b");
typeof value === "number";
```

- let's say the object is from api response, do i need to explicitly write the api response type?

zod example
```typescript
import { z } from "zod";

const Data = z.object({
    id: z.string(),
    name: z.string(),
});

type DataType = z.infer<typeof Data>;


interface DataFromApi {
    id: string;
    name: string;
}

fetch("/something")
    .then(res => res.json())
    .then(result => {
        const data = Data.parse(result);
    });
```

conditional-types
```typescript
type Animal = {
    name: string;
};

type Human = {
    firstName: string;
    lastName: string;
};

type GetRequiredInformation<TType> = TType extends Animal ? { age: number; } : TType extends Human ? { socialSecurityNumber: number; } : TType extends { planet: string } ? { whyAreYouHere: string; } : never;

export type RequiredInformationForAnimal = GetRequiredInformation<Animal>;

export type RequiredInformationForHuman = GetRequiredInformation<Human>;

export type RequiredInformationForAlien = GetRequiredInformation<{ plane: string; }>
```


- search-params-decoding
```typescript
import { String, Union } from "ts-toolbelt";

const query = `/home?a=foo&b=wow`;

type Query = typeof query;

type SecondQueryPart = String.Split<Query, "?">[1];

type QueryElements = String.Split<SecondQueryPart, "&">;

type QueryParams = {
    [QueryElement in QueryElemennts[number]]: {
        [Key inn String.Split<QueryElement, "=">[0]]: String.Split<QueryElement, "=">[1];
    };
}[QueryElemennts[number]];

const obj: Union.Merge<QueryParams> = {
    a: "foo",
    b: "wow",
};
```