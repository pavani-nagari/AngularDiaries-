# Using `@Input()` and `@Output()` in Angular

Angular provides `@Input()` and `@Output()` decorators to enable communication between components, especially between parent and child components.

---

## `@Input()` – Passing Data from Parent to Child

The `@Input()` decorator allows a parent component to bind data to a property of the child component.

### Example

### `parent.component.html`
```html
<app-child [message]="'Hello from parent!'"></app-child>
```

---

## `@Output()` – Sending Data from Child to Parent

The `@Output()` decorator allows the child component to emit an event that the parent component can listen to and respond to.

### Example

### `child.component.ts`
```ts
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<button (click)="sendMessage()">Send to Parent</button>`
})
export class ChildComponent {
  @Output() messageEvent = new EventEmitter<string>();

  sendMessage() {
    this.messageEvent.emit('Hello from child!');
  }
}
```

### `parent.component.html`
```html
<app-child (messageEvent)="receiveMessage($event)"></app-child>
<p>{{ receivedMessage }}</p>
```

### `parent.component.ts`
```ts
export class ParentComponent {
  receivedMessage: string = '';

  receiveMessage(message: string) {
    this.receivedMessage = message;
  }
}
```

---

## Summary

| Decorator   | Purpose                    | Used In |
|-------------|----------------------------|---------|
| `@Input()`  | Receive data from parent   | Child   |
| `@Output()` | Send data/event to parent  | Child   |

These decorators are essential for proper component interaction in Angular applications.
