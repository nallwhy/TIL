# How to put session in tests

```elixir
import Plug.Test

test "DELETE /sign_out clears the session", %{conn: conn} do
  conn = conn
    |> init_test_session(foo: "bar")
    |> delete(session_path(conn, :delete))

  refute get_session(conn, :foo)
end
```

Reference: https://github.com/phoenixframework/phoenix/issues/861#issuecomment-294711607
