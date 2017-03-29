### 2017-03-29

#### Using decorators and observables to implement retry

http://blog.kwintenp.com/decorators-and-observables-to-implement-retry-logic

How to create decorator.

#### Server Side Rendering With Angular 4

https://www.softwarearchitekt.at/post/2017/03/07/server-side-rendering-with-angular-4.aspx


### 2017-03-28

#### Top 27 Angular 2 Components for Web Developers

https://colorlib.com/wp/angular-2-components


### 2017-03-16

#### Get key events
```typescript
// example
@HostListener('document:keypress', ['$event'])
handleKeyboardEvent(event: KeyboardEvent) {
  this.key = event.key;
}
```

Reference: http://stackoverflow.com/questions/37362488/angular-2-listen-for-keypress-event-on-whole-page

#### Style inheritance

```css
:host /deep/ h3 {
  font-style: italic;
}

// or

:host >>> h3 {
  font-style: italic;
}
```

Reference: https://angular.io/docs/ts/latest/guide/component-styles.html
