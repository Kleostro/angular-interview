
Валидация форм в Angular может быть реализована по-разному в зависимости от используемого подхода: **Template-driven Forms** или **Reactive Forms**. Рассмотрим основные различия в работе с валидацией для этих двух подходов.

### Template-driven Forms

#### Объявление валидации

В Template-driven Forms валидация объявляется непосредственно в шаблоне с использованием атрибутов HTML и Angular-директив.

#### Пример

```TS
<form #form="ngForm">
  <input name="name" ngModel required minlength="3">
  <div *ngIf="form.controls.name?.invalid && form.controls.name?.touched">
    <div *ngIf="form.controls.name.errors?.required">Name is required</div>
    <div *ngIf="form.controls.name.errors?.minlength">Name must be at least 3 characters long</div>
  </div>
  <button type="submit" [disabled]="form.invalid">Submit</button>
</form>
```

#### Особенности

- **Простота**: Валидация легко добавляется через атрибуты HTML.
- **Декларативность**: Валидация прописывается прямо в шаблоне, что делает код более читаемым.
- **Ограниченная гибкость**: Подходит для простых случаев валидации, но сложные сценарии могут быть труднее реализовать.

### Reactive Forms

#### Объявление валидации

В Reactive Forms валидация объявляется программно с использованием валидаторов, которые добавляются к элементам формы в TypeScript-коде.

#### Пример

```TS
import { FormGroup, FormControl, Validators } from '@angular/forms';

this.form = new FormGroup({
  name: new FormControl('', [Validators.required, Validators.minLength(3)])
});
```

```TS
<form [formGroup]="form">
  <input formControlName="name">
  <div *ngIf="form.controls.name.invalid && form.controls.name.touched">
    <div *ngIf="form.controls.name.errors?.required">Name is required</div>
    <div *ngIf="form.controls.name.errors?.minlength">Name must be at least 3 characters long</div>
  </div>
  <button type="submit" [disabled]="form.invalid">Submit</button>
</form>
```

#### Особенности

- **Гибкость**: Более мощный и гибкий способ управления валидацией, подходящий для сложных сценариев.
- **Программируемость**: Позволяет легко добавлять динамические валидаторы и управлять состоянием формы в коде.
- **Синхронность**: Обновления формы происходят синхронно, что делает поведение более предсказуемым.

### Различия в подходах


### Template-driven Forms:

1. **Место объявления**:
    - В шаблоне (HTML)
2. **Сложность**:
    - Простая настройка
3. **Гибкость**:
    - Ограниченная
4. **Привязка данных**:
    - Двусторонняя (ngModel)
5. **Валидация**:
    - Атрибуты HTML и Angular-директивы
6. **Поддержка динамики**:
    - Менее удобна для динамических форм
7. **Читаемость**:
    - Легко читается, так как всё в шаблоне

### Reactive Forms:

1. **Место объявления**:
    - В TypeScript-коде
2. **Сложность**:
    - Подходит для сложных форм и логики
3. **Гибкость**:
    - Высокая
4. **Привязка данных**:
    - Односторонняя (formControlName, formGroup)
5. **Валидация**:
    - Программная с использованием валидаторов
6. **Поддержка динамики**:
    - Легко управляется динамическими изменениями
7. **Читаемость**:
    - Легко управляется, так как логика в коде

### Когда использовать

- **Template-driven Forms**: Подходят для простых форм, которые не требуют сложной логики и валидации. Легче освоить и использовать, особенно для небольших приложений.
- **Reactive Forms**: Подходят для сложных форм с богатой логикой валидации и динамическим управлением состоянием. Лучше масштабируются и обеспечивают более предсказуемое поведение.
