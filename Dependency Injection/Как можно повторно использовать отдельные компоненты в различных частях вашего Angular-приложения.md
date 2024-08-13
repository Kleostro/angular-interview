
Повторное использование компонентов в Angular достигается благодаря созданию их в виде модулей и использовании их в различных частях приложения. Вот шаги, которые необходимо выполнить для достижения этого:

### 1. Создание повторно используемого компонента

Создайте новый компонент, который будет использован повторно.

`ng generate component shared/my-reusable-component`

#### Пример компонента:

```TS
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-my-reusable-component',
  template: `<div>{{message}}</div>`,
})
export class MyReusableComponent {
  @Input() message: string;
}
```

### 2. Создание модуля для общего использования

Создайте модуль, который будет содержать все повторно используемые компоненты. Это позволяет вам импортировать этот модуль в любые другие модули приложения.

`ng generate module shared/shared`

#### Пример модуля:

```TS
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MyReusableComponent } from './my-reusable-component/my-reusable-component.component';

@NgModule({
  declarations: [MyReusableComponent],
  imports: [CommonModule],
  exports: [MyReusableComponent] // Экспортируем компонент
})
export class SharedModule { }
```

### 3. Импортирование модуля в другие модули

Теперь вы можете импортировать ваш `SharedModule` в любые другие модули вашего приложения, где вы хотите использовать повторно используемый компонент.

#### Пример использования в `AppModule`:

```TS
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { SharedModule } from './shared/shared.module'; // Импортируем SharedModule

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, SharedModule], // Добавляем SharedModule в импорты
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### Пример использования в другом модуле (например, `FeatureModule`):

```TS
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FeatureComponent } from './feature.component';
import { SharedModule } from '../shared/shared.module'; // Импортируем SharedModule

@NgModule({
  declarations: [FeatureComponent],
  imports: [CommonModule, SharedModule], // Добавляем SharedModule в импорты
})
export class FeatureModule { }
```

### 4. Использование компонента в шаблонах

Теперь вы можете использовать ваш повторно используемый компонент в шаблонах любых компонентов, которые относятся к модулям, импортирующим `SharedModule`.

#### Пример использования в шаблоне:

```TS
<!-- app.component.html -->
<app-my-reusable-component message="Hello from AppComponent!"></app-my-reusable-component>

<!-- feature.component.html -->
<app-my-reusable-component message="Hello from FeatureComponent!"></app-my-reusable-component>
```

### Заключение

Создание повторно используемых компонентов и модулей в Angular позволяет легко поддерживать и масштабировать ваше приложение. Это достигается путем:

1. Создания компонентов.
2. Объединения их в общий модуль.
3. Импортирования этого модуля в любые другие модули приложения.

Этот подход обеспечивает модульность, повторное использование кода и упрощает поддержку.