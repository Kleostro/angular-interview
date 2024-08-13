
`ngIf` и `ngFor` — это директивы структурного типа в Angular, которые позволяют изменять структуру DOM на основе условий или данных.

### Директива `ngIf`

Директива `ngIf` используется для условного отображения элементов в шаблоне. Если выражение, переданное в `ngIf`, истинно, элемент отображается; если ложно — элемент удаляется из DOM.

#### Пример использования `ngIf`

```TS
<div *ngIf="isVisible">
  This text is visible if the 'isVisible' variable is true.
</div>
```

#### Компонент

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="toggleVisibility()">Toggle Visibility</button>
    <div *ngIf="isVisible">
      This text is visible if the 'isVisible' variable is true.
    </div>
  `
})
export class AppComponent {
  isVisible = true;

  toggleVisibility() {
    this.isVisible = !this.isVisible;
  }
}
```

### Директива `ngFor`

Директива `ngFor` используется для итерации по массиву и отображения элемента шаблона для каждого элемента массива. Она создает копию элемента для каждого элемента массива.

#### Пример использования `ngFor`

```TS
<ul>
  <li *ngFor="let item of items; let i = index">
    {{ i }} - {{ item }}
  </li>
</ul>
```

#### Компонент

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <ul>
      <li *ngFor="let item of items; let i = index">
        {{ i }} - {{ item }}
      </li>
    </ul>
  `
})
export class AppComponent {
  items = ['Item 1', 'Item 2', 'Item 3', 'Item 4'];
}
```

### Подробное объяснение

#### `ngIf`

- **Синтаксис**: `*ngIf="condition"`, где `condition` — логическое выражение.
- **Пример**:
    
    ```TS
    <div *ngIf="user.isLoggedIn">
	  Welcome, {{ user.name }}!
	</div>
    ```
    
- **Описание**: Если `user.isLoggedIn` истинно, div будет отображен, иначе — нет.

#### `ngFor`

- **Синтаксис**: `*ngFor="let item of items; let i = index"`, где `item` — текущий элемент массива, `items` — массив, по которому происходит итерация, `i` — индекс текущего элемента.
- **Пример**:
    
    
    ```TS
    <ul>
	  <li *ngFor="let user of users; let i = index">
	    {{ i + 1 }}. {{ user.name }}
	  </li>
	</ul>
	```
    
- **Описание**: Для каждого элемента в массиве `users`, будет создан элемент `li`, в котором будет отображено имя пользователя и его индекс в массиве.

### Расширенные возможности

#### ngIf с else

Вы можете использовать `ngIf` вместе с `else` для отображения альтернативного шаблона, когда условие ложно.

```TS
<div *ngIf="isLoggedIn; else loggedOut">
  Welcome back!
</div>
<ng-template #loggedOut>
  Please log in.
</ng-template>
```


#### ngFor с trackBy

Для оптимизации рендеринга можно использовать `trackBy`, чтобы Angular отслеживал изменения в коллекции более эффективно.

```TS
<ul>
  <li *ngFor="let item of items; trackBy: trackByFn">
    {{ item.id }} - {{ item.name }}
  </li>
</ul>

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  items = [
    { id: 1, name: 'Item 1' },
    { id: 2, name: 'Item 2' },
    { id: 3, name: 'Item 3' }
  ];

  trackByFn(index: number, item: any): number {
    return item.id; // уникальный идентификатор элемента
  }
}
```

Эти возможности `ngIf` и `ngFor` делают их незаменимыми инструментами для гибкого и эффективного управления отображением элементов в Angular приложениях.