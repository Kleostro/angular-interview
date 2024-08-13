
Angular предоставляет API `effect()` для создания побочных эффектов, которые автоматически выполняются при изменении сигнала. Это позволяет создать механизм наблюдения за изменениями сигнала и выполнить определенные действия в ответ на эти изменения.

### Пример использования `effect`

Допустим, у нас есть сигнал `count`, и мы хотим выполнять некоторое действие каждый раз, когда его значение изменяется.

```TS
import { signal, effect } from '@angular/core';

// Создаем сигнал
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
    // Создаем эффект в конструкторе компонента
    effect(() => {
      console.log(`Count has changed to: ${this.count()}`);
    });
  }

  increment() {
    this.count.set(this.count() + 1);
  }
}
```

### Остановка эффекта

Если вам нужно остановить выполнение эффекта, вы можете сохранить ссылку на возвращаемую функцию очистки и вызвать её, когда это необходимо.

```TS
import { signal, effect } from '@angular/core';

// Создаем сигнал
const count = signal(0);

// Создаем эффект и сохраняем функцию очистки
const stopEffect = effect(() => {
  console.log(`Count has changed to: ${count()}`);
});

// Изменяем значение сигнала
count.set(1); // Лог: Count has changed to: 1

// Останавливаем эффект
stopEffect();

// Изменяем значение сигнала снова
count.set(2); // Лог не будет вызван, так как эффект остановлен
```

### Пример с компонентом и остановкой эффекта

```TS
import { Component, signal, effect } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `
    <button (click)="increment()">Increment</button>
    <button (click)="stopEffect()">Stop Effect</button>
  `
})
export class ExampleComponent {
  count = signal(0);
  private stopEffectFn: () => void;

  constructor() {
    // Создаем эффект в конструкторе компонента и сохраняем функцию очистки
    this.stopEffectFn = effect(() => {
      console.log(`Count has changed to: ${this.count()}`);
    });
  }

  increment() {
    this.count.set(this.count() + 1);
  }

  stopEffect() {
    // Останавливаем эффект
    this.stopEffectFn();
  }
}
```

### Заключение

API `effect()` в Angular позволяет вам создавать побочные эффекты, которые автоматически выполняются при изменении сигналов. Это дает вам возможность реагировать на изменения данных и выполнять необходимые действия. Эффекты можно также остановить, сохраняя и вызывая функцию очистки, возвращаемую `effect()`.