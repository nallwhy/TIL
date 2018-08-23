# Decompile and Disassemble Beam

## Decompile

When compiled with `debug_info`

```elixir
f = './_build/dev/lib/test/ebin/Elixir.Test.beam'
result = :beam_lib.chunks(f,[:abstract_code])
{:ok,{_,[{:abstract_code,{_,ac}}]}} = result
IO.puts :erl_prettypr.format(:erl_syntax.form_list(ac))
```

## Disassemble

f = ‘./_build/dev/lib/test/ebin/Elixir.Test.beam’
{:ok, beam} = File.read(f)
IO.inspect :beam_disasm.file(beam), pretty: true

Reference:  
https://medium.com/learn-elixir/disassemble-elixir-code-1bca5fe15dd1  
https://elixirphoenix.wordpress.com/2016/01/10/decompile-beam-files-to-erlang/  
https://elixirforum.com/t/releasing-with-distillery-is-safe-against-decompiling/14631/3
