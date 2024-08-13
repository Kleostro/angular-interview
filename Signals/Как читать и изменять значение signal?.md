
В Angular, чтобы читать и изменять значение `Signal`, можно использовать специальные методы, предоставляемые сигнальным объектом. Давайте рассмотрим простые примеры для чтения и изменения значений `Signal`.

### Создание Signal

Для начала создадим простой `Signal`:

```TS
import { signal } from '@angular/core';

const count = signal(0);
```

### Чтение значения Signal

Для чтения значения `Signal` просто вызовите его как функцию:

```TS
console.log(count()); // Выведет: 0
```

### Изменение значения Signal

Существует несколько способов изменить значение `Signal`:

1. **Метод `set`**: Устанавливает новое значение для сигнала.
    
    ```TS
    count.set(5);
	console.log(count()); // Выведет: 5
	```
    
2. **Метод `update`**: Принимает функцию, которая принимает текущее значение и возвращает новое значение.
    
    ```TS
    count.update(value => value + 1);
	console.log(count()); // Выведет: 6
	```
    
3. **Метод `mutate`**: Позволяет изменять сигнал непосредственно, если он является объектом или массивом. Пример для массива:
    
    ```TS
    const arraySignal = signal([1, 2, 3]);
	
	arraySignal.mutate(arr => {
	  arr.push(4);
	});
	
	console.log(arraySignal()); // Выведет: [1, 2, 3, 4]
	```
    

### Полный пример

```TS
import { signal } from '@angular/core';

const count = signal(0);

// Чтение значения
console.log(count()); // 0

// Установка нового значения
count.set(5);
console.log(count()); // 5

// Обновление значения
count.update(value => value + 1);
console.log(count()); // 6

// Работа с массивом
const arraySignal = signal([1, 2, 3]);

arraySignal.mutate(arr => {
  arr.push(4);
});

console.log(arraySignal()); // [1, 2, 3, 4]
```

### Заключение

Чтение и изменение значений `Signal` в Angular — это простой процесс, который делает управление состоянием более предсказуемым и простым. Используя методы `set`, `update` и `mutate`, вы можете легко управлять значениями сигналов в вашем приложении.