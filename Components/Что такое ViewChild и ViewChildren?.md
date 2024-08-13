
# ViewChild - используется для получения одного дочернего элемента или компонента. Он принимает два аргумента:

- Первый аргумент - это имя или селектор дочернего элемента или компонента, к которому нужно получить доступ.
- Второй аргумент - это опциональный тип, который определяет тип дочернего элемента или компонента, к которому нужно получить доступ.

`ViewChild` возвращает экземпляр дочернего элемента или компонента, который можно использовать для взаимодействия с ним или получения его данных.

```TS
import { Component, ViewChild } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: `
    <input #myInput>
    <button (click)="getInputValue()">Get Input Value</button>
  `
})
export class MyComponent {
  @ViewChild('myInput') inputElement: HTMLInputElement;

  getInputValue() {
    console.log(this.inputElement.value);
  }
}
```


# ViewChildren - используется для получения нескольких дочерних элементов или компонентов. Он принимает два аргумента:

- Первый аргумент - это имя или селектор дочерних элементов или компонентов, к которым нужно получить доступ.
- Второй аргумент - это опциональный тип, который определяет тип дочерних элементов или компонентов, к которым нужно получить доступ.

`ViewChildren` возвращает `QueryList`, который содержит список экземпляров дочерних элементов или компонентов. Этот список может быть использован для итерации по элементам или для доступа к конкретному элементу.

```TS
import { Component, ViewChildren, QueryList } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: `
    <input #myInput>
    <input #myInput2>
    <button (click)="getInputValues()">Get Input Values</button>
  `
})
export class MyComponent {
  @ViewChildren('myInput') inputElements: QueryList<HTMLInputElement>;

  getInputValues() {
    this.inputElements.forEach(inputElement => {
      console.log(inputElement.value);
    });
  }
}
```

