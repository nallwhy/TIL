# Validate not blank of Ecto changeset

`cast/4` 는 처음부터 `nil`, `""` 를 걸러낸다.

`validate_required/3` 는 작업의 결과를 체크한다. 그래서 changeset 이 다른 field 를 건드리더라도 해당 field 의 결과가 `nil`, whitespace 가 아니어야한다.

특정 field 의 변경이 들어왔을 때 그 변경이 blank 가 아니도록 하기 위해서는 아래와 같이 하면 된다. (편의를 위해 Blankable 사용)

```elixir
import Ecto.Changeset

def validate_not_blank(changeset, fields) when is_list(fields) do
  Enum.reduce(fields, changeset, fn field, changeset ->
    validate_not_blank(changeset, field)
  end)
end

def validate_not_blank(changeset, field) do
  with change <- get_change(changeset, field, :not_exist),
        true <- change != :not_exist,
        true <- Blankable.blank?(change) do
    add_error(changeset, field, "can't be blank")
  else
    _ -> changeset
  end
end
```

Reference:  
https://groups.google.com/forum/#!topic/elixir-ecto/KXlNyNk4IRo  
https://hexdocs.pm/ecto/2.2.9/Ecto.Changeset.html#cast/4  
https://hexdocs.pm/ecto/2.2.9/Ecto.Changeset.html#validate_required/3



