### Commonly Asked Coding Questions
### Output Based Questions

<details>
  <summary> Hoisting (var, let, const) </summary>
  
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

**Question 2**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 3**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 4**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 5**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 6**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 7**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 8**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 9**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 10**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 11**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 12**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 13**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 14**
```js

```
**Output**:
```js

```
**Explanation**:

**Question 15**
```js

```
**Output**:
```js

```
**Explanation**:

</details>
