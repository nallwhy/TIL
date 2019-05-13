# Add params to function with macro

```elixir
defmacro deflogic(call, expr) do
  # def test(a, b), do: a + b
  # call: {:test, [line: 16], [{:a, [line: 16], nil}, {:b, [line: 16], nil}]}
  # expr: [do: {:+, [line: 16], [{:a, [line: 16], nil}, {:b, [line: 16], nil}]}]

  {name, context, args} = call
  new_call = {name, context, [{:user_id, context, nil}, {:from, context, nil} | args]}

  quote do
    Kernel.def(unquote(new_call), unquote(expr))
  end
end
```
