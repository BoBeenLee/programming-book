# Typescript Error Handling

- https://www.youtube.com/watch?v=UdekNaCXt6w&list=WL&index=11&t=103s

```ts
// error.ts
export type MyError {
    message: ErrorMessages;
    resolution?: string | undefined;
}

export const enum ErrorMessages {
    DBError = "error occured while dealing with db."
};

export const isError (toBeDetermined: any | MyError): toBeDetermined is MyError => {
    return Boolean((toBeDetermined as MyError)?.message);
}
// user.ts
export const getUser = ():Promise<User | MyError> => {
    return Promise.resolve({
        message: ErrorMessages.DBError,
        resolution: "check db connection"
    });
}

// main.ts
const main = async () => {
    const user = await getUser();
    if(isError(user)) {
        if(user.message === ErrorMessages.DBError) {
            console.log("return db error:");
        } else {
            console.log("return general error:");
        }
    } else {
        console.log("get user:");
    }
}

main();
```

## 위와 같이 체킹할 경우 에러 핸들링의 주체의 제어 역전이 가능하다
