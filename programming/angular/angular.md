### 2018-05-17

#### Super Powered, Server Rendered Progressive Native Apps - Nathan Walker, Jeff Whelpley

https://www.youtube.com/watch?v=EqqNexmu3Ug

https://nstudio.io/xplat/


### 2017-10-14

#### The Ultimate Angular CLI Reference Guide

https://www.sitepoint.com/ultimate-angular-cli-reference/


### 2017-07-09

#### ngAir 120 - Code Sharing between NativeScript and Web with Sebastian Witalec

https://www.youtube.com/watch?v=uEPSY_X9pUc


### 2017-07-08

#### Great Progressive Web App Experiences with Angular (Google I/O '17)

https://www.youtube.com/watch?v=C8KcW1Nj3Mw


### 2017-06-05

#### Preserving query params for the next navigation

https://angular.io/docs/js/latest/api/router/index/NavigationExtras-interface.html

```typescript
// Preserve query params from /results?page=1 to /view?page=1
this.router.navigate(['/view'], { preserveQueryParams: true });
```

#### Angular-Material 2 Theme Tutorial

https://medium.com/covalent-ui/angular-material-2-theme-tutorial-2f7e6c344006


### 2017-06-02

#### Angular University

https://angular-university.io/


### 2017-05-09

#### Build a simple Emoji Chrome Extension with Angular CLI

https://medium.com/@_JoshSommer/build-a-simple-emoji-chrome-extension-with-angular-cli-84937a1ca640

#### Preloading in Angular

https://alligator.io/angular/preloading


### 2017-05-03

#### Sidenav and fixed elements

https://github.com/angular/material2/issues/3031

`position: fixed` elements inside `transform: translate3d()` doesn't work.


### 2017-05-02

#### Angular Language Service

http://brianflove.com/2017/04/11/angular-language-service/


### 2017-05-01

#### Angular Augury

https://augury.angular.io/

A Google Chrome Dev Tools extension for debugging Angular 2 applications.

#### Angular2 Routerlink: add query parameters

http://stackoverflow.com/questions/35226245/angular2-routerlink-add-query-parameters

```html
<a [routerLink]="['/users']" [queryParams]="{ page: 1 }">next page</a>
```

#### Pagination for Angular (ngx-pagination)

https://github.com/michaelbromley/ngx-pagination

#### Angular Infinite Scroll (ngx-infinite-scroll)

https://github.com/orizens/ngx-infinite-scroll

#### Use pipes in services

http://stackoverflow.com/questions/35144821/angular-2-use-pipes-in-services?answertab=active#tab-top

```typescript
import { DatePipe } from '@angular/common';
class MyService {
  constructor(private datePipe: DatePipe) {}

  test() {
    this.datePipe.transform(new Date(), 'yyyyMMdd');
  }
}

// app.module.ts
providers: [DatePipe, ...]
```


### 2017-04-18

#### Reactive Forms in Angular: Creating a Custom Validator

https://alligator.io/angular/reactive-forms-custom-validator


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
