### 2017-04-17

#### Angular CLI Deployment: Host Your Angular 2 App on Heroku

https://medium.com/@ryanchenkie_40935/angular-cli-deployment-host-your-angular-2-app-on-heroku-3f266f13f352


#### Understanding Angular modules (NgModule) and their scopes

https://medium.com/@cyrilletuzi/understanding-angular-modules-ngmodule-and-their-scopes-81e4ed6f7407

The purpose of a *NgModule* is to declare each thing you create in Angular.

There is two kind of main structures :  
*declarations* is for things you’ll use in your templates : mainly components (~ *views* : the classes displaying data), but also directives and pipes.  
*providers* is for services (~ *models* : the classes getting and handling data).

It seemed unnecessary complexity, as it feels redundant with ES6 imports. But it's worth it.

* It allows *Ahead of Time (AoT) compilation*, which is amazing for performance.
* It actually saves you many lines of imports. In beta versions of Angular 2, you needed to import your components and directives every time you used them.

And How to import modules..


### 2017-03-29

#### Using decorators and observables to implement retry

http://blog.kwintenp.com/decorators-and-observables-to-implement-retry-logic

How to create decorator.

#### Server Side Rendering With Angular 4

https://www.softwarearchitekt.at/post/2017/03/07/server-side-rendering-with-angular-4.aspx

#### Planning An Angular Application

http://developer.telerik.com/topics/web-development/planning-an-angular-application

Angular 개발 시 이럴 땐 이걸 써라 정리.


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
