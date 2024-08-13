
Двустороннее связывание данных (two-way data binding) в контексте Template-driven Forms в Angular позволяет синхронизировать данные между моделью и представлением. Это означает, что изменения в модели автоматически отображаются в представлении, и наоборот, изменения в представлении автоматически обновляются в модели.

### Как работает двустороннее связывание данных:

В Angular для реализации двустороннего связывания данных используется директива `ngModel`. Она создаёт связь между элементами формы (например, `<input>`, `<select>`, `<textarea>`) и моделью данных компонента.

### Пример использования:

#### 1. Создайте компонент:

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-example-form',
  templateUrl: './example-form.component.html'
})
export class ExampleFormComponent {
  user = {
    name: '',
    email: ''
  };

  onSubmit() {
    console.log('Form Submitted!', this.user);
  }
}
```

#### 2. Создайте HTML-шаблон с использованием `ngModel`:

```TS
<form #exampleForm="ngForm" (ngSubmit)="onSubmit()">
  <div>
    <label for="name">Name:</label>
    <input id="name" name="name" [(ngModel)]="user.name" required>
  </div>
  <div>
    <label for="email">Email:</label>
    <input id="email" name="email" [(ngModel)]="user.email" required email>
  </div>
  <button type="submit">Submit</button>
</form>
```

### Что происходит в этом примере:

1. **`[(ngModel)]="user.name"`**:
    
    - `ngModel` связывает значение поля ввода с свойством `user.name` в компоненте.
    - Синтаксис `[(ngModel)]` — это сокращение для реализации двустороннего связывания данных. Он объединяет одностороннюю привязку данных (`[ngModel]`) и событие `ngModelChange` (`(ngModelChange)`).
2. **Обновление модели и представления**:
    
    - Если пользователь вводит текст в поле имени, значение `user.name` в компоненте автоматически обновляется.
    - Если значение свойства `user.name` изменяется в компоненте, текст в поле имени автоматически обновляется.

### Преимущества двустороннего связывания данных:

- **Простота использования**: Легко связывать данные формы с моделью компонента.
- **Синхронизация данных**: Обеспечивает автоматическую синхронизацию между моделью и представлением.
- **Чистый и понятный код**: Упрощает кодировку форм и делает её более читаемой и поддерживаемой.

### Важные замечания:

- Двустороннее связывание данных возможно благодаря директиве `FormsModule`, которую нужно импортировать в модуль вашего приложения:

```TS
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';
import { ExampleFormComponent } from './example-form/example-form.component';

@NgModule({
  declarations: [
    AppComponent,
    ExampleFormComponent
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Использование двустороннего связывания данных с `ngModel` делает работу с Template-driven Forms в Angular простой и интуитивно понятной.