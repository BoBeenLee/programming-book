# Type Narrowing in TypeScript

- https://www.youtube.com/watch?v=WAlJfSFngxw&list=LL&index=2

## case 1)

```
// "typeof"
function toNumber(val: number | string); number {
	if(ttypeof val === "string") {
		return parseInt(val, 10);
	}
	return val;
}
```

## case 2)

Correction

- 'in' is part of javascript, not just typescript. but it does type narrowing

```
// in

type StandardUser = {
	name: string;
	sessionTTL: number;
}

type AdminUser = StandardUser & {
	isAdmin: true;
	access: "read-admin" | "write-admin";
}


function login(user: StandardUser | AdminUser) {
	if("isAdmin" in user) {
		user // AdminUser
		return;
	}
	user // StandardUser
}

```

## case 3)

```
// Type predicates
type User = StandardUser | AdminUser;

const users: User[] = [
	{ name: "test", sessionTTL: 3 }
	{ name: "test", sessionTTL: 1, isAdmin: true }
];

const standardUsers = users.filter((user): user is StandardUser => !('isAdmin' in user));

```

## case 4)

```
// Discriminated unions
type StandardUser2 = {
	type: "standard";
	name: string;
	sessionTTL: number;
}

type AdminUser2 = {
	type: "admin";
	name: string;
	access: "read-admin" | "write-admin";
}

type ProspectUser = {
	type: "prospect";
}
// ProspectUser라는 타입이 추가되었을 경우 // never에서 타입 할당이 올바르지 않기에 타입 체킹이 가능하다.

type User2 = StandardUser2 | AdminUser2;

function login2(user: User2) {
	switch(user.type) {
		case "standard":
			// StandardUser2
			return;
		case "admin":
			// AdminUser2
			return;
		default:
			const notPossible: never = user; // never
			return;
	}
}
```
