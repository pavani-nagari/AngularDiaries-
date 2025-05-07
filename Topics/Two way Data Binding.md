## 🔄 Two-Way Data Binding in Angular

### 🧠 What is Two-Way Data Binding?

**Two-way data binding** in Angular allows for **synchronization between the component's class (TypeScript)** and the **view (HTML template)**.

- If the user updates the UI, the component’s state changes.
- If the component state changes, the UI reflects the update.

It's a **bi-directional binding** between the class and the view.

---

### 🔧 Syntax: `[(ngModel)]`

Angular provides a special syntax for two-way data binding using `[(ngModel)]`.

```html
<input [(ngModel)]="username" />
```

- `[(ngModel)]` is **shorthand for** combining:
  - `[value]="username"` → property binding
  - `(input)="username = $event.target.value"` → event binding

> ℹ️ To use `[(ngModel)]`, you must import the **FormsModule**.

---

### ✅ Setup: Enabling FormsModule

Before using `ngModel`, you must import the **FormsModule** in your `AppModule`.

```ts
// app.module.ts
import { FormsModule } from '@angular/forms';

@NgModule({
  declarations: [ AppComponent ],
  imports: [ BrowserModule, FormsModule ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

---

### 📘 Example

```ts
// app.component.ts
export class AppComponent {
  username: string = '';
}
```

```html
<!-- app.component.html -->
<input [(ngModel)]="username" placeholder="Enter username" />
<p>Welcome, {{ username }}!</p>
```

🟢 Now:
- When the user types into the input box, `username` updates.
- When `username` changes in the class, the input box updates automatically.

---

### 🔁 How Two-Way Binding Works (Conceptual Diagram)

```
     +--------------------+        View Updates Component
     |     <input>        | <----------------------+
     |  [(ngModel)]       |                       |
     +--------------------+                       |
             |                                     |
             v                                     |
     +--------------------+                       |
     |   Component Class   |  Component Updates View
     |   username = "..."  | --------------------->|
     +--------------------+
```

---

### 🎯 When to Use

Use two-way binding when:
- You need **instant feedback** from user input (e.g., form fields).
- The **view and model need to stay in sync** (e.g., live search, settings forms, etc.).

---

### ⚠️ Best Practices

✅ Use for form fields or interactive UI elements  
❌ Avoid overusing it in large forms without reactive form logic  
🔁 For complex forms, consider using **Reactive Forms** instead  

---

### 🔍 Alternatives to `[(ngModel)]`

You can also manually implement two-way binding with:

```html
<input [value]="username" (input)="username = $event.target.value" />
```

But `[(ngModel)]` makes this easier and cleaner.

---

### 🧪 Two-Way Binding with Other Types

```ts
// TypeScript
quantity: number = 1;
isChecked: boolean = false;
```

```html
<input type="number" [(ngModel)]="quantity" />
<input type="checkbox" [(ngModel)]="isChecked" />
```

---

### ✅ Summary

| Feature       | Description                                       |
|---------------|---------------------------------------------------|
| Directive     | `ngModel`                                         |
| Module Needed | `FormsModule`                                     |
| Use Case      | Bi-directional syncing between class and template |
| Syntax        | `[(ngModel)]="property"`                          |

---

> 📚 **Two-way binding** is a powerful feature in Angular, but it should be used thoughtfully to avoid performance or debugging issues in larger applications.
