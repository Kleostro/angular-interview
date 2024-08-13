### Observable

**Observable** — это основной строительный блок RxJS. Observable представляет собой поток данных, который может быть как синхронным, так и асинхронным. Observable создается и используется для отправки данных подписчикам (Observers).

#### Пример создания Observable

```TS
import { Observable } from 'rxjs';

const observable = new Observable(subscriber => {
  subscriber.next('Hello');
  subscriber.next('World');
  subscriber.complete();
});
```

### Observer

**Observer** — это объект, который получает уведомления от Observable. Он содержит три метода:

- `next(value)`: Вызывается, когда Observable отправляет новое значение.
- `error(err)`: Вызывается, когда Observable сталкивается с ошибкой.
- `complete()`: Вызывается, когда Observable завершает отправку данных.

#### Пример создания Observer

```TS
const observer = {
  next: (value) => console.log('Received value:', value),
  error: (err) => console.error('Error:', err),
  complete: () => console.log('Stream complete')
};
```

### Subscription

**Subscription** — это объект, представляющий активную подписку на Observable. Он используется для управления подпиской, в частности, для ее отмены.

#### Пример подписки на Observable

```TS
const subscription = observable.subscribe(observer);

// Отмена подписки
subscription.unsubscribe();
```

### Взаимодействие между Observable, Observer и Subscription

1. **Создание Observable**: Вы создаете Observable, который определяет, как и когда данные будут отправлены подписчикам.
2. **Подписка Observer на Observable**: Вы подписываете Observer на Observable, чтобы начать получать данные.
3. **Управление подпиской с помощью Subscription**: Вы используете Subscription для управления и отмены подписки, если это необходимо.

#### Полный пример

```TS
import { Observable } from 'rxjs';

// Создание Observable
const observable = new Observable(subscriber => {
  subscriber.next('Hello');
  subscriber.next('World');
  setTimeout(() => {
    subscriber.complete();
  }, 1000);
});

// Создание Observer
const observer = {
  next: (value) => console.log('Received value:', value),
  error: (err) => console.error('Error:', err),
  complete: () => console.log('Stream complete')
};

// Подписка на Observable
const subscription = observable.subscribe(observer);

// Отмена подписки через 500 мс (если нужно)
setTimeout(() => {
  subscription.unsubscribe();
  console.log('Subscription cancelled');
}, 500);
```

### Заключение

- **Observable** создается для определения потока данных.
- **Observer** подписывается на Observable и получает данные, ошибки и уведомления о завершении.
- **Subscription** представляет собой активную подписку, которую можно отменить, чтобы прекратить получение данных.

Эти концепции являются основными строительными блоками для работы с асинхронными данными и событиями в RxJS и Angular.