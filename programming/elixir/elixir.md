### 2017-11-20

#### Encoding Ecto Validation Errors in Phoenix 1.3

https://www.mitchellhanberg.com/post/2017/10/23/encoding-ecto-validation-errors-in-phoenix/


### 2017-11-12

#### Maximizing HTTP/2 performance with GenStage

http://tech.footballaddicts.com/blog/maximizing-http2-performance-with-genstage


#### Monitoring GenServers with PryIn

https://blog.pryin.io/monitoring-gen-servers-with-pryin/


### 2017-11-01

#### Guaxinim

Literate programming for Elixir

https://github.com/tmbb/guaxinim


### 2017-10-24

#### Ecto Query Examples

https://elixirnation.io/references/ecto-query-examples


### 2017-10-15

#### Embrace The Database With Ecto

https://speakerdeck.com/jbranchaud/embrace-the-database-with-ecto


#### Elixir tips

https://github.com/blackode/elixir-tips


#### Alias your Phoenix mix commands for some nice developer UX

https://sergiotapia.me/alias-your-phoenix-mix-commands-for-some-nice-developer-ux-4a02b2bf3474


#### Dialyxir

Mix tasks to simplify use of Dialyzer in Elixir projects

https://github.com/jeremyjh/dialyxir


#### How Discord handles push request bursts of over a million per minute with Elixir’s GenStage

https://blog.discordapp.com/how-discord-handles-push-request-bursts-of-over-a-million-per-minute-with-elixirs-genstage-8f899f0221b4


### 2017-10-11

#### Today I Learned in Elixir

https://github.com/hashrocket/tilex


### 2017-09-12

#### Flowex

https://medium.com/@anton.mishchuk/flow-based-rest-api-with-flowex-and-plug-323d6920f166  
https://github.com/antonmi/flowex


### 2017-08-16

#### StreamData

StreamData is an Elixir library for data generation and property testing.

https://github.com/whatyouhide/stream_data

#### PryIn

Monitoring Phoniex app

https://pryin.io


### 2017-08-09

#### Lessons From Using Phoenix 1.3

https://robots.thoughtbot.com/lessons-from-using-phoenix-1-3

#### Making Sense of Ecto 2 SQL.Sandbox and Connection Ownership Modes

https://medium.com/@qertoip/making-sense-of-ecto-2-sql-sandbox-and-connection-ownership-modes-b45c5337c6b7


### 2017-08-07

#### Engineering at Teachers Pay Teachers

http://engineering.teacherspayteachers.com/2017/08/02/reducing-elixir-backend-time-from-120ms-to-20ms-with-parallelization.html


### 2017-08-04

#### State of the art in deploying Elixir / Phoenix applications

https://hackernoon.com/state-of-the-art-in-deploying-elixir-phoenix-applications-fe72a4563cd8


### 2017-07-19

#### How Discord Scaled Elixir to 5,000,000 Concurrent Users

https://blog.discordapp.com/scaling-elixir-f9b8e1e7c29b


### 2017-07-09

#### Security Scanning Your Phoenix App (Sobelow)

https://brainlid.org/elixir/2017/06/14/security-scanning-phoenix.html  
https://github.com/nccgroup/sobelow

#### Lonestar ElixirConf 2017- KEYNOTE: Phoenix 1.3 by Chris McCord

https://www.youtube.com/watch?v=tMO28ar0lW8


### 2017-07-07

#### Never compare dates in Elixir using "<" or ">"

http://blog.leif.io/never-use-to-compare-dates/

It's just Struct comparing.

Use [NaiveDateTime.compare()](https://hexdocs.pm/elixir/NaiveDateTime.html#compare/2).

#### Elmchemy

https://github.com/wende/elmchemy  
https://hackernoon.com/elmchemy-write-type-safe-elixir-code-with-elms-syntax-part-1-introduction-8968b76d721d

Using elm syntax to write type-safe elixir code.


### 2017-07-04

#### Cortex

https://github.com/urbint/cortex

Cortex is the intelligent coding assistant for Elixir.

#### The Missing Guide To Elixir

https://circleci.com/blog/the-missing-guide-to-elixir

CircleCI + Elixir


### 2017-06-05

#### Optimizing Your Elixir and Phoenix projects with ETS

https://dockyard.com/blog/2017/05/19/optimizing-elixir-and-phoenix-with-ets


### 2017-06-02

#### Elixir and Unicode, Part 1: Unicode and UTF-8 Explained

https://www.bignerdranch.com/blog/unicode-and-utf-8-explained/


### 2017-05-17

#### Thinking in Ecto - schemas and changesets

http://cultofmetatron.io/2017/04/22/thinking-in-ecto---schemas-and-changesets

#### Using GenStage for a Batching Pipeline

https://alexgaribay.com/2017/04/25/using-genstage-for-a-batching-pipeline


### 2017-05-09

#### 10 Killer Elixir Tips

https://medium.com/blackode/10-killer-elixir-tips-2a9be1bec9be

##### Multiple [ OR ]

```elixir
# Regular Approach
find = fn(x) when x>10 or x<5 or x==7 -> x end

# Our Hack
hell = fn(x) when true in [x>10,x<5,x==7] -> x end
```

##### Thinking `||` as `Kernel.||`

```elixir
# Bad
result = :input
|> do_something
|> do_another_thing

result = (result || :default_output)
|> do_something_else

# Good
result = :input
|> do_something
|> do_another_thing
|> Kernel.||(:default_output)  #<-- This line
|> do_something_else
```

##### Recompiling Project

```
$ iex -S mix
iex> recompile() 
```

#### Scout

https://scoutapp.com/

Performance insights for Ruby & Elixir apps.

#### FunWithFlags

https://github.com/tompave/fun_with_flags

#### Que

https://github.com/sheharyarn/que

#### The building blocks of a poker application

https://medium.com/carwow-product-engineering/the-building-blocks-of-a-poker-application-6042357a58c1

#### Ravenx

https://medium.com/acutario/sending-notifications-in-elixir-with-ravenx-1f2502a1f272  
https://github.com/acutario/ravenx

Notification dispatch library for Elixir applications.

#### How to use Elixir’s GenStage.Flow for image resizing

https://medium.com/carwow-product-engineering/how-to-use-elixirs-genstage-flow-for-image-resizing-ec3f7343f641

#### Phoenix Presence for social networks

https://medium.com/@alvinlindstam/phoenix-presence-for-social-networks-5fb67143f0ad

#### Weave

https://www.rawkode.io/2017/04/introducing-weave-for-elixir/  
https://github.com/GT8Online/weave

A library that makes it possible to load configuration, especially secrets, from disk (Ala Docker Swarm / Kubernetes) on start-up.

#### Trans

https://github.com/belaustegui/trans

A library that manage and query translations embedded into schemas and removes the necessity of maintaing extra tables only for translation storage.

#### PHOENIX 1.3 AND GRAPHQL WITH ABSINTHE

https://seanclayton.me/post/phoenix-1-3-and-graphql-with-absinthe

#### Flub

https://github.com/meyercm/flub

Flub does Pub. Flub does Sub. Flub does PubSub, bub.

#### Phoenix and Elm, a real use case

http://codeloveandboards.com/blog/2017/02/02/phoenix-and-elm-a-real-use-case-pt-1/


### 2017-05-02

#### Elixir Project Generator

https://pragdave.me/blog/2017/04/18/elixir-project-generator.html


### 2017-04-25

#### Length vs Amount

https://medium.com/@kana_sama/length-vs-amount-37a1c431141a

`Kernel.length()` is much faster than `Enum.count()`, but it's only for lists while `Enum.count()` is for all enumerations.

#### Replace Callbacks with Ecto.Multi

http://blog.danielberkompas.com/2016/09/27/ecto-multi-services.html

#### Simple Scheduler exmpale

https://gist.github.com/danielberkompas/7212ef0ba261e4a19a0b86ec1e109282


### 2017-04-21

#### Small Data with Elixir

http://blog.plataformatec.com.br/2017/03/small-data-with-elixir

#### Flow

https://github.com/elixir-lang/flow


### 2017-04-18

#### Logging slow Ecto queries: adventures in metaprogramming

https://hackernoon.com/logging-slow-ecto-queries-adventures-in-metaprogramming-110f3472be33

#### Exnumerator

https://github.com/KamilLelonek/exnumerator


### 2017-04-12

#### Floating Point and currency

http://blog.plataformatec.com.br/2014/09/floating-point-and-currency/

Do not use `floating point` for currency. Use `integer` or something for `decimal number`.

#### Elixir Module Attributes - Alchemy 101 Part 1

https://www.erlang-solutions.com/blog/elixir-module-attributes-alchemy-101-part-1.html

Module attributes are evaluated at **compile time**, not runtime.

#### From Elixir Mix configuration to release configuration - Alchemy 101 Part 2

https://www.erlang-solutions.com/blog/from-elixir-mix-configuration-to-release-configuration-alchemy-101-part-2.html

When creating a release, `config.exs` is evaluated and the result is written to `rel/$app/releases/$version/sys.config` which is picked up by your application on startup.

#### Fault Tolerance doesn't come out of the box - Alchemy 101: Part 3

https://www.erlang-solutions.com/blog/fault-tolerance-doesn-t-come-out-of-the-box-alchemy-101-part-3.html

#### Setting Up Phoenix/Elixir With Nginx and LetsEncrypt

https://medium.com/@a4word/setting-up-phoenix-elixir-with-nginx-and-letsencrypt-ada9398a9b2c


### 2017-04-07

#### Credo

https://github.com/rrrene/credo

Credo is a static code analysis tool for the Elixir language with a focus on teaching and code consistency.


### 2017-03-29

#### Distributed Elixir on… Heroku?

https://medium.com/@karmajunkie/distributed-elixir-on-heroku-59b691d9868e

#### Slap

https://github.com/derniercri/slap

A simple load testing tool.


### 2017-03-28

#### Updating individual Elixir libraries using mix

http://thisischichi.me/2017/03/22/elixirphoenix-mix-tip-1-mix-deps-unlock/

Get outdated libraries
```
mix hex.outdated
```

Update libraries
```
mix deps.unlock <library>
mix deps.get
```

#### Understanding Elixir Pattern Matching

http://www.littlealchemist.io/2017-03-15-understading-elixir-pattern-matching/

`=` is not **assignment**, but **pattern matching** in Elixir.

Elixir will try to make the expressions on both sides be equal.

Elixir will only bind variables on the **left side** though.

```elixir
[foo, bar, ho] = ["b", "a", "r"]
# foo => "b", bar => "a", ho => "r"

["b", "a", "r"] = [foo, bar, ho]
# error!

%{"key" => my_value} = %{"key" => "foo"}
# my_value => "foo"
```

##### Pin operator `^`

You can match using value stored within the variable, not as a normal variable using `^`

```elixir
foo = 3
[^foo, bar] = [3, "awesome"]
# bar => "awesome"

foo = 3
[^foo, bar] = [5, "not good"]
# error!
```


### 2017-03-22

#### Avoiding race conditions in GenServer

https://bhelx.simst.im/articles/avoiding-race-conditions-in-genserver-state/

"GenServer makes this easy for us because the process model ensures that everything that happens in the callback is atomic!"

#### Phoenix 1.3 is pure love for API development

http://swanros.com/phoenix-1-3-is-pure-love-for-api-development/

#### Clustering libraries

https://github.com/bitwalker/libcluster
https://github.com/mrluc/peerage

#### ConCache

https://github.com/sasa1977/con_cache

ETS(Erlang Term Storage) based key/value storage.
You can store all of the Elixir types. (cf. the limited types Redis supports)

#### Bourne

https://github.com/mtwilliams/bourne

Ecto streaming

#### ExMachina

https://github.com/thoughtbot/ex_machina

Create test data like factory_girl

#### Guardian

https://github.com/ueberauth/guardian

Elixir authentication framework


### 2017-03-20

#### Focus

https://github.com/tpoulsen/focus

Nested map, sturcture 의 getter, setter 를 만들기 쉽게해줌.

#### Scriverner.Ecto

https://github.com/drewolson/scrivener_ecto

Ecto pagination
