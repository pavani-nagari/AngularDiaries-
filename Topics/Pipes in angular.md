# 🌪 Pipes in Angular – In-Depth Guide

Angular **pipes** are a powerful feature used to **transform data directly in the template**. They are extremely useful for formatting values such as strings, currency amounts, dates, and more.

---

## 🔹 What is a Pipe?

A **pipe** takes in data as input and transforms it to a desired output. Think of it as a filter.

### Basic Syntax

```html
{{ value | pipeName }}
```

You can also pass **parameters** to a pipe:

```html
{{ value | pipeName:arg1:arg2 }}
```

---

## 🔹 Built-in Pipes in Angular

Angular includes a variety of **built-in pipes**. Here's a list of some commonly used ones:

| Pipe         | Description                              | Example |
|--------------|------------------------------------------|---------|
| `date`       | Formats a date value                     | `{{ today | date:'short' }}` |
| `uppercase`  | Transforms text to uppercase             | `{{ 'hello' | uppercase }}` → `HELLO` |
| `lowercase`  | Transforms text to lowercase             | `{{ 'HELLO' | lowercase }}` → `hello` |
| `titlecase`  | Capitalizes first letter of each word    | `{{ 'angular rocks' | titlecase }}` → `Angular Rocks` |
| `currency`   | Transforms number to currency format      | `{{ 2500 | currency:'USD' }}` → `$2,500.00` |
| `percent`    | Transforms number to percentage           | `{{ 0.75 | percent }}` → `75%` |
| `json`       | Converts object to JSON string            | `{{ user | json }}` |
| `slice`      | Returns a slice of a string/array         | `{{ 'Angular' | slice:0:3 }}` → `Ang` |
| `async`      | Handles Observable/Promise values         | `{{ observableData | async }}` |

---

## 🔹 Using Built-in Pipes – Example

### `app.component.ts`

```ts
export class AppComponent {
  today: number = Date.now();
  salary: number = 5200.5;
  text: string = 'angular tutorial';
  percentValue: number = 0.876;
}
```

### `app.component.html`

```html
<p>Current Date: {{ today | date:'fullDate' }}</p>
<p>Uppercase Text: {{ text | uppercase }}</p>
<p>Formatted Salary: {{ salary | currency:'USD' }}</p>
<p>Percentage: {{ percentValue | percent }}</p>
```

---

## 🔹 Chaining Pipes

You can **chain multiple pipes** together:

```html
<p>{{ 'hello angular' | titlecase | slice:0:5 }}</p> <!-- Output: Hello -->
```

---

## 🔹 Using Parameters with Pipes

You can **pass arguments** to pipes for more control:

```html
<!-- Date with full format -->
{{ today | date:'fullDate' }}

<!-- Currency with custom code and symbol -->
{{ 2500 | currency:'EUR':'symbol' }}

<!-- Slice from index 1 to 4 -->
{{ 'Angular' | slice:1:4 }} <!-- Output: ngu -->
```

---

## 🔹 Creating a Custom Pipe

You can define your own custom pipe by implementing the `PipeTransform` interface.

### Step 1: Create the Pipe

```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'capitalize'
})
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    if (!value) return '';
    return value.charAt(0).toUpperCase() + value.slice(1).toLowerCase();
  }
}
```

### Step 2: Register It

Add it to your module’s `declarations`:

```ts
@NgModule({
  declarations: [
    AppComponent,
    CapitalizePipe
  ]
})
export class AppModule { }
```

### Step 3: Use in Template

```html
<p>{{ 'angular' | capitalize }}</p> <!-- Output: Angular -->
```

---

## 🔹 Use Case – Pipe with Observables (`async` Pipe)

```ts
data$: Observable<string> = of('async pipe demo');
```

```html
<p>{{ data$ | async }}</p> <!-- Output: async pipe demo -->
```

---

## ✅ Summary

| Feature | Explanation |
|--------|-------------|
| **Built-in Pipes** | Quick formatting for common needs |
| **Chaining** | Apply multiple transformations |
| **Parameters** | Customize output (e.g., currency, slice range) |
| **Custom Pipes** | Implement your own transformation logic |
| **Async Pipe** | Handles Observables and Promises in templates |
