
# HostBinding - используется для связывания свойства компонента с атрибутом или свойством его хост-элемента. Это позволяет изменять внешний вид или поведение хост-элемента на основе свойств компонента.

Синтаксис `HostBinding`:

```TS
@HostBinding('attributeName') propertyName;
```

Где `attributeName` - имя атрибута или свойства хост-элемента, а `propertyName` - имя свойства компонента, которое будет связано с этим атрибутом.

```TS
import { Component, HostBinding } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: '<p>My Component</p>'
})
export class MyComponent {
  @HostBinding('class.active') isActive = true;
}
```

В этом примере свойство `isActive` компонента будет связано с атрибутом `class` хост-элемента, что позволит добавить класс `active` к хост-элементу, когда `isActive` равно `true`.


# HostListener - используется для связывания метода компонента с событием хост-элемента. Это позволяет выполнять действия в ответ на события, происходящие на хост-элементе.

Синтаксис `HostListener`:

CopyInsert

```TS
@HostListener('eventName', ['$event']) methodName($event);
```

Где `eventName` - имя события хост-элемента, а `methodName` - имя метода компонента, который будет вызван в ответ на это событие.

```TS
import { Component, HostListener } from '@angular/core';

@Component({
  selector: 'app-my-component',
  template: '<p>My Component</p>'
})
export class MyComponent {
  @HostListener('click', ['$event']) onClick($event) {
    console.log('Clicked!');
  }
}
```

В этом примере метод `onClick` компонента будет вызван в ответ на событие `click` хост-элемента.

