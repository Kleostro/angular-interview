
`ActivatedRoute` в Angular представляет собой сервис, который предоставляет доступ к информации о маршруте, который был активирован. Он позволяет получать данные о текущем маршруте, параметры маршрута, данные, переданные через маршрут, и другую связанную информацию.

### Основные возможности `ActivatedRoute`

- **Параметры маршрута** (`params`): Параметры, указанные в пути URL.
- **Параметры запроса** (`queryParams`): Параметры, указанные после знака `?` в URL.
- **Фрагмент URL** (`fragment`): Часть URL после знака `#`.
- **Данные маршрута** (`data`): Дополнительные данные, которые могут быть переданы при конфигурации маршрута.
- **Параметры родительского маршрута** (`parent`): Доступ к информации о родительском маршруте.

### Пример использования `ActivatedRoute`

Рассмотрим пример, где мы используем `ActivatedRoute` для получения параметров маршрута и параметров запроса.

#### Шаг 1: Настройка маршрутов

```TS
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { UserComponent } from './user/user.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'user/:id', component: UserComponent } // Маршрут с параметром `id`
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

#### Шаг 2: Получение информации о маршруте в компоненте

```TS
// user.component.ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user',
  template: `
    <h2>User Component</h2>
    <p>User ID: {{ userId }}</p>
    <p>Query Params: {{ queryParams | json }}</p>
  `
})
export class UserComponent implements OnInit {
  userId: string | null = null;
  queryParams: any = {};

  constructor(private route: ActivatedRoute) {}

  ngOnInit(): void {
    // Получение параметра маршрута `id`
    this.userId = this.route.snapshot.paramMap.get('id');

    // Подписка на изменения параметров маршрута
    this.route.params.subscribe(params => {
      this.userId = params['id'];
    });

    // Получение параметров запроса
    this.queryParams = this.route.snapshot.queryParams;

    // Подписка на изменения параметров запроса
    this.route.queryParams.subscribe(params => {
      this.queryParams = params;
    });
  }
}
```

#### Шаг 3: Навигация к маршруту

Чтобы перейти к маршруту и передать параметры, можно использовать `Router`:

```TS
// some.component.ts
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-some',
  template: `<button (click)="goToUser()">Go to User</button>`
})
export class SomeComponent {
  constructor(private router: Router) {}

  goToUser(): void {
    this.router.navigate(['/user', 1], { queryParams: { ref: 'home' } });
  }
}
```

### Заключение

`ActivatedRoute` предоставляет мощные возможности для получения информации о текущем маршруте и параметрах URL. Это особенно полезно для динамической загрузки данных и управления состоянием приложения на основе URL.