# Tools

## `mix hex.outdated`

Shows outdated Hex deps for the current project

## excoveralls

https://github.com/parroty/excoveralls

## `mix xref graph`

Show the dependency tree for the application

```bash
$ mix xref graph --format dot
$ dot -Grankdir=LR -Epenwidth=2 -Ecolor=#a0a0a0 \
          -Tpng xref_graph.dot -o xref_graph.png
```
