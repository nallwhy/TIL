## Setting global path of Yarn

[As I wrote before](./add_yarn_global_path.md), you need to add `$(yarn global bin)` to environment `$PATH` to use the cli commands of packages which is installed globally via `yarn`.

But if you update `node`, you will notice that the commands doens't work anymore. The reason is that `yarn global bin` depends on the version of `node`.

```bash
$ yarn global bin
/usr/local/Cellar/node/<node-version>/bin
```

To fix this, you need to set the `yarn global bin` manually to make it independent from the version of `node`.

For example,
```bash
# /usr/local/ is a good place to save global cli commands but it's not necessary.
$ yarn config set prefix /usr/local/
success Set "prefix" to "/usr/local/".

$ yarn global bin
/usr/local/bin
```

Then, it won't be changed when `node` is updated.

Reference: https://github.com/yarnpkg/yarn/issues/2064
