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
