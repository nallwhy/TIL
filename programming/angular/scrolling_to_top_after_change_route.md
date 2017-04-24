## Scrolling to top after changing route

When changing route, the scroll of `outlet` is not initialized(scrolling to the top).

There are several ways to solve this problem.

If you just need to scroll `body` to the top, you can listen route events and scroll `body` to the top. Simple!

```typescript
this.router.events.subscribe(event => {
  document.body.scrollTop = 0;
});
```

Or if you want it in a specific scope of `route`, you can listen `activate` event of `router-outlet` and scroll that outlet to the top.

```typescript
@Component({
  template: '<router-outlet (activate)="onActivate($event, outlet)" #outlet></router-outlet>',
})
export class SomeComponent {
  onActivate(e, outlet) {
    outlet.scrollTop = 0;
  }
}
```

Reference: https://github.com/angular/angular/issues/7791
