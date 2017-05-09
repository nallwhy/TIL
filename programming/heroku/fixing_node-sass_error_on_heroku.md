## Fixing `Error: ENOENT: no such file or directory, scandir '**/node_modules/node-sass/vendor'` on Heroku

>npm will only execute install scripts for direct dependencies in your package.json. This is a performance optimisation on their end which is unfortunate.
`npm rebuild node-sass` is the official solution. Deleting your `node_modules` and running `npm install` will also do the trick.

`npm rebuild node-sass` doesn't work on Heroku. So, you need to disable caches for node modules.

```bash
$ heroku config:set NODE_MODULES_CACHE=false
```

Reference:  
https://github.com/sass/node-sass/issues/1579  
https://devcenter.heroku.com/articles/nodejs-support#cache-behavior
