## Deployment

>"Build environment must match deployment environment."  
>(https://www.youtube.com/watch?time_continue=1465&v=nZ-U8ZszmeI)

To create Erlang/OTP release from Mix project, you can use [Distillery](https://github.com/bitwalker/distillery).

As it is really documented well, you can generate releases easily by `mix release`.

I've tried to

1. build a release of elixir app on my Mac
2. copy it to AWS EC2 ubuntu machine
3. run it

But it fails.

You should build your release on the `exactly same environment` as deployment environment.

So you need a build server or can use docker to deployment.

(Doing)