## 1

```javascript
function test() {
  if(undefined == null) {
    console.log('Yes undefined is == null');
  }
  if(undefined === null) {
    console.log('yes undefined is === null');
  }
}
test();
```
## 2

```javascript
Object.freeze, Object.seal
```
## 3

```javascript
var foo = function(n) {
    if(n < 5) {
        return 
        	n * 2;
    }
    else 
        return n;
};
foo(6)
foo(3);
```
## 4 hoisting

```javascript
function foo() {
	console.log('foo called...');
}

foo();

function foo() {
	console.log('foo redefined');
}

foo();
```

## 5 hasOwnProperty

```javascript
var Car = function(year) {
	this.year = year;
};

Car.proptotype.miles = 0;

Car.prototype.drive = function(dist) {
	this.miles += dist;
}

var car1 = new Car(2015);
var car2 = new Car(2017);

for(var prop in car1) {
	console.log(prop + ' ' + car1.hasOwnProperty(prop));
}

car1.drive(10);

for(var prop in car1) {
	console.log(prop + ' ' + car1.hasOwnProperty(prop));
}

for(var prop in car2) {
	console.log(prop + ' ' + car2.hasOwnProperty(prop));
}
```
