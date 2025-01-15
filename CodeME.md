### Commonly Asked Coding Questions
### Output Based Questions

<details>
  <summary> Hoisting (var, let, const) </summary>
  
  #### Hoisting
  **Question 1** (Important):
  ```js
let arr = [1,2];
for(var i = 0; i<arr.length;i++){
setTimeout(()=>{
console.log(i);
},[1000])
}
```
**Output**:
```js
2
2
```
**Explanation**:
Since `var` is global-scoped, the value of `i` is shared across all iterations of the loop. By the time the `setTimeout` callbacks execute (after 1000ms), the loop will have completed, and `i` will have the value `2` (the length of the array).
`i = 0` for the 1st time
`i = 1` for the 2nd time 
Then `i = 2` checks the for loop length is `2 < 2` which is false but as i is `var` after settimeout `i` will be printed `2`

**Question 2** Temporal Dead Zone
```js
console.log(a);
var a = 10;

console.log(b);
let b = 20;

```
**Output**:
```js
undefined
ReferenceError: Cannot access 'b' before initialization
```
**Explanation**:
`var` declarations are hoisted (moved to the top of their scope) and initialized with undefined. So, `console.log(a)` works but prints undefined.
let declarations are also hoisted but are in the temporal dead zone until their initialization. Accessing b before the let b = 20 line throws a ReferenceError

**Question 3**: `var` in a loop
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
```
**Output**:
```js
3
3
3
```
**Explanation**:
Similar to Question 1

**Question 4**: `let` in a loop
```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}

```
**Output**:
```js
0
1
2
```
**Explanation**:
`let` is block-scoped, so each iteration of the loop creates a new instance of `i` that is preserved for the `setTimeout` callback.

**Question 5** : `const` in a loop
```js
for (const i = 0; i < 3; i++) {
  console.log(i);
}
```
**Output**:
```js
TypeError: Assignment to constant variable.
```
**Explanation**:
`const` variables cannot be reassigned. The loop tries to increment `i`, causing a `TypeError`.

**Question 6** : Re-declaration
```js
var a = 10;
var a = 20;

let b = 30;
let b = 40;

const c = 50;
const c = 60;

```
**Output**:
```js
No Error for var
SyntaxError: Identifier 'b' has already been declared
SyntaxError: Identifier 'c' has already been declared

```
**Explanation**:
`let` and `const` do not allow re-declaration in the same scope and throw a SyntaxError.

**Question 7** : Block Scope
```js
{
  let a = 10;
  var b = 20;
}
console.log(a);
console.log(b);

```
**Output**:
```js
ReferenceError: a is not defined
20
```
**Explanation**:
`let` is blocked scope so a is not reachable. whereas `var` is global scope so prints `20`

**Question 8** : Shadowing
```js
let x = 10;
{
  var x = 20;
}

```
**Output**:
```js
SyntaxError: Identifier 'x' has already been declared
```
**Explanation**:
A `SyntaxError` is thrown because `x` is already declared with let.
`var` and `let` declarations cannot co-exist in the same scope.

**Question 9** : Scoping with Functions
```js
function test() {
  if (true) {
    var a = 10;
    let b = 20;
  }
  console.log(a);
  console.log(b);
}
test();

```
**Output**:
```js
10
ReferenceError: b is not defined
```
**Explanation**:
let is block-scoped, so b is not accessible outside the if block.

**Question 10** : Global `var` vs Global `let`
```js
var a = 10;
let b = 20;

window.a = 30; // works in browsers
window.b = 40;

console.log(a, b);
console.log(window.a, window.b);

```
**Output**:
```js
10 20
30 undefined
```
**Explanation**:
`let` does not create a property on the `window` object.

**Question 11** : `var` Hoisting in Functions (Important)
```js
function test() {
  console.log(a);
  var a = 10;
  function a() {}
}
test();

```
**Output**:
```js
[Function: a]
```
**Explanation**:
Function declarations take precedence over var declarations during hoisting, so a is initially a function

**Question 12** : Default Values and Hoisting (Important)
```js
console.log(foo());
function foo() {
  return "Hello";
}
var foo = function () {
  return "Hi";
};

```
**Output**:
```js
"Hello"
```
**Explanation**:
- Function declarations are hoisted with the function definition.
- The `foo` function declaration is hoisted, and the `var foo` assignment comes later, so the original `foo` function executes.

**Question 13** : Multiple Declarations and Hoisting
```js
var a = 1;

function test() {
  console.log(a);
  var a = 2;
  console.log(a);
}
test();
console.log(a);

```
**Output**:
```js
undefined
2
1

```
**Explanation**:
Inside test, the `var` a declaration is hoisted, shadowing the global `a`. It is initialized to `undefined` initially, so `console.log(a)` inside the function prints `undefined` at first and `2` after assignment.

**Question 14**
```js
function tricky() {
  console.log(a);
  var a = 10;
  let b = 20;
  console.log(b);
}
tricky();

```
**Output**:
```js
undefined
ReferenceError: Cannot access 'b' before initialization
```
**Explanation**:
The `let b` is in the **temporal dead zone** until it is initialized, so accessing it before initialization throws a `ReferenceError`.

**Question 15**: Nested Function Hoisting
```js
function outer() {
  console.log(typeof inner);
  function inner() {}
  console.log(typeof inner);
}
outer();

```
**Output**:
```js
function
function
```
**Explanation**:
The `function inner` is hoisted inside `outer`. Before its definition, typeof inner is "function", not "undefined", because function declarations are hoisted with their definitions.

</details>

<details>
  <summary>Commonly Asked Questions</summary>
  
  ### Commonly Asked Questions during interview

  **Question 1**:
  ```js

  ```
  **Output**:
   ```js

  ```

  **Explanation**:
  
</details>
