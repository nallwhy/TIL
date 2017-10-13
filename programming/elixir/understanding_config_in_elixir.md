## Understanding Config in Elixir

### How `config` works in Elixir

Under the hood, config is actually just a key/value list. They are stored as a list of lists, one list for each key you define. For each key, you have another key/value list, which is the actual variables. An example will make this clear.

```elixir
# config.exs
config :my_app
  name: "MyApp"

config :my_app, MyApp.Repo
  url: "postgres://blabla"


iex) Application.get_all_env(:my_app)
[
  {:name, ["MyApp"]},
  {MyApp.Repo, [url: "postgres://blabla"]}
]

iex) Application.get_env(:my_app, :name, "Default")
"MyApp"

iex) Application.get_env(:my_app, MyApp.Repo)[:url]
"postgres://blabla"
```

### config in Elixir release


sys.config. Lets take a look.

cat rel/my_app/releases/0.1.0/sys.config 

[{sasl,[{errlog_type,error}]},
 {my_app,[{twitter_url,<<"https://api.mock.com">>}]}].


 This doesn’t have to be a problem though as you can set Application configuration at runtime via Application.put_env/3. Using this you could create a function that reads the OS environmental variable and adds it to the application’s configuration.

def os_env_config_to_app_env_config do
  twitter_url = System.get_env("TWITTER_URL")
  Application.put_env(:my_app, :twitter_url, twitter_url)
  :ok
end
 




With Distillery releases, you can set REPLACE_OS_VARS=true in the OS environment, which will cause any variable contents from eg. config/*.exs of the form "${TWITTER_URL}" to be replaced in the runtime configuration when starting your release.

I'm using this in a special version of config/prod.exs that's only used during release builds, so that we can later use the same release for both the staging and prod environments.
http://disq.us/p/1ff47hd

Reference:  
http://sheldonkreger.com/understanding-config-in-elixir.html  
https://www.erlang-solutions.com/blog/from-elixir-mix-configuration-to-release-configuration-alchemy-101-part-2.html