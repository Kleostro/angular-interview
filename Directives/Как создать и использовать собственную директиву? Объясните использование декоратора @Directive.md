## Основные опции

1. **selector**: Указывает, как Angular будет определять, к каким элементам применяется директива. Это обязательное поле.
    
    `@Directive({   selector: '[appHighlight]' })`
    
2. **inputs**: Позволяет указать свойства директивы, которые могут быть установлены через привязки в шаблоне.
    
    `@Directive({   selector: '[appHighlight]',   inputs: ['highlightColor'] })`
    
3. **outputs**: Позволяет указать события, которые директива может эмитировать.
    
    `@Directive({   selector: '[appHighlight]',   outputs: ['highlighted'] })`
    
4. **providers**: Позволяет указать зависимости, которые будут предоставлены директиве.
    
    `@Directive({   selector: '[appHighlight]',   providers: [SomeService] })`
    
5. **exportAs**: Позволяет экспортировать директиву под определенным именем, чтобы к ней можно было обратиться в шаблоне.
    
    `@Directive({   selector: '[appHighlight]',   exportAs: 'highlight' })`
    

## Пример использования всех опций

Давайте рассмотрим пример директивы, которая использует все основные опции:

#### custom.directive.ts

```TS
import { Directive, ElementRef, Renderer2, Input, Output, EventEmitter, OnInit } from '@angular/core';
import { SomeService } from './some.service';

@Directive({
  selector: '[appCustom]',
  inputs: ['highlightColor'],
  outputs: ['highlighted'],
  providers: [SomeService],
  exportAs: 'custom'
})
export class CustomDirective implements OnInit {
  @Input() highlightColor: string;
  @Output() highlighted: EventEmitter<string> = new EventEmitter();

  constructor(private el: ElementRef, private renderer: Renderer2, private someService: SomeService) {}

  ngOnInit() {
    this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', this.highlightColor);
    this.highlighted.emit(`Element highlighted with color: ${this.highlightColor}`);
  }
}
```

#### app.component.html

```TS
<div appCustom [highlightColor]="'yellow'" (highlighted)="onHighlighted($event)" #custom="custom">
  Custom Directive Element
</div>
```

#### app.component.ts

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  onHighlighted(message: string) {
    console.log(message);
  }
}
```

### Подробное описание опций

1. **selector**: Указывает, как Angular будет определять, к каким элементам применяется директива. Это может быть атрибут, класс или элемент.
    
    `selector: '[appHighlight]' // Атрибут selector: '.appHighlight' // Класс selector: 'appHighlight' // Элемент`
    
2. **inputs**: Массив строк, каждая из которых представляет имя свойства директивы, которое может быть установлено через привязку в шаблоне.
    
    `inputs: ['highlightColor', 'anotherProperty']`
    
3. **outputs**: Массив строк, каждая из которых представляет имя события, которое директива может эмитировать.
    
    `outputs: ['highlighted', 'anotherEvent']`
    
4. **providers**: Массив поставщиков зависимостей, которые будут использоваться в директиве.
    
    `providers: [SomeService, AnotherService]`
    
5. **exportAs**: Имя, под которым директива будет экспортироваться в шаблоне, что позволяет обращаться к ней из шаблона.
    
    `exportAs: 'highlight'`
    

Эти опции позволяют гибко настраивать поведение директивы и делать ее более универсальной и многофункциональной.