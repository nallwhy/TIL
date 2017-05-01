## How to manage subscriptions

```typescript
// rx-dispose.ts
import { OnDestroy } from '@angular/core';
import { Subject } from 'rxjs/Subject';

class RxDispose implements OnDestroy {
  protected disposeBag = new Subject<void>();

  ngOnDestroy() {
    this.disposeBag.next();
    this.disposeBag.complete();
  }
}

...
import 'rxjs/add/operator/takeUntil';
import { RxDispose } from '...';

@Component({
...
})
class MyComponent extends RxDispose {

  constructor(
    private myService: MyService
  ) { super(); }

  test() {
    this.myService.getAny()
      .takeUntil(this.disposeBag)
      .subscribe(...)
  }
}
```

Reference: http://stackoverflow.com/questions/38008334/angular2-rxjs-when-should-i-unsubscribe-from-subscription
