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
