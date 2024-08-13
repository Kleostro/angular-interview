
В Angular сигналы предоставляют встроенные механизмы для реагирования на их изменения, что делает их использование простым и интуитивным. Основной способ "подписки" на сигнал заключается в использовании функции `effect`. Давайте рассмотрим, как это делается.

### Использование `effect`

Функция `effect` позволяет вам создавать побочные эффекты, которые автоматически выполняются каждый раз, когда сигнал изменяется.

#### Пример

```TS
import { signal, effect } from '@angular/core';

const count = signal(0);

// Создаем эффект, который будет выполняться при изменении count
effect(() => {
  console.log(`Count has changed to: ${count()}`);
});

// Изменяем значение сигнала
count.set(1); // Лог: Count has changed to: 1
count.set(2); // Лог: Count has changed to: 2
```

### Пример с компонентом

Давайте посмотрим, как это работает в контексте Angular компонента.

```TS
import { Component, signal, effect } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `<button (click)="increment()">Increment</button>`
})
export class ExampleComponent {
  count = signal(0);

  constructor() {
    effect(() => {
      console.log(`Count has changed to: ${this.count()}`);
    });
  }

  increment() {
    this.count.set(this.count() + 1);
  }
}
```

### Использование `computed`

Хотя `computed` - это не совсем "подписка", его также можно использовать для создания зависимых значений, которые автоматически обновляются при изменении исходного сигнала.

```TS
import { signal, computed } from '@angular/core';

const count = signal(0);
const doubleCount = computed(() => count() * 2);

console.log(doubleCount()); // 0

count.set(1);
console.log(doubleCount()); // 2
```

### Пример с компонентом и `computed`

```TS
import { Component, signal, computed } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `
    <button (click)="increment()">Increment</button>
    <p>Count: {{ count() }}</p>
    <p>Double Count: {{ doubleCount() }}</p>
  `
})
export class ExampleComponent {
  count = signal(0);
  doubleCount = computed(() => this.count() * 2);

  increment() {
    this.count.set(this.count() + 1);
  }
}
```

### Заключение

Для подписки на изменения сигнала в Angular используйте функцию `effect`, которая создает побочные эффекты, автоматически выполняющиеся при изменении сигнала. Это делает работу с реактивными данными простой и удобной. Также можно использовать `computed` для создания зависимых значений, которые автоматически обновляются при изменении исходных сигналов.