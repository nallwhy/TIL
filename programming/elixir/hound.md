## Hound

### Adding Hound to dependency

### Set config of Hound

`config/config.exs`
```elixir
config :hound, driver: "selenium"
```

### Run!

```elixir
defmodule MyModule do
  use Hound.Helpers

  def func(url) do
    # It's not necessary.
    # Application.ensure_all_started(:hound)

    Hound.start_session
    navigate_to url
    source = page_source()
    Hound.end_session
  end
end
```

https://github.com/HashNuke/hound
https://github.com/HashNuke/hound/blob/master/notes/configuring-hound.md
https://github.com/HashNuke/hound/wiki/Starting-a-webdriver-server
https://github.com/HashNuke/hound/blob/master/notes/simple-browser-automation.md
