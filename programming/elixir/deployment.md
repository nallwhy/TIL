## Deployment


### Environment

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


### Local release

https://hexdocs.pm/distillery/getting-started.html#content

Add `distillery` to the dependencies.

Run `mix deps.get`.

Run `mix release.init` to setup the project with a `rel` directory.

Set `rel/config.exs`.

#### Phoenix

https://hexdocs.pm/distillery/use-with-phoenix.html#content

file: config/prod.exs
```elixir
config :phoenix_distillery, PhoenixDistillery.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [host: "localhost", port: {:system, "PORT"}], # This is critical for ensuring web-sockets properly authorize.
  cache_static_manifest: "priv/static/manifest.json",
  server: true,
  root: ".",
  version: Mix.Project.config[:version]
```

* `server` configures the endpoint to boot the Cowboy application http endpoint on start.
* `root` configures the application root for serving static files
* `version` ensures that the asset cache will be busted on versioned application upgrades (more on this later)

To build

1. (phoenix) `./node_modules/brunch/bin/brunch b -p` To build your assets in production mode.
2. (phoenix) `MIX_ENV=prod mix phoenix.digest` To compress and tag your assets for proper caching.
3. (umbrella) `mix release --env=prod` To actually generate a release for a production environment.

#### Especially Umbrella + Phoenix with dev environment

https://github.com/bitwalker/distillery/issues/25

You CANNOT run release that is built by `(MIX_ENV=dev) mix release --env=<whatever>` because of live reloading of phoenix and you can't turn off it. (Please let me know if not)

MIX_ENV -> project
--env -> distillery

##### Easy way

**Just give up to run dev release!**

##### Maybe available (not tested)

Bring environments of product to local environments.


### TODO

run `npm install` in phoenix project directory

install awscli

aws configure

AWS ECS - ECR snappy/elixir-build

aws ecr get-login --region ap-northeast-1
여기서 나오는 명령어로 다시 입력할것.

AWS Codebuild, Elastic Beanstalk, CloudFormation, CodePipeline, ...

copy `_build/prod/rel/snappy/releases/0.1.0/snappy.tar.gz`.

tar -xzf <name>.tar.gz

run `bin/<name>`

Confirm to dynamic env of elixir release.

add ecto migration
http://blog.firstiwaslike.com/elixir-deployments-with-distillery-running-ecto-migrations/

