### Frontend Interview Questions
### Angular Questions

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
  <summary>Observable VS Promise</summary>

  **Observable**
   - Observable handles multiple asynchronous events over time and executes only when subscribed.
  
  **Promise**
   - Promise handles single asynchronous event executes immediately upon creation
</details>
