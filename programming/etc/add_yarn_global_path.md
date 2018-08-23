## Add Yarn global path

When you install packages globally via `npm`, it's natural to use the cli command of the packages, like

```bash
$ npm install -g @angular/cli
$ ng help
```

But when you add packages via `yarn`, it might not work.

```bash
$ yarn global add @angular/cli
$ ng help
~ Unknown command 'ng'
```

To use cli commands of global packages, you should add `yarn global bin` path to the `PATH` environment variable.

```bash
# ~/.bash_profile or whatever you use
export PATH=$(yarn global bin):$PATH
```

```bash
# ~/.config/fish/config.fish
set -x PATH $PATH (yarn global bin)
```

Reference: https://github.com/yarnpkg/yarn/issues/1321
