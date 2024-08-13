
Обработка аутентификации и авторизации с помощью HTTP-интерсепторов в Angular — эффективный способ централизовать логику, связанную с добавлением токенов доступа к запросам и обработкой ответов, связанных с авторизацией. Вот пример, как это можно сделать:

### 1. **Добавление токена авторизации к запросам**

Для добавления токена авторизации к каждому HTTP-запросу, можно создать интерсептор, который будет клонировать запрос и добавлять заголовок `Authorization`.

```TS
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor(private authService: AuthService) {}

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const authToken = this.authService.getAuthToken();
    const authReq = req.clone({
      setHeaders: {
        Authorization: `Bearer ${authToken}`
      }
    });

    return next.handle(authReq);
  }
}
```

### 2. **Обновление токена и перенаправление на страницу входа**

Если сервер возвращает ошибку 401 (Unauthorized) или 403 (Forbidden), интерсептор может обработать эти ответы, обновить токен или перенаправить пользователя на страницу входа.

```TS
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent, HttpErrorResponse } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError, switchMap } from 'rxjs/operators';
import { AuthService } from './auth.service';
import { Router } from '@angular/router';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor(private authService: AuthService, private router: Router) {}

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const authToken = this.authService.getAuthToken();
    let authReq = req.clone({
      setHeaders: {
        Authorization: `Bearer ${authToken}`
      }
    });

    return next.handle(authReq).pipe(
      catchError((error: HttpErrorResponse) => {
        if (error.status === 401) {
          // Токен истек или недействителен, попробуем обновить токен
          return this.authService.refreshToken().pipe(
            switchMap((newToken: string) => {
              // Обновляем запрос с новым токеном
              authReq = req.clone({
                setHeaders: {
                  Authorization: `Bearer ${newToken}`
                }
              });
              return next.handle(authReq);
            }),
            catchError((refreshError) => {
              // Если обновить токен не удалось, перенаправляем на страницу входа
              this.authService.logout();
              this.router.navigate(['/login']);
              return throwError(refreshError);
            })
          );
        } else if (error.status === 403) {
          // Доступ запрещен, можно перенаправить на страницу с ошибкой или входа
          this.router.navigate(['/forbidden']);
        }
        return throwError(error);
      })
    );
  }
}
```

### 3. **Сервис для аутентификации**

Необходимо также создать сервис для управления токенами, аутентификацией и обновлением токенов.

```TS
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable, of } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private authToken: string | null = null;

  constructor(private http: HttpClient) {}

  getAuthToken(): string | null {
    return this.authToken;
  }

  setAuthToken(token: string): void {
    this.authToken = token;
  }

  refreshToken(): Observable<string> {
    // Пример реализации запроса для обновления токена
    return this.http.post<{ token: string }>('/api/refresh-token', {}).pipe(
      tap(response => {
        this.setAuthToken(response.token);
      }),
      map(response => response.token)
    );
  }

  logout(): void {
    this.authToken = null;
    // Дополнительная логика выхода, например, очистка localStorage
  }
}
```

### 4. **Регистрация интерсептора**

Не забудьте зарегистрировать интерсептор в модуле вашего приложения.

```TS
import { HTTP_INTERCEPTORS } from '@angular/common/http';

@NgModule({
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true }
  ]
})
export class AppModule {}
```