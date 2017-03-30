## Converting a callback to a promise

https://medium.com/@bluepnume/learn-about-promises-before-you-start-using-async-await-eb148164a9c8

```javascript
function callbackToPromise(method, ...args) {
    return new Promise(function(resolve, reject) {
        return method(...args, function(err, result) {
            return err ? reject(err) : resolve(result);
        });
    });
}
```
