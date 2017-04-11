## Angular Material with Angular CLI

### Install dependencies

```bash
$ ng new <app-name>
$ cd <app-name>
$ yarn add @angular/material
$ yarn add @angular/animations
$ yarn add hammerjs
```


### Import the Modules

```typescript
// app.module.ts
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MaterialModule } from '@angular/material';
import 'hammerjs'
...

@NgModule({
  ...
  imports: [
    ...
    BrowserAnimationModule,
    MaterialModule,
  ],
  ...
})
export class AppModule { }
```


### Define a custom theme

Create a custom theme scss file, in this example `theme.scss`.  
(You can generate a custom pallete on http://mcg.mbitson.com/)
```scss
@import "~@angular/material/theming";

@include mat-core();

// #db047a
$my-primary: (
  50 : #fbe1ef,
  100 : #f4b4d7,
  200 : #ed82bd,
  300 : #e64fa2,
  400 : #e02a8e,
  500 : #db047a,
  600 : #d70372,
  700 : #d20367,
  800 : #cd025d,
  900 : #c4014a,
  A100 : #ffecf2,
  A200 : #ffb9cf,
  A400 : #ff86ac,
  A700 : #ff6d9a,
  contrast: (
    50 : #000000,
    100 : #000000,
    200 : #000000,
    300 : #000000,
    400 : #ffffff,
    500 : #ffffff,
    600 : #ffffff,
    700 : #ffffff,
    800 : #ffffff,
    900 : #ffffff,
    A100 : #000000,
    A200 : #000000,
    A400 : #000000,
    A700 : #000000,
  )
);

// #00b4e7
$my-accent: (
  50 : #e0f6fc,
  100 : #b3e9f8,
  200 : #80daf3,
  300 : #4dcbee,
  400 : #26bfeb,
  500 : #00b4e7,
  600 : #00ade4,
  700 : #00a4e0,
  800 : #009cdd,
  900 : #008cd7,
  A100 : #feffff,
  A200 : #cbebff,
  A400 : #98d7ff,
  A700 : #7fcdff,
  contrast: (
    50 : #000000,
    100 : #000000,
    200 : #000000,
    300 : #000000,
    400 : #000000,
    500 : #000000,
    600 : #ffffff,
    700 : #ffffff,
    800 : #ffffff,
    900 : #ffffff,
    A100 : #000000,
    A200 : #000000,
    A400 : #000000,
    A700 : #000000,
  )
);

$my-primary-palette: mat-palette($my-primary);
$my-accent-palette:  mat-palette($my-accent);
$my-app-theme: mat-light-theme($my-primary-palette, $my-accent-palette);
@include angular-material-theme($my-app-theme);
```

Add theme scss file to `.angular-cli.json`
```json
{
  ...
  "apps": [
    {
      ...
      "styles": [
        ...
        "theme.scss"
      ],
      ...
    }
  ]
  ...
}
```

Reference:  
https://material.angular.io/guide  
http://stackoverflow.com/questions/41440998/angular2-material-real-custom-theming  
http://mcg.mbitson.com/
