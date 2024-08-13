
# ElementRef - предоставляет доступ к конкретному элементу DOM. Он используется для доступа к свойствам и методам элемента, таких как `nativeElement`, `attributes`, `classList` и другие. `ElementRef` позволяет извлекать данные из элемента, изменять его свойства и выполнять другие операции.

```TS
import { Component, ElementRef } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: `
    <input #myInput>
    <button (click)="getInputValue()">Get Input Value</button>
  `
})
export class MyComponent {
  @ViewChild('myInput') inputElement: ElementRef;

  getInputValue() {
    console.log(this.inputElement.nativeElement.value);
  }
}
```

# Renderer2 - предоставляет методы для изменения внешнего вида и содержимого элементов DOM. Он используется для выполнения операций, таких как изменение стилей, добавление или удаление классов, изменение содержимого элемента и другие. `Renderer2` позволяет обновлять DOM без прямого доступа к элементам.

```TS
import { Component, Renderer2, ElementRef } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: `
    <input #myInput>
    <button (click)="changeInputColor()">Change Input Color</button>
  `
})
export class MyComponent {
  constructor(private renderer: Renderer2, private elementRef: ElementRef) {}

  changeInputColor() {
    this.renderer.setStyle(this.elementRef.nativeElement.querySelector('input'), 'color', 'red');
  }
}
```

### Основное различие между `ElementRef` и `Renderer2` заключается в том, что `ElementRef` предоставляет прямой доступ к элементу DOM, а `Renderer2` предоставляет методы для изменения внешнего вида и содержимого элементов DOM. 