
Создание собственных структурных директив в Angular позволяет вам реализовать пользовательскую логику для отображения и манипуляции элементами в шаблоне. Для этого часто используется `ng-template`, который позволяет отложить рендеринг части шаблона до момента, когда это будет необходимо.

### Шаги для создания собственной структурной директивы

1. **Создание директивы**.
2. **Использование `TemplateRef` и `ViewContainerRef` для управления вложенным шаблоном**.

### Пример: Создание директивы `appUnless`, которая работает как обратный `*ngIf`

#### Шаг 1: Создание директивы

Создайте новую директиву с помощью Angular CLI:

`ng generate directive appUnless`

#### Шаг 2: Реализация директивы

Откройте файл `unless.directive.ts` и реализуйте директиву.

```TS
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {
  private hasView = false;

  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {}

  @Input() set appUnless(condition: boolean) {
    if (!condition && !this.hasView) {
      this.viewContainer.createEmbeddedView(this.templateRef);
      this.hasView = true;
    } else if (condition && this.hasView) {
      this.viewContainer.clear();
      this.hasView = false;
    }
  }
}
```

#### Шаг 3: Использование директивы в шаблоне

Теперь вы можете использовать вашу структурную директиву в шаблоне. Для этого откройте файл шаблона (например, `app.component.html`) и добавьте следующий код:

```TS
<div *appUnless="isVisible">
  This content is displayed when isVisible is false.
</div>

<button (click)="toggleVisibility()">Toggle Visibility</button>
```

#### Шаг 4: Обновление компонента

Обновите компонент, чтобы управлять условием, используемым в вашей директиве.

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent {
  isVisible = true;

  toggleVisibility() {
    this.isVisible = !this.isVisible;
  }
}
```
### Обзор

1. **`TemplateRef`**: Представляет вложенный шаблон, который вы хотите вставить. В директиве `appUnless` он используется для хранения содержимого, которое будет отображаться или скрываться.
2. **`ViewContainerRef`**: Представляет контейнер для одного или нескольких `View`. В директиве `appUnless` он используется для управления отображением содержимого.

### Заключение

Создание собственных структурных директив позволяет вам расширять функциональность Angular и добавлять пользовательские логические проверки при рендеринге элементов. Использование `ng-template`, `TemplateRef` и `ViewContainerRef` делает этот процесс гибким и мощным.