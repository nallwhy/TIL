# Cancel a multiline command on IEx

```elixir
iex(1)> ["ab
...(1)> ]
...(1)> #iex:break
** (TokenMissingError) iex:1: incomplete expression
```

Reference: https://hexdocs.pm/iex/IEx.html#module-shell-history
