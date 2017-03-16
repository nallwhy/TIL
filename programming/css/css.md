### 2017-03-16


#### How to give line-break from css, without using `<br />`?

```css
white-space: pre | pre-wrap | pre-line // But 'pre-line' collapse whitespaces
```

Translation:
https://developer.mozilla.org/ko/docs/Web/CSS/white-space


#### Difference between `inline` and `inline-block`

##### inline

1. Allow other elements to sit to their left and right.
2. Respect left & right margins and padding, but **not** top & bottom
3. **Cannot** have a width and height set

See also https://hacks.mozilla.org/2015/03/understanding-inline-box-model/

##### inline-block

1. Allow other elements to sit to thier left and right
2. Respect margins and padding for all side
3. Respect height and width

Reference: http://stackoverflow.com/questions/9189810/css-display-inline-vs-inline-block


#### object-fit

It's very simillar to `background-size` property, but it's for `relaced elements`(<img>, <video>, <object>, ...).

cf. `background-position` - `object-position`

Reference: https://developer.mozilla.org/ko/docs/Web/CSS/object-fit
