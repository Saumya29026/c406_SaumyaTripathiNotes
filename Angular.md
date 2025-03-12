# Angular
Angular is a TypeScript-based open-source front-end web application framework developed by Google. It is used to build single-page applications (SPAs) and dynamic web apps. Angular provides a structured way to develop scalable and maintainable web applications.

## Uses
- Structured Framework: Angular provides a clear structure for building applications, making it easier to maintain and scale.
- Two-Way Data Binding: Simplifies the synchronization between the model and the view.
- Modularity: Applications are divided into modules, making them more organized.
- Dependency Injection: Makes the application more modular and testable.
- TypeScript: Enhances code quality and readability with strong typing.
- Rich Ecosystem: Includes tools like Angular CLI, RxJS, and Angular Material.

### Key Parts of an Angular Component
- An Angular component consists of three main parts:
- Template (HTML): Defines the view.
- Styles (CSS/SCSS): Defines the appearance.
- Logic (TypeScript): Defines the behavior.

### 1. app.component.ts (TypeScript)
- Contains the logic for the component.
- Defines the component's behavior and data.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'my-angular-app';
}
```

- @Component: Decorator that marks the class as a component.
- selector: The custom HTML tag used to include the component in templates.
- templateUrl: Path to the HTML template.
- styleUrls: Path to the CSS styles.

### 2. app.component.html (Template)
- Defines the view of the component.
- Contains HTML and Angular template syntax.

```html
<h1>{{ title }}</h1>
<p>Welcome to my Angular app!</p>
```
{{ title }}: Interpolation to display the title property from the component.

### 3. app.component.css (Styles)
- Defines the styles for the component.
- Scoped to the component (not global).

Example:

```css
h1 {
  color: blue;
}
```
