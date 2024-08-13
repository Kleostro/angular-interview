
В Angular вы можете легко отслеживать состояния форм и их элементов управления, такие как `touched`, `dirty`, `pristine`, `valid`, `invalid` и другие. Эти состояния помогают вам управлять поведением и отображением формы в зависимости от состояния ввода пользователя.

### Основные состояния формы и элементов управления:

- `touched`: Элемент управления был затронут пользователем.
- `dirty`: Значение элемента управления было изменено пользователем.
- `pristine`: Значение элемента управления не было изменено.
- `valid`: Элемент управления прошел все проверки валидаторов.
- `invalid`: Элемент управления не прошел проверки валидаторов.

### Пример отслеживания состояний формы и элементов управления:

#### Шаги:

1. **Создайте форму с помощью `FormBuilder`**: Начнем с создания формы, как в предыдущем примере.

```TS
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-example-form',
  templateUrl: './example-form.component.html',
  styleUrls: ['./example-form.component.scss']
})
export class ExampleFormComponent {
  exampleForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.exampleForm = this.fb.group({
      name: ['', Validators.required],
      email: ['', [Validators.required, Validators.email]]
    });
  }

  onSubmit() {
    if (this.exampleForm.valid) {
      const formData = this.exampleForm.value;
      console.log('Form Data:', formData);

      // Обработка данных
      // Например, отправка данных на сервер
      // this.myService.submitForm(formData).subscribe(response => {
      //   console.log('Response:', response);
      // });
    }
  }
}
```

2. **Отслеживание состояний в шаблоне**: Используйте директивы Angular и встроенные свойства для отображения состояний формы и элементов управления.

```TS
<form [formGroup]="exampleForm" (ngSubmit)="onSubmit()">
  <div>
    <label for="name">Name:</label>
    <input id="name" formControlName="name" required>
    <div *ngIf="exampleForm.get('name').touched && exampleForm.get('name').invalid">
      <small *ngIf="exampleForm.get('name').errors.required">Name is required.</small>
    </div>
  </div>
  <div>
    <label for="email">Email:</label>
    <input id="email" formControlName="email" required email>
    <div *ngIf="exampleForm.get('email').touched && exampleForm.get('email').invalid">
      <small *ngIf="exampleForm.get('email').errors.required">Email is required.</small>
      <small *ngIf="exampleForm.get('email').errors.email">Email is invalid.</small>
    </div>
  </div>
  <button type="submit">Submit</button>
</form>
```
### Объяснение:

1. **Получение контролов**: Используйте метод `get` для получения конкретного элемента управления формы.
    
    `exampleForm.get('name')`
    
2. **Отслеживание состояний**: Используйте встроенные свойства, такие как `touched`, `dirty`, `valid`, `invalid`, чтобы отслеживать состояния.
    
    ```TS
    <div *ngIf="exampleForm.get('name').touched && exampleForm.get('name').invalid">
	  <small *ngIf="exampleForm.get('name').errors.required">Name is required.</small>
	</div>
	```
    
3. **Условный рендеринг сообщений об ошибках**: Выводите сообщения об ошибках на основе состояния элемента управления.
    

### Дополнительные состояния:

- **`pristine`**: Элемент управления не был изменен.
    
    ```TS
    <div *ngIf="exampleForm.get('name').pristine">
	  <small>Name has not been changed.</small>
	</div>
	```
    
- **`valid` и `invalid`**: Проверка валидности элемента управления.
    
    ```TS
    <div *ngIf="exampleForm.get('email').valid">
	  <small>Email is valid.</small>
	</div>
	```
    

Эти состояния и свойства позволяют вам гибко управлять поведением и отображением формы в зависимости от взаимодействия пользователя.