
DI-токен (Dependency Injection Token) в Angular используется для уникальной идентификации зависимости, которую необходимо внедрить. Токены позволяют Angular отличать разные зависимости и правильно их разрешать.

### Типы DI-токенов

1. **Классовый токен**:
    
    - Используется, когда класс служит в качестве ключа для зависимости.
    - Пример: `MyService`.
2. **Строковый токен**:
    
    - Используется, когда строка служит в качестве ключа для зависимости.
    - Пример: `'API_ENDPOINT'`.
3. **InjectionToken**:
    
    - Специальный тип токена, предоставляемый Angular для создания уникальных токенов.
    - Используется для более сложных типов данных или конфигураций, особенно если требуется типизация.
    - Пример: `new InjectionToken<string>('API_ENDPOINT')`.

### Использование DI-токенов

#### Классовый токен

Классовые токены наиболее распространены и используются по умолчанию, когда вы регистрируете сервисы.

```TS
@Injectable({
  providedIn: 'root',
})
export class MyService {
  // Логика сервиса
}

@Component({
  selector: 'app-my-component',
  template: `<div></div>`,
})
export class MyComponent {
  constructor(private myService: MyService) {
    // Использование сервиса
  }
}
```

В этом примере `MyService` используется как токен для внедрения зависимости.

#### Строковый токен

Строковые токены могут быть полезны для внедрения простых значений или объектов конфигурации.

```TS
@NgModule({
  providers: [
    { provide: 'API_ENDPOINT', useValue: 'https://api.example.com' }
  ]
})
export class AppModule { }

@Component({
  selector: 'app-my-component',
  template: `<div>{{ apiEndpoint }}</div>`,
})
export class MyComponent {
  constructor(@Inject('API_ENDPOINT') public apiEndpoint: string) {}
}
```

В этом примере строка `'API_ENDPOINT'` используется как токен для внедрения значения.

#### InjectionToken

`InjectionToken` используется для создания уникальных и типизированных токенов, что особенно полезно для сложных конфигураций.

```TS
import { InjectionToken } from '@angular/core';

export const API_ENDPOINT = new InjectionToken<string>('API_ENDPOINT');

@NgModule({
  providers: [
    { provide: API_ENDPOINT, useValue: 'https://api.example.com' }
  ]
})
export class AppModule { }

@Component({
  selector: 'app-my-component',
  template: `<div>{{ apiEndpoint }}</div>`,
})
export class MyComponent {
  constructor(@Inject(API_ENDPOINT) public apiEndpoint: string) {}
}
```

В этом примере `InjectionToken` используется для создания уникального токена `API_ENDPOINT`.

### Заключение

DI-токены в Angular позволяют четко и однозначно идентифицировать зависимости, что делает систему внедрения зависимостей более гибкой и мощной. Использование различных типов токенов помогает лучше организовать код, особенно в сложных приложениях с множеством зависимостей.