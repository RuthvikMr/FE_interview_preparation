### Frontend Interview Questions ([GPT](https://chatgpt.com/g/g-p-693973d8e0a48191afa1cfc40598f23f-js-angular-questions/project))
### Basic Angular/React/Javascript Questions

<details>
  <summary>Component VS Decorators VS Directives</summary>

  **Component**:
  - It is a building block for an angular application that represents the web page.
  - Used to create a view (HTML + logic).
  - Always has a `.ts` file, an HTML file, and an optional CSS/SCSS file.
  - Example:
    ```typescript
    @Component({
      selector: 'app-page',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {
      title = 'my-interview-preparation-app';
    }
    ```

  **Decorator**:
  - A special function that modifies the behavior of a class, property, or method.
  - Used to add metadata to classes (like components, directives, etc.).
  - Decorator Uses are:
    - @Directive, @Component, @Pipe, @NgModule, @ViewChild, @Input etc.
  - Example:
    ```typescript
    import { ViewChild, TemplateRef, EventEmitter } from "@angular/core";  
    @Component({
      selector: 'app-page',
      templateUrl: './app.component.html',
    })
    @ViewChild('buttonClick') buttonClick :TemplateRef<any>
    @Output() emitData = new EventEmitter();
   
    export class AppComponent {}
    ```

  **Directive**:
  - Used to manipulate the DOM directly.
  - Can be structural (e.g., `*ngIf`, `*ngFor`) or attribute directives (e.g., `ngClass`, `ngStyle`).
  - Example of a custom directive:
    ```typescript
    import { Directive, ElementRef, Renderer2 } from '@angular/core';

    @Directive({
      selector: '[appHighlight]'
    })
    export class HighlightDirective {
      constructor(el: ElementRef, renderer: Renderer2) {
        renderer.setStyle(el.nativeElement, 'backgroundColor', 'yellow');
      }
    }
    ```
</details>

<details>
  <summary>Observable VS Promise VS Subject (Rxjs)</summary>
  
  **Rxjs**
  - It is a library for reactive programming that simplifies asynchronous operations.

  **Observable**
   - Observable handles multiple asynchronous events over time and executes only when subscribed,making it more versatile.
     ```typescript
     import { Observable } from 'rxjs';
     const observable = new Observable(subscriber => {
     setTimeout(()=> subscriber.next('Real time data'),1000);
      });
      observable.subscribe(data => console.log(data));
      ```
  
  **Promise**
   - Promise handles single asynchronous event executes immediately upon creation
     ```typescript
     const promise = new Promise((resolve,reject)=>{
        setTimeout(()=> resolve('Data Loaded')),1000;
     });
     promise.then((data)=> console.log(data));
     ```
  **Subjects**
  - A special type of observable that allows multicasting
  - **BehaviourSubject**: Keeps the latest value
    ```typescript
    import {BehaviourSubject} from 'rxjs';
    const behaviorSubject = new BehaviorSubject('Initial value');
    behaviorSubject.subscribe(value => console.log(`Subscriber 1: ${value}`));
    behaviorSubject.next('New value');
    behaviorSubject.subscribe(value => console.log(`Subscriber 2: ${value}`)); // Will print 'New value'
    ```
  - **ReplaySubject**: Keeps track of the previous values to late subscribers
      ```typescript
      import {ReplaySubject} from 'rxjs';
      // Previous/last 2 emitted values
      const replaySubject = new ReplaySubject<string>(2);

      // Subscriber 1 subscribes
      replaySubject.subscribe(value => console.log(`Subscriber 1 received: ${value}`));
      replaySubject.next('Message 1');
      replaySubject.next('Message 2');
      replaySubject.next('Message 3');

      // Subscriber 2 subscribes (receives the last 2 buffered values)
      replaySubject.subscribe(value => console.log(`Subscriber 2 received: ${value}`));
      replaySubject.next('Message 4');

      // Subscriber 3 subscribes (receives the last 2 buffered values)
      replaySubject.subscribe(value => console.log(`Subscriber 3 received: ${value}`));

      //Output
      Subscriber 1 received: Message 1
      Subscriber 1 received: Message 2
      Subscriber 1 received: Message 3
      Subscriber 2 received: Message 2
      Subscriber 2 received: Message 3
      Subscriber 1 received: Message 4
      Subscriber 2 received: Message 4
      Subscriber 3 received: Message 3
      Subscriber 3 received: Message 4
      ```
    - **Async Subject**
    - Emits only Last value
    - Emits only after ```complete()```
    - Think like 'An Order will be succssefull only after the item is delivered then we call it as completed similary async subject'
    - Example
      ```
      const async = new AsyncSubject();
      async.subscribe(v => console.log(v));
      async.next(1);
      async.next(2);  // O/P will be 2
      ```
      
  **When to Use**
  - **Observable**: When using real time data like live chat updates etc...
  - **Promise**: Fetch single API like user data
  - **Subjects**: When you need to manually emit events (e.g., button click handlers or event emitters).
</details>

<details>
  <summary>React VS Angular</summary>
  
  | React | Angular |
  | --- | --- |
  | A library focusing on building UIs. Requires additional libraries for state management and routing. | A complete framework with built-in tools like dependency injection, routing, and state management |
  
</details>

<details>
  <summary>Angular Architecture VS React Architecture</summary>
  
  | Feature | React | Angular |
  | --- | --- | --- |
  | **Type** | UI library | Full-fledged framework |
  | **Building Block** | Components,JSX,Props,State,Context,State Management,Routing `react-router-dom` | Modules,Component,Directives,Services and Dependency Injection,Routing, Change detection
  | **Language** | JavaScript (TypeScript optional) | TypeScript (built-in support)	|
  | **Routing** | Requires third-party libraries `react-router` | Built-in with `RouterModule` |
  | **State Management** | Requires libraries like Redux or Context | Built-in services and RxJS |
  | **Performance** | Virtual DOM for fast rendering | Optimized with Ahead-of-Time (AOT) Compilation |
  | **Dependency Injection** | Not built-in; use Context or libraries | Built-in |
  
</details>

<details>
  <summary>Auth Guard/Route Guard in Angular</summary>

  **Route Guard**
  - Route Guard is a feature in angular that control navigation from route based custom logic.
  - Type of route Guards

  | Guard Type | Purpose |
  | --- |--- |
  | `canActivate` | Prevent access to route |
  | `canActivateChild` | prevent access to child route |
  | `canDeactivate` | prevent leaving a route/component |
  | `canLoad` | Prevent lazy loading of modules |
  | `Resolve` | Pre-fetch data before route loads |
  

  **Auth Guard**
  - Auth Guard is a specific implementation of a Route Guard(usually `canActivate`) used to check if user is authenticated before allowing access to a route.
  - Auth Guards implement the `CanActivate` interface to control access to routes
    
    ```typescript
    import { Injectable } from '@angular/core';
    import { CanActivate, Router } from '@angular/router';

    @Injectable({ providedIn: 'root' })
    export class AuthGuard implements CanActivate {
    constructor(private router: Router) {}

    canActivate(): boolean {
    const isAuthenticated = !!localStorage.getItem('token');
    if (!isAuthenticated) {
      this.router.navigate(['/login']);
    }
    return isAuthenticated;
    }
    }
    ```

</details>

<details>
  <summary>Authentication vs Authorization</summary>

  **Difference**
  - **Authentication**: Verifies the user's identity (e.g., login).
  - **Authorization**: Determines what resources a user can access based on roles.

  **Example**
  - **Authentication**:Using JWT tokens for login.
  - **Authorization**:Restricting access to admin routes based on user roles.
</details>

<details>
  <summary>Change Detection in Angular</summary>

  **Answer**: 
  - Angular’s change detection tracks changes in the component's data model and updates the DOM. By default, it checks the entire component tree.
  - To optimize performance,`OnPush` strategy for immutable data, ensuring Angular only checks the components when input properties change or an event is triggered.
    **Default Change Detection Strategy**
 - Angular’s default change detection strategy is to check every component in the component tree from top to bottom whenever any event happens (e.g., click, HTTP response, timer, input change). This can lead to performance issues in large applications because even components whose data hasn't changed get checked.
   **ChangeDetectionStrategy.OnPush (What OnPush Does)**
   When `OnPush` is set. Angular will only run change detection for that component if:
   - An `@Input` reference changes
   - An event handler inside the component is triggered (like a button click).
   - Manually triggered using `ChangeDetectorRef.markForCheck()` or `detectChanges()`

     Use of OnPush - Improved performance, Scales better(Especially useful in data-heavy)

     ```typescript
     import { ChangeDetectionStrategy, Component } from '@angular/core';
     @Component({
      selector: 'app-user',
      template: `{{ user.name }}`,
      changeDetection: ChangeDetectionStrategy.OnPush
      })
      export class UserComponent {
      @Input() user!: { name: string };
      }
      ```
In this case:
If user.name changes but the reference doesn't (same object), the view will not update.
If you pass a new object like `{ name: 'New Name' }`, Angular detects the change.

</details>

<details>
  <summary>HTTP Interceptor</summary>
  
  **Answer**
  - HTTP interceptors intercept and modify HTTP requests and responses globally.
  - Used them to attach JWT tokens to API requests for authentication and log errors globally for debugging. For instance, in a secure app, every outgoing request included an Authorization header set by an interceptor.
    
</details>

<details>
  <summary>CI/CD Pipelines</summary>

  **Answer**
  - CI/CD pipelines automate testing, building, and deploying code.
  - This ensures a seamless and error-free deployment process.
    
</details>

<details>
  <summary>Event Loops (Imp)</summary>

  **Answer**
  - The event loop is a JavaScript mechanism that handles asynchronous operations by executing synchronous code first, then microtasks like Promises, and finally macrotasks like setTimeout, enabling non-blocking behavior in a single-threaded environment. (Check more details on this)
    
</details>

<details>
  <summary>View Encapsulation in Angular</summary>
  
  **Question**
  - Load a child component in another component but exclude the styles of the child component..! How can we achieve this?

   **Answer**
  - This can be achieved by **disabling the view encapsulation** in the childs component.
  - We can remove the styles effect of the component by setting `ViewEncapsulation` to `None` inside the component's decorator.
  - Types of encapsulation are:
  - **Emulated** : Styles are scoped to the component only
  - **None**: No style scope. Styles are global
  - **ShadowDom**: Uses real shadowdom for true encapsulation. Meaning When you need strong style encapsulation or we can say it as `ViewEncapsulation.ShadowDom` uses the browser's native Shadow DOM to achieve true encapsulation of a component's template and styles, meaning styles are completely isolated from the rest of the app.

  ```js
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-child',
  templateUrl: './child.component.html',
  styleUrls: ['./child.component.css'],
  encapsulation: ViewEncapsulation.None  // <<< This line is important
})
export class ChildComponent { }
```
  
</details>

<details>
  <summary>HTML Block Elements and Inline Elements</summary>
  
  **Block Elements**
  - Block elements take up full horizontall space in its container.
  - They start on new line and adds some space before and after the element.
  - Example:
```js
<address>  <article>    <aside>  <blockquote>  <canvas>  <dd>  <div>  <dl>  <dt>  <fieldset>
<figcaption>  <figure>  <footer>  <form>  <h1>-<h6>  <header>  <hr>  <li>  <main>  <nav>  <noscript>
<ol>  <p>  <pre>  <section>  <table>  <tfoot>  <ul>  <video>
```
**Inline Elements**
- Inline elements only takes up as much width necessary.
- Does not start on new line.

```js
<a>  <abbr>  <acronym>  <b>  <bdo>  <big>  <br>  <button>  <cite>  <code>  <dfn>  <em>
<i>  <img>  <input>  <kbd>  <label>  <map>  <object>  <output>  <q>  <samp>  <script>
<select>  <small>  <span>  <strong>  <sub>  <sup>  <textarea>  <time>  <tt>  <var>
```
    
</details>

<details>
  <summary>CSS Questions</summary>
  
  **Q1. Which CSS property is used to set the distance between lines of text.**
  - `line-height`

  **Q2. illustrate how to use this CSS :nth-Child() pseudo class select and style every third list item in an unordered list differently from the rest. Provide this CSS code example along with your explanation**
  - The `:nth-child()` pseudo-class in CSS allows you to select elements based on their position among siblings.
  ```js
  ul li:nth-child(3n) {
  background-color: lightblue;
  color: darkblue;
  font-weight: bold;
}
  ```
```js
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li> <!-- Styled differently -->
  <li>Item 4</li>
  <li>Item 5</li>
  <li>Item 6</li> <!-- Styled differently -->
  <li>Item 7</li>
  <li>Item 8</li>
  <li>Item 9</li> <!-- Styled differently -->
</ul>
```
**Explanation**
- `:nth-child(3n)` matches every 3rd element: 3, 6, 9, etc.
- `li:nth-child(3n)` applies the style only to `<li>` elements that are the 3rd, 6th, 9th, etc., child of their parent (`<ul>` in this case).

</details>

### Interview coding questions
<details>
  <summary>Count the occurrence of the characters</summary>

  **Problem**:
  
  ```js
const characters = 'aaddbccc';
const countOccurance = {};
for (let ch of characters) {
    countOccurance[ch] = (countOccurance[ch] || 0) + 1;
}
console.log(countOccurance);
```
  **Output**
  ```javascript
  {
  a:2,
  d:2,
  b:1,
  c:3
  }
```

</details>
