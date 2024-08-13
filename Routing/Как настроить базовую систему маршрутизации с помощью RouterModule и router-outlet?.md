
### Основные шаги для настройки маршрутизации

#### Шаг 1: Импортировать RouterModule и настроить маршруты

В файле модуля вашего приложения (например, `app.module.ts`), импортируйте `RouterModule` и настройте маршруты.

```TS
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { RouterModule, Routes } from '@angular/router';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', component: HomeComponent }, // Путь по умолчанию
  { path: 'about', component: AboutComponent } // Путь для страницы "О нас"
];

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent
  ],
  imports: [
    BrowserModule,
    RouterModule.forRoot(routes) // Настройка маршрутов
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

#### Шаг 2: Добавить RouterOutlet в шаблон

В основном шаблоне вашего приложения (`app.component.html`) добавьте директиву `<router-outlet>`.

```TS
<!-- app.component.html -->
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

#### Шаг 3: Создание компонентов

Создайте компоненты, на которые будут ссылаться ваши маршруты, например `HomeComponent` и `AboutComponent`.

```TS
// home.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-home',
  template: `<h2>Home</h2><p>Welcome to the homepage!</p>`
})
export class HomeComponent { }
```

```TS
// about.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-about',
  template: `<h2>About</h2><p>This is the about page.</p>`
})
export class AboutComponent { }
```

### Заключение

Маршрутизация в Angular позволяет создавать одностраничные приложения с несколькими представлениями, обеспечивая плавную и быструю навигацию между различными частями приложения. Она используется для управления навигацией и представлениями, что делает ваше приложение более интерактивным и динамичным.