### Frontend Interview Questions
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
  <summary>Auth Guard in Angular</summary>

  **Auth Guard**
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
