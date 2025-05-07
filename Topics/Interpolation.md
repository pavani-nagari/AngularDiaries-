# Angular Data Binding Notes

This README covers the basics of **Interpolation** and **Event Binding** in Angular, with examples and best practices.

---

## 🔁 Interpolation in Angular

**Interpolation** in Angular is a technique used to bind data from the component class to the HTML template using double curly braces `{{ }}`.

### 🔧 Syntax
```html
<p>{{ title }}</p>
```

- `title` is a variable defined in the component class.
- Angular replaces `{{ title }}` with the actual value of `title`.

### 📘 Example

**Component:**
```ts
export class AppComponent {
  title = 'Welcome to Angular!';
}
```

**Template:**
```html
<h1>{{ title }}</h1>
```

**Rendered Output:**
```html
<h1>Welcome to Angular!</h1>
```

### 🧠 Additional Usage

- **Expressions:**
  ```html
  <p>{{ 5 + 5 }}</p> <!-- Outputs: 10 -->
  ```

- **Function Calls:**
  ```html
  <p>{{ getMessage() }}</p>
  ```

> ⚠️ Avoid calling heavy functions inside interpolation as they run on every change detection cycle.

### ❌ Not Allowed in Interpolation

- Control flow statements like `if`, `for`, `while`
- Assignments (e.g., `{{ count = 5 }}`)

### ✅ Best For

- Displaying text content
- Showing computed values
- Concatenating strings

---

## 🔗 Event Binding in Angular

**Event binding** in Angular allows you to listen to DOM events and trigger methods in your component.

###  Syntax
```html
<button (click)="handleClick()">Click me</button>
```

- `(click)` is the event name in parentheses.
- `handleClick()` is the method in the component that gets called when the event occurs.

### 📘 Example

**Template:**
```html
<input (input)="onInputChange($event)" placeholder="Type something" />
<p>You typed: {{ message }}</p>
```

**Component:**
```ts
export class AppComponent {
  message = '';

  onInputChange(event: Event) {
    const input = event.target as HTMLInputElement;
    this.message = input.value;
  }
}
```

### 🎯 Common DOM Events

| Event         | Description                    |
|---------------|--------------------------------|
| `(click)`     | Mouse click event              |
| `(keyup)`     | Key released on keyboard       |
| `(mouseenter)`| Mouse enters an element        |
| `(mouseleave)`| Mouse leaves an element        |
| `(submit)`    | Form submission                |
| `(change)`    | Input value change (on blur)   |
| `(input)`     | Real-time input value changes  |

### ✅ Best For

- Listening to user interactions
- Triggering methods based on DOM events
- Updating component state dynamically

---

