## 📋 Template Reference Variables in Angular

**Template reference variables** in Angular are used to reference a DOM element, a component, or a directive within the template. They provide a way to access these elements directly from the template and interact with them without having to go through the component class.

These reference variables are declared in the template and are prefixed with a `#` symbol.

---

### 🔧 Syntax

```html
<element #variableName></element>
```

* `#variableName` is the template reference variable.
* It gives a reference to the **DOM element**, **directive**, or **component**.

For example:

```html
<input #myInput />
```

Here, `#myInput` is the reference variable pointing to the `<input>` element.

---

### 🔍 Accessing the Template Reference Variable

You can access this variable in different ways:

#### 1. Accessing DOM Elements

You can use the reference variable to access the DOM element itself in the template.

```html
<input #myInput type="text">
<button (click)="logInput(myInput)">Log Input</button>
```

**Component:**

```ts
export class AppComponent {
  logInput(input: HTMLInputElement) {
    console.log(input.value);  // Logs the value of the input
  }
}
```

#### 2. Accessing Component or Directive

You can also use template reference variables to access **child components** or **directives**.

```html
<app-child-component #childComp></app-child-component>
<button (click)="childComp.doSomething()">Call Child Method</button>
```

**Component:**

```ts
@Component({
  selector: 'app-child-component',
  template: '<p>Child Component</p>',
})
export class ChildComponent {
  doSomething() {
    console.log('Child method called');
  }
}
```

---

### 📘 Example: Accessing Form Elements

```html
<form #myForm="ngForm">
  <input name="username" ngModel #username="ngModel">
  <div *ngIf="username.invalid && username.touched">Username is required!</div>
</form>

<button (click)="submitForm(myForm)">Submit</button>
```

**Component:**

```ts
export class AppComponent {
  submitForm(form: NgForm) {
    if (form.valid) {
      console.log(form.value);
    } else {
      console.log('Form is invalid');
    }
  }
}
```

* `#myForm="ngForm"` creates a reference to the form and binds it to the `NgForm` directive.
* `#username="ngModel"` creates a reference to the input and binds it to the `NgModel` directive.

---

### ✅ Benefits of Template Reference Variables

1. **Simplifies Template Interactions:** You can interact with DOM elements, components, or directives directly in the template without needing to reference them in the component class.
2. **Access to Native DOM Methods and Properties:** Template reference variables give direct access to DOM methods like `focus()`, `select()`, etc.
3. **Component Communication:** They allow communication between parent and child components by referencing the child component instance in the template.

---

### 📝 Best Practices

* **Use descriptive variable names** to clearly indicate what the reference is pointing to (e.g., `#formRef`, `#inputRef`).
* **Avoid complex logic in templates**. Use template reference variables for simple interactions, like accessing form controls or invoking component methods.
* **Combine with Angular directives** like `ngIf`, `ngFor` to reference specific DOM elements or components conditionally.

---

### 🧪 Example: Focus Control with Template Reference Variables

Here’s how you can use template reference variables to focus an input element when a button is clicked:

```html
<input #myInput type="text" placeholder="Focus me!">
<button (click)="myInput.focus()">Focus Input</button>
```

**Component:**

```ts
export class AppComponent {
  // You don't need to write any logic here as the focus method is on the input itself
}
```

---

### 🔄 Summary Table

| Feature        | Description                                                         |
| -------------- | ------------------------------------------------------------------- |
| Syntax         | `#variableName`                                                     |
| Purpose        | Reference to DOM elements, components, or directives                |
| Access Method  | Directly within the template or in component methods                |
| Use Case       | Accessing DOM properties, calling methods of child components, etc. |
| Common Example | Accessing form elements, child components, or directives            |

--

Template reference variables in Angular offer an easy way to interact with DOM elements, components, or directives directly within the template. They are highly useful for scenarios like managing form elements, triggering component methods, and working with native DOM properties and methods.
