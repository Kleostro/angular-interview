Тестирование директив и пайпов в Angular имеет свои особенности. Давайте рассмотрим, как это можно сделать на примерах.

### Тестирование директив

Рассмотрим простую директиву, которая изменяет цвет текста элемента.

#### Директива `HighlightDirective`

```TS
import { Directive, ElementRef, Renderer2, HostListener } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener('mouseenter') onMouseEnter() {
    this.highlight('yellow');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.highlight('');
  }

  private highlight(color: string) {
    this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', color);
  }
}
```

#### Тест для `HighlightDirective`

```TS
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { Component } from '@angular/core';
import { By } from '@angular/platform-browser';
import { HighlightDirective } from './highlight.directive';

@Component({
  template: `<p appHighlight>Test Highlight</p>`
})
class TestComponent {}

describe('HighlightDirective', () => {
  let fixture: ComponentFixture<TestComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [HighlightDirective, TestComponent]
    });
    fixture = TestBed.createComponent(TestComponent);
    fixture.detectChanges();
  });

  it('should highlight the text on mouse enter', () => {
    const p = fixture.debugElement.query(By.css('p'));
    
    p.triggerEventHandler('mouseenter', null);
    fixture.detectChanges();
    expect(p.nativeElement.style.backgroundColor).toBe('yellow');

    p.triggerEventHandler('mouseleave', null);
    fixture.detectChanges();
    expect(p.nativeElement.style.backgroundColor).toBe('');
  });
});
```

### Тестирование пайпов

Рассмотрим простой пайп, который форматирует строку в верхний регистр.

#### Пайп `UppercasePipe`

```TS
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'uppercase'
})
export class UppercasePipe implements PipeTransform {
  transform(value: string): string {
    return value.toUpperCase();
  }
}
```

#### Тест для `UppercasePipe`

```TS
import { UppercasePipe } from './uppercase.pipe';

describe('UppercasePipe', () => {
  let pipe: UppercasePipe;

  beforeEach(() => {
    pipe = new UppercasePipe();
  });

  it('should transform text to uppercase', () => {
    expect(pipe.transform('hello')).toBe('HELLO');
  });

  it('should handle empty string', () => {
    expect(pipe.transform('')).toBe('');
  });

  it('should handle null value', () => {
    expect(pipe.transform(null)).toBe(null);
  });
});
```

### Объяснение

1. **Тестирование директивы**:
    
    - Мы создаем тестовый компонент `TestComponent`, который использует директиву `HighlightDirective`.
    - В тесте мы эмулируем события `mouseenter` и `mouseleave` для проверки изменения фона элемента.
2. **Тестирование пайпа**:
    
    - Мы создаем экземпляр пайпа `UppercasePipe`.
    - В тестах проверяем различные входные значения, чтобы убедиться, что пайп правильно преобразует строки в верхний регистр.

Эти примеры показывают, как тестировать директивы и пайпы в Angular, обеспечивая их корректную работу и взаимодействие с компонентами.