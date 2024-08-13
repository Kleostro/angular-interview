
Route Guards в Angular позволяют контролировать доступ к маршрутам на основе определенных условий. Они могут быть использованы для защиты маршрутов от неавторизованных пользователей, проверки несохраненных изменений и других задач. Наиболее часто используемые guard'ы - это `CanActivate` и `CanDeactivate`.

### Пример использования `CanActivate`

`CanActivate` guard используется для проверки, имеет ли пользователь право на доступ к маршруту.

#### Шаг 1: Создание guard'а

```TS
// auth.guard.ts
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';
import { AuthService } from './auth.service'; // пример сервиса авторизации

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(): boolean {
    if (this.authService.isLoggedIn()) {
      return true;
    } else {
      this.router.navigate(['/login']);
      return false;
    }
  }
}
```

#### Шаг 2: Использование guard'а в маршрутах

```TS
// app.routes.ts
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { DashboardComponent } from './dashboard/dashboard.component';
import { LoginComponent } from './login/login.component';
import { AuthGuard } from './auth.guard';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] },
  { path: 'login', component: LoginComponent }
];

export default routes;
```

### Пример использования `CanDeactivate`

`CanDeactivate` guard используется для проверки, можно ли покинуть маршрут, например, если на странице есть несохраненные изменения.

#### Шаг 1: Создание интерфейса для компонента

```TS
// can-deactivate.component.ts
export interface CanComponentDeactivate {
  canDeactivate: () => boolean | Promise<boolean>;
}
```

#### Шаг 2: Создание guard'а

```TS
// can-deactivate.guard.ts
import { Injectable } from '@angular/core';
import { CanDeactivate } from '@angular/router';
import { CanComponentDeactivate } from './can-deactivate.component';

@Injectable({
  providedIn: 'root'
})
export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {
  canDeactivate(component: CanComponentDeactivate): boolean | Promise<boolean> {
    return component.canDeactivate ? component.canDeactivate() : true;
  }
}
```

#### Шаг 3: Реализация интерфейса в компоненте

```TS
// edit-profile.component.ts
import { Component } from '@angular/core';
import { CanComponentDeactivate } from './can-deactivate.component';

@Component({
  selector: 'app-edit-profile',
  template: `<h2>Edit Profile</h2>`
})
export class EditProfileComponent implements CanComponentDeactivate {
  canDeactivate(): boolean {
    // Логика проверки, можно ли покинуть страницу (например, проверка несохраненных изменений)
    return confirm('Are you sure you want to leave this page?');
  }
}
```

#### Шаг 4: Использование guard'а в маршрутах

```TS
// app.routes.ts
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { EditProfileComponent } from './edit-profile/edit-profile.component';
import { CanDeactivateGuard } from './can-deactivate.guard';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'edit-profile', component: EditProfileComponent, canDeactivate: [CanDeactivateGuard] }
];

export default routes;
```

### Заключение

Использование route guards в Angular позволяет контролировать доступ к маршрутам и защищать их от неавторизованного доступа или предотвратить потерю данных при навигации. `CanActivate` подходит для проверки доступа к маршруту, а `CanDeactivate` - для проверки возможности покинуть маршрут.