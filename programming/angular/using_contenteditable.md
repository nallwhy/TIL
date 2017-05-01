## Using `contenteditable`

```typescript
import { Component, ElementRef } from '@angular/core';

@Component({
  selector: 'contenteditable',
  template: `
    <div class="test" contenteditable="true"></div>
    <button (click)="onConfirm()">Confirm</button>
  `
})
export class ContenteditableComponent {
  onConfirm() {
    const description = this.elementRef.nativeElement.querySelector('.test').innerText;
    console.log(description);
  }
}
```

If you want two-way binding to contenteditable element, see also https://www.namekdev.net/2016/01/two-way-binding-to-contenteditable-element-in-angular-2/
