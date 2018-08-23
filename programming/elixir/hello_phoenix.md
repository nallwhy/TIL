## Hello, Phoenix!

### Up and Running

```
$ mix phoenix.new hello_phoenix
$ cd hello_phoenix
$ mix ecto.create
$ mix phoenix.server
```

### Adding Pages

Top-level directory structure
```
├── _build
├── config
├── deps
├── lib
├── priv
├── test
├── web
```

`web` directory structure
```
├── channels
    └── user_socket.ex
├── controllers
│   └── page_controller.ex
├── models
├── static
│   ├── assets
│   |   ├── images
|   |   |   └── phoenix.png
|   |   └── favicon.ico
|   |   └── robots.txt
│   |   ├── vendor
├── templates
│   ├── layout
│   │   └── app.html.eex
│   └── page
│       └── index.html.eex
└── views
|   ├── error_helpers.ex
|   ├── error_view.ex
|   ├── layout_view.ex
|   └── page_view.ex
├── router.ex
├── gettext.ex
├── web.ex
```

By convention, in the **development** environment, anything in the web directory will be automatically recompiled when there is a new web request.

Unlike the `web` directory, Phoenix won't recompile files inside of `lib` when there is a new web request. This is intentional! The distinction between `web` and `lib` provides a convention for the different ways that we handle state inside of our application. The `web` directory contains anything whose state lasts for the duration of a web request. The `lib` directory contains both shared modules and anything that needs to manage state outside of the duration of a web request.

