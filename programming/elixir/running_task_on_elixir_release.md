## Running tasks on Elixir release

To deploy Elixir application, it's common to create **Erlang/OTP release** from the app. Erlang/OTP release can be run anywhere with **NO** dependencies.

[Distillery](https://github.com/bitwalker/distillery) is a best way to do that. But you can't run **mix-tasks** on releases as they don't have `Mix`.

It's very common to run migrations after release. Here's the solution.


### Create a module that contains your tasks

```elixir
defmodule MyApp.ReleaseTasks do

  # My app name
  @myapp :myapp

  # Apps that is necessary for executing tasks
  @dep_apps [:postgrex, :ecto, :ssl_verify_fun, :httpoison]

  # Repo module
  @repo MyApp.Repo

  def create do
    load_apps()

    IO.puts "Creating DB table..."
    case MyApp.Repo.__adapter__.storage_up(MyApp.Repo.config) do
      :ok -> IO.puts "Success!"
      {:error, term} -> IO.puts term
    end

    :init.stop()
  end

  def drop do
    load_apps()

    IO.puts "Drop DB table..."
    case MyApp.Repo.__adapter__.storage_down(MyApp.Repo.config) do
      :ok -> IO.puts "Success!"
      {:error, term} -> IO.puts term
    end

    :init.stop()
  end

  def migrate do
    load_apps()
    start_repo()

    run_migrations_for(@myapp, @repo)

    IO.puts "Success!"
    :init.stop()
  end

  def seed do
    load_apps()
    start_repo()

    run_migrations_for(@myapp, @repo)

    seed_script = seed_path(@myapp)
    if File.exists?(seed_script) do
      IO.puts "Running seed script.."
      Code.eval_file(seed_script)
      IO.puts "Success!"
    else
      IO.puts "No seed script!"
    end

    :init.stop()
  end

  defp load_apps() do
    # Load the environment of the app, but don't start it
    :ok = Application.load(@myapp)

    # Start apps necessary for executing tasks
    Enum.each(@dep_apps, &Application.ensure_all_started/1)
  end

  defp start_repo() do
    # Start the Repo(s) for myapp
    MyApp.Repo.start_link(pool_size: 1)
  end

  defp run_migrations_for(app, repo) do
    # Run migrations
    Ecto.Migrator.run(repo, migrations_path(app), :up, all: true)
  end

  defp priv_dir(app), do: "#{:code.priv_dir(app)}"

  defp migrations_path(app), do: Path.join([priv_dir(app), "repo", "migrations"])

  defp seed_path(app), do: Path.join([priv_dir(app), "repo", "seeds.exs"])

end
```

### Add custom commands to the release

For example,

`rel/commands/migrate.sh`:
```bash
#!/bin/sh

bin/myapp command Elixir.MyApp.ReleaseTasks migrate
```

`rel/config.exs`:
```elixir
release :myapp do
  ...
  set commands: [
    "migrate": "rel/commands/migrate.sh"
  ]
end
```

Now, you can run migrations with `bin/myapp migrate`.

Reference:  
https://hexdocs.pm/distillery/running-migrations.html  
http://blog.firstiwaslike.com/elixir-deployments-with-distillery-running-ecto-migrations/  
http://stackoverflow.com/questions/43270981/do-ecto-migration-from-a-release-of-an-elixir-app
