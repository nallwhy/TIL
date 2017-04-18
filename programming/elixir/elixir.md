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
