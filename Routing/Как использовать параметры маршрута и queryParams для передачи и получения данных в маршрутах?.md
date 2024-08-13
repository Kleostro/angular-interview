
Использование параметров маршрута и queryParams в Angular позволяет передавать данные между компонентами через URL. Это особенно полезно для создания динамических и интерактивных приложений. Давайте рассмотрим, как можно использовать оба типа параметров.

### Параметры маршрута (Route Parameters)

#### Шаг 1: Настройка маршрутов с параметрами

Обновим конфигурацию маршрутов для использования параметров. Например, добавим маршрут для отображения деталей пользователя по его ID:

```TS
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { RouterModule, Routes } from '@angular/router';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { UserDetailComponent } from './user-detail/user-detail.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: 'user/:id', component: UserDetailComponent } // Маршрут с параметром
];

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent,
    UserDetailComponent
  ],
  imports: [
    BrowserModule,
    RouterModule.forRoot(routes)
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### Шаг 2: Получение параметров в компоненте

В компоненте, связанном с маршрутом, используем `ActivatedRoute` для получения параметров.

```TS
// user-detail.component.ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-detail',
  template: `<h2>User Detail</h2><p>User ID: {{ userId }}</p>`
})
export class UserDetailComponent implements OnInit {
  userId: string;

  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
    this.userId = this.route.snapshot.paramMap.get('id');
  }
}
```

#### Шаг 3: Ссылки с параметрами маршрута

Для навигации к маршруту с параметрами используем директиву `routerLink`.

```TS
<!-- app.component.html -->
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
  <a [routerLink]="['/user', 1]">User 1</a>
  <a [routerLink]="['/user', 2]">User 2</a>
</nav>
<router-outlet></router-outlet>
```

### Query Parameters (Параметры запроса)

#### Шаг 1: Настройка маршрутов

Маршруты не требуют специальной настройки для использования queryParams.

#### Шаг 2: Передача queryParams при навигации

Используем директиву `routerLink` для передачи queryParams.

```TS
<!-- app.component.html -->
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
  <a [routerLink]="['/user', 1]" [queryParams]="{ role: 'admin' }">User 1 (Admin)</a>
  <a [routerLink]="['/user', 2]" [queryParams]="{ role: 'user' }">User 2 (User)</a>
</nav>
<router-outlet></router-outlet>
```

#### Шаг 3: Получение queryParams в компоненте

В компоненте используем `ActivatedRoute` для получения queryParams.

```TS
// user-detail.component.ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-detail',
  template: `
    <h2>User Detail</h2>
    <p>User ID: {{ userId }}</p>
    <p>Role: {{ role }}</p>
  `
})
export class UserDetailComponent implements OnInit {
  userId: string;
  role: string;

  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
    this.userId = this.route.snapshot.paramMap.get('id');
    this.role = this.route.snapshot.queryParamMap.get('role');
  }
}
```

### Заключение

Использование параметров маршрута и queryParams в Angular позволяет создавать более динамичные и интерактивные приложения. Параметры маршрута используются для обязательных данных, таких как уникальные идентификаторы, тогда как queryParams чаще используются для фильтрации, сортировки и других опциональных данных.