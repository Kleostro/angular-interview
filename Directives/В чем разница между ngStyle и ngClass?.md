
`ngStyle` и `ngClass` — это директивы Angular, которые используются для динамического управления стилями элементов и классами CSS соответственно.

### `ngStyle`

`ngStyle` позволяет динамически устанавливать стили на элемент на основе объекта стилей.

#### Пример

```TS
<div [ngStyle]="{ 'background-color': bgColor, 'font-size': fontSize + 'px' }">
  This is a styled div.
</div>
```

#### Компонент

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div [ngStyle]="{ 'background-color': bgColor, 'font-size': fontSize + 'px' }">
      This is a styled div.
    </div>
  `
})
export class AppComponent {
  bgColor = 'lightblue';
  fontSize = 16;
}
```

### `ngClass`

`ngClass` позволяет динамически устанавливать классы CSS на элемент на основе строки, массива строк или объекта.

#### Пример

```TS
<div [ngClass]="{ 'active': isActive, 'disabled': isDisabled }">
  This is a conditionally styled div.
</div>
```

#### Компонент

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div [ngClass]="{ 'active': isActive, 'disabled': isDisabled }">
      This is a conditionally styled div.
    </div>
  `
})
export class AppComponent {
  isActive = true;
  isDisabled = false;
}
```

### Ключевые различия

1. **Использование**:
    
    - `ngStyle` используется для применения стилей CSS непосредственно к элементу.
    - `ngClass` используется для применения классов CSS к элементу.
2. **Формат данных**:
    
    - `ngStyle` принимает объект, где ключи — это свойства стилей CSS, а значения — это значения этих свойств.
    - `ngClass` принимает строку, массив строк или объект, где ключи — это имена классов CSS, а значения — логические значения, определяющие, применять ли данный класс.
3. **Пример с объектом**:
    
    - `ngStyle`:
        
        `<div [ngStyle]="{ 'color': 'red', 'font-weight': 'bold' }"></div>`
        
    - `ngClass`:
        
        `<div [ngClass]="{ 'class1': true, 'class2': false }"></div>`
        

### Итоги

- `ngStyle` используется для динамического применения инлайн-стилей к элементу.
- `ngClass` используется для динамического применения классов CSS к элементу.

Обе директивы полезны для управления внешним видом элементов в зависимости от состояния приложения или данных.

