
Директивы `ngSwitch`, `ngSwitchCase` и `ngSwitchDefault` в Angular используются для условного отображения одного из нескольких возможных элементов на основе значения выражения. Они аналогичны конструкции `switch` в языках программирования и позволяют управлять отображением элементов в шаблоне на основе значений.

### Основные директивы

- **`ngSwitch`**: Директива контейнера, которая проверяет значение выражения и решает, какой из дочерних элементов отображать.
- **`ngSwitchCase`**: Директива, которая определяет шаблон, который будет отображен, если значение выражения `ngSwitch` совпадает с ее значением.
- **`ngSwitchDefault`**: Директива, которая определяет шаблон, который будет отображен, если ни одно из значений `ngSwitchCase` не совпадает с значением выражения `ngSwitch`.

### Пример использования

#### Шаблон

```TS
<div [ngSwitch]="selectedOption">
  <div *ngSwitchCase="'option1'">Content for Option 1</div>
  <div *ngSwitchCase="'option2'">Content for Option 2</div>
  <div *ngSwitchCase="'option3'">Content for Option 3</div>
  <div *ngSwitchDefault>Default Content</div>
</div>
```

#### Компонент


```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <select [(ngModel)]="selectedOption">
      <option value="option1">Option 1</option>
      <option value="option2">Option 2</option>
      <option value="option3">Option 3</option>
    </select>

    <div [ngSwitch]="selectedOption">
      <div *ngSwitchCase="'option1'">Content for Option 1</div>
      <div *ngSwitchCase="'option2'">Content for Option 2</div>
      <div *ngSwitchCase="'option3'">Content for Option 3</div>
      <div *ngSwitchDefault>Default Content</div>
    </div>
  `
})
export class AppComponent {
  selectedOption = 'option1';
}
```

### Подробное объяснение

#### `ngSwitch`

- **Синтаксис**: `[ngSwitch]="expression"`, где `expression` — выражение, значение которого будет проверяться.
- **Описание**: Значение `expression` сравнивается с каждым `ngSwitchCase`. Если есть совпадение, соответствующий элемент отображается.

#### `ngSwitchCase`

- **Синтаксис**: `*ngSwitchCase="value"`, где `value` — значение, которое сравнивается с выражением `ngSwitch`.
- **Описание**: Если значение `value` совпадает с выражением `ngSwitch`, этот элемент отображается.

#### `ngSwitchDefault`

- **Синтаксис**: `*ngSwitchDefault`
- **Описание**: Этот элемент отображается, если ни одно из значений `ngSwitchCase` не совпадает с выражением `ngSwitch`.

### Пример с объяснением

Представьте, что у вас есть несколько вкладок, и вы хотите отображать различное содержимое в зависимости от выбранной вкладки.

#### Шаблон

```TS
<div>
  <button (click)="selectTab('home')">Home</button>
  <button (click)="selectTab('about')">About</button>
  <button (click)="selectTab('contact')">Contact</button>
</div>

<div [ngSwitch]="currentTab">
  <div *ngSwitchCase="'home'">Welcome to the Home page!</div>
  <div *ngSwitchCase="'about'">Learn more About us.</div>
  <div *ngSwitchCase="'contact'">Get in Touch with us.</div>
  <div *ngSwitchDefault>Select a tab to see content.</div>
</div>
```

#### Компонент

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  currentTab: string;

  selectTab(tab: string) {
    this.currentTab = tab;
  }
}
```

### Итоги

- `ngSwitch` используется для проверки значения выражения и выбора одного из нескольких возможных элементов для отображения.
- `ngSwitchCase` определяет, какой элемент отображать, если значение `ngSwitch` совпадает с его значением.
- `ngSwitchDefault` определяет элемент, который отображается, если ни одно из значений `ngSwitchCase` не совпадает с значением `ngSwitch`.