## 1

`
function test() {
  if(undefined == null) {
    console.log('Yes undefined is == null');
  }
  if(undefined === null) {
    console.log('yes undefined is === null');
  }
}
test();
`
## 2

`
Object.freeze, Object.seal
`
## 3

`
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
`
## 4
