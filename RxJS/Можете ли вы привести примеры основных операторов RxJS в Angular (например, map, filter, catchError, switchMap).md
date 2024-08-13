
Операторы RxJS играют ключевую роль в работе с потоками данных в Angular. Давайте рассмотрим примеры использования некоторых основных операторов RxJS: `map`, `filter`, `catchError`, и `switchMap`.

### 1. `map`

Оператор `map` используется для трансформации значений, испускаемых Observable.

```TS
import { of } from 'rxjs';
import { map } from 'rxjs/operators';

const numbers$ = of(1, 2, 3, 4, 5);

numbers$.pipe(
  map(value => value * 2)
).subscribe(result => console.log(result)); // 2, 4, 6, 8, 10
```

### 2. `filter`

Оператор `filter` используется для фильтрации значений, испускаемых Observable, на основе предиката.

```TS
import { of } from 'rxjs';
import { filter } from 'rxjs/operators';

const numbers$ = of(1, 2, 3, 4, 5);

numbers$.pipe(
  filter(value => value % 2 === 0)
).subscribe(result => console.log(result)); // 2, 4
```

### 3. `catchError`

Оператор `catchError` используется для обработки ошибок в Observable.

```TS
import { of, throwError } from 'rxjs';
import { catchError } from 'rxjs/operators';

const source$ = throwError('Error occurred');

source$.pipe(
  catchError(error => {
    console.error(error);
    return of('Error handled');
  })
).subscribe(result => console.log(result)); // "Error handled"
```

### 4. `switchMap`

Оператор `switchMap` используется для переключения на новый Observable, отменяя предыдущий. Это полезно для работы с последовательными асинхронными запросами, такими как HTTP-запросы.

```TS
import { fromEvent } from 'rxjs';
import { switchMap, map } from 'rxjs/operators';
import { ajax } from 'rxjs/ajax';

const button = document.getElementById('button');

const clicks$ = fromEvent(button, 'click');

clicks$.pipe(
  switchMap(() => ajax.getJSON('https://api.example.com/data'))
).subscribe(response => console.log(response));
```

### Пример использования операторов в Angular

Предположим, у нас есть Angular сервис, который делает HTTP-запрос и использует различные операторы RxJS для обработки данных:

```TS
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { map, filter, catchError, switchMap } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  constructor(private http: HttpClient) {}

  getData(): Observable<any> {
    return this.http.get<any[]>('https://api.example.com/data').pipe(
      map(data => data.filter(item => item.active)), // Фильтрация активных элементов
      map(data => data.map(item => ({ ...item, name: item.name.toUpperCase() }))), // Преобразование данных
      catchError(error => {
        console.error('Error occurred:', error);
        return of([]); // Возвращаем пустой массив в случае ошибки
      })
    );
  }

  getDataOnClick(button: HTMLElement): Observable<any> {
    return fromEvent(button, 'click').pipe(
      switchMap(() => this.http.get<any[]>('https://api.example.com/data')),
      catchError(error => {
        console.error('Error occurred:', error);
        return of([]); // Возвращаем пустой массив в случае ошибки
      })
    );
  }
}
```

### Заключение

Операторы RxJS, такие как `map`, `filter`, `catchError` и `switchMap`, предоставляют мощные инструменты для работы с потоками данных в Angular. Они позволяют трансформировать, фильтровать, обрабатывать ошибки и управлять асинхронными запросами удобным и декларативным способом.