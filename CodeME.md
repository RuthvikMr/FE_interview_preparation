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

  **Question 1**: (Infosys)
  ```js
const [x,y=5] = [10]
console.log(x+y);
  ```
  **Output**:
   ```js
15
  ```

  **Explanation**:
  - It is a  `[x,y=5]` is destructuring syntax so in destructuring the values are assigned in the same order as they appear in the array.
  - So `x = 10` and initially `y = undefined` as there is no value but here `y`=5` so `undefined` will become `5`. `x + y` i.e `10 + 5` = `15`

     **Question 2**: (TCS)
  ```js
console.log(!!{});
console.log(!![]);
  ```
  **Output**:
   ```js
True
True
  ```

  **Explanation**:
  - In JavaScript, some values are falsy (e.g., 0, "", null, undefined, NaN, and false), and all other values are truthy.
  - Empty objects `({})` and empty arrays `([])` are truthy values.
  - So output here will be 1st negation will `!{}` will be give `false` and 2nd negation `!!{}` will give `true` similarly  for `!![]`

     **Question 3**:
  ```js
let h = "100px";
let w = "20px"
console.log(parseInt(h + w));
  ```
  **Output**:
   ```js
100
  ```

  **Explanation**:
  - `h + w` results in "100px20px", parseInt only takes the 1st valid numbers from the string, anything else is ignored.so after 100 p isn't a number so ignored.

     **Question 4**: (Infosys)
  ```js
let x = 1 || 2 && 3;
console.log(x);
  ```
  **Output**:
   ```js
1
  ```

  **Explanation**:
  - In javascript `AND` operator has more precedence over  `OR`operator. So our expression becomes `2 && 3` `3` will be returned now it checks `1 || 3` OR operator will check truthy value `1 || 3` 1 is truthy so returns final output as `1` 
  
</details>

<details>
<summary>Practice Programs</summary>


**Find Next Largest**
- Expected O/p : [4,4,7,9,9,-1] If no greater number put -1 (Here 2 loops are used O(n2) try using 1 loop only O(n))
```js
function findNextLargest(arr){
  let res = [];
  for(let i = 0; i < arr.length; i++){
    let nextG = -1;
    for(let j = i + 1; j < arr.length; j++){
      if(arr[i] < arr[j]){
        nextG = arr[j];
        break;
      }
    }
    res.push(nextG);
  }
  console.log(res);
}

findNextLargest([3,1,4,7,2,9]);
```
**Find the missing natural number**
- Input: n = 5;total length of array including missing number, array = [1,2,4,5]; Expected Output 3 [checkout: Check how can we achive for multime missing number]
```
// find missing number
let arr = [1,2,4,5];
let n = 5;

function findMissingNumber(arr){
  let sum = 0;
  let diff = 0;
  for(let i=0;i < arr.length;i++){
    sum += arr[i];
  }
  diff = (n * (n + 1)/2) - sum;
  return diff;
}

const missingNumber = findMissingNumber(arr);
console.log(missingNumber);
```
 
</details>
