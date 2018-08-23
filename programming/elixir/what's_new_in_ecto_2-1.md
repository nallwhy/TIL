# What's new in ecto 2.1


## Ecto is not your ORM

### Object

There is no object in Elixir

### Relational Mapper

While Ecto is not a relational mapper, it contains a relational mapper as part of the many different tools it offers.

#### Issues associated with ORMs that Ecto developers may run into when using schema

##### Projects using Ecto may end-up with "God Schemas" which could conatain hundreds of fields.

 Instead of providing one single schema with fields that span multiple concerns, it is better to break the schema across multiple contexts.

 ex) `MyApp.User` -> `MyApp.Accounts.User`, `MyApp.Purchases.User`

##### Developers may rely on schemas even while sometimes the best way to retrieve data from the database is into regular data structures.

##### Developers may try to use the same schema for operations that may be quite different structurally.

Using different schemas would lead to simpler and clearer solutions.


## Schemaless Queries

```elixir
MyApp.Repo.all(Post)
# same code
MyApp.Repo.all(from p in Post, select: %Post{title: p.title, body: p.body, ...})

# Queries could only be written directly against a database table by passing the table name as a string:
MyApp.Repo.all(from p in "posts", select: {p.title, p.body})
```

Ecto 2.0 levels up the game by adding many improvements to schemaless queries, not only by improving the syntax for reading and updating data, but also by allowing all database operations to be expressed without a schema.


### `insert_all`

With `Ecto.Repo.insert_all/3`, developers can insert multiple entries at once into a repository:
```elixir
MyApp.Repo.insert_all(Post, [[title: "hello", body: "world"],
                             [title: "another", body: "post"]])
```

Although `insert_all` is just a regular Elixir function, it plays an important role in Ecto 2.0 as it allows developers to read, create, update and delete entries without a schema.

```elixir
import Ecto.Query

def running_activities(start_at, end_at)
  MyApp.Repo.all(
    from u in "users",
      join: a in "activities",
      on: a.user_id == u.id,
      where: a.start_at > type(^start_at, :naive_datetime) and
             a.end_at < type(^end_at, :naive_datetime),
      group_by: a.user_id,
      select: %{user_id: a.user_id, interval: a.end_at - a.start_at, count: count(u.id )}
  )
end

Inserts, updates and deletes can also be done without schemas via `insert_all` , `update_all` and `delete_all` respectively.

```elixir
# Insert data into posts and return its ID
[%{id: id}] =
  MyApp.Repo.insert_all "posts", [[title: "hello"]], returning: [:id]

# Use the ID to trigger updates
post = from p in "posts", where: [id: ^id]
{1, _} = MyApp.Repo.update_all post, set: [title: "new title"]

# As well as for deletes
{1, _} = MyApp.Repo.delete_all post
```

### Simpler Queries

```elixir
from p in "posts", select: %{title: p.title, body: p.body}

# simpler
from "posts", select: [:title, :body]
```

#### `update` construct

- :set - sets the given column to the given values
- :inc - increments the given column by the given value
- :push - pushes (appends) the given value to the end of an array column
- :pull - pulls (removes) the given value from an array column

```elixir
def update_title(post, new_title) do
  query = from "posts", where: [id: ^post.id], update: [set: [title: ^new_title]]
  MyApp.Repo.update_all(query)
end

def increment_page_views(post) do
  query = from "posts", where: [id: ^post.id], update: [inc: [page_views: 1]]
  MyApp.Repo.update_all(query)
end
```


## Schemas and Changesets

### Schemas are mappers

> An Ecto schema is used to map any data source into an Elixir struct.

Imagine you are working with a client that wants the "Sign Up" form to contain the fields "First name", "Last name" along side "E-mail" and other information.

Not everyone has a first and last name. Although your client is decided on presenting both fields, they are a UI concern, and you don't want the UI to dictate the shape of your data. And you know it would be useful to break the "Sign Up" information across two tables, the "accounts" and "profiles" tables.

```elixir
# Bad
defmodule Profile do
  use Ecto.Schema

  schema "profiles" do
    field :name
    field :first_name, :string, virtual: true
    field :last_name, :string, virtual: true
    ...
  end
end

# Good
# We used `embedded_schema` because it is not our intent to persist it anywhere.

defmodule Registration do
  use Ecto.Schema

  embedded_schema do
    field :first_name
    field :last_name
    field :email
  end
end

fields = [:first_name, :last_name, :email]
changeset =
  %Registration{}
  |> Ecto.Changeset.cast(params["sign_up"], fields)
  |> validate_required(...)
  |> validate_length(...)

if changeset.valid? do
  # Get the modified registration struct out of the changeset
  registration = Ecto.Changeset.apply_changes(changeset)

  MyApp.Repo.transaction fn ->
    MyApp.Repo.insert_all "accounts", [Registration.to_account(registration)]
    MyApp.Repo.insert_all "profiles", [Registration.to_profile(registration)]
  end

  {:ok, registration}
else
  # Annotate the action we tried to perform so the UI shows errors
  changeset = %{changeset | action: :registration}
  {:error, changeset}
end

def to_account(registration) do
  Map.take(registration, [:email])
end
def to_profile(%{first_name: first, last_name: last}) do
  %{name: "#{first} #{last}"}
end
```


## Dynamic Queries

```elixir
import Ecto.Query

# keywords syntax
from p in Post,
  where: [author: "José", category: "Elixir"],
  where: p.published_at > ^minimum_date,
  order_by: [desc: :published_at]

# pipe-based
Post
|> where(author: "José", category: "Elixir")
|> where([p], p.published_at > ^minimum_date)
|> order_by(desc: :published_at)
```

The data structure can be specified at compile-time, as above, and also dynamically at runtime, shown below:
```elixir
where = [author: "José", category: "Elixir"]
order_by = [desc: :published_at]
Post
|> where(^where)
|> where([p], p.published_at > ^minimum_date)
|> order_by(^order_by)
```

Since where converts a key-value to a `key == value` comparison, order- based comparisons such as `p.published_at > ^minimum_date` still need to be written as part of the query as before.

Luckily, Ecto 2.1 solves this issue.

### Dynamic Macro

```elixir
def filter(params) do
  Post
  |> order_by(^filter_order_by(params["order_by"]))
  |> where(^filter_where(params))
  |> where(^filter_published_at(params["published_at"]))
end

def filter_order_by("published_at_desc"), do: [desc: :published_at]
def filter_order_by("published_at"), do: [asc: :published_at]
def filter_order_by(_), do: []

def filter_where(params) do
  for key <- [:author, :category],
    value = params[Atom.to_string(key)],
    do: {key, value}
end

def filter_published_at(date) when is_binary(date), do: dynamic([p], p.published_at > ^date)
def filter_published_at(_date), do: true

# Testing also becomes simpler as we can test each function in isolation, even when using dynamic queries.
test "filter published at based on the given date" do
  assert inspect(filter_published_at("2010-04-17")) == "dynamic([p], p.published_at > ^\"2010-04-17\")"
  assert inspect(filter_published_at(nil)) == "true"
end
```


## Multi Tenancy with Query Prefixes

skip


## Aggregates and Subqueries

```elixir
MyApp.Repo.aggregate(MyApp.Post, :avg, :visits)

# translated to
MyApp.Repo.one(from p in MyApp.Post, select: avg(p.visits))
```

Imagine that instead of calculating the average of all posts, you want the average of only the top 10. Your first try may be:
```elixir
MyApp.Repo.one(from p in MyApp.Post,
                order_by: [desc: :visits],
                limit: 10,
                select: avg(p.visits))
```

The option `limit: 10` has no effect here since it is limiting the aggregated result and queries with aggregates return only a single row anyway.
```elixir
# Good
query = from MyApp.Post, order_by: [desc: :visits], limit: 10
MyApp.Repo.aggregate(query, :avg, :visits)

# translated to
MyApp.Repo.one(from q in subquery(query), select: avg(q.visits))
```

### Subqueries

Imagine you manage a library and there is a table that logs every time the library lends a book.

```elixir
defmodule Library.Lending do
  use Ecto.Schema

  schema "lendings" do
    belongs_to :book, MyApp.Book       # defines book_id
    belongs_to :visitor, MyApp.Visitor # defines visitor_id
  end
end

last_lendings =
  from l in MyApp.Lending,
    group_by: l.book_id,
    select: %{book_id: l.book_id, last_lending_id: max(l.id)}

from l in Lending,
  join: last in subquery(last_lendings),
  on: last.last_lending_id == l.id,
  join: b in assoc(l, :book),
  join: v in assoc(l, :visitor),
  select: {b.name, v.name}
```


## Improved Associations and Factories

```elxiir
Repo.insert! %Post{
  title: "hello world",
  comments: [
    %Comment{body: "excellent article"},
    %Comment{body: "I learned something new"}
  ]
}

Repo.insert! %Comment{
  body: "excellent article",
  post: %Post{title: "hello world"}
}
```

### Test Factories

```elixir
defmodule MyApp.Factory do
  alias MyApp.Repo

  # Factories
  def build(:post) do
    %MyApp.Post{title: "hello world"}
  end

  def build(:comment) do
    %MyApp.Comment{body: "good post"}
  end

  def build(:post_with_comments) do
    %MyApp.Post{
      title: "hello with comments",
      comments: [
        build(:comment, body: "first"),
        build(:comment, body: "second")
      ]
    }
  end

  def build(:user) do
    %MyApp.User{
      email: "hello#{System.unique_integer()}",
      username: "hello#{System.unique_integer()}"
    }
  end

  # Convenience API
  def build(factory_name, attributes) do
    factory_name |> build() |> struct(attributes)
  end

  def insert!(factory_name, attributes \\ []) do
    Repo.insert! build(factory_name, attributes)
  end
end
```

To use test factory, open up your "mix.exs" and make sure the "test/support/factory.ex" file is compiled:
```elixir
def project do
  [
    ...,
    elixirc_paths: elixirc_paths(Mix.env),
    ...
  ]
end

defp elixirc_paths(:test), do: ["lib", "test/support"]
defp elixirc_paths(_), do: ["lib"]
```


## Many to Many and Casting

Besides `belong_to` , `has_many` , `has_one` and `:through` associations, Ecto 2.0 also includes `many_to_many` which is better than `has_many :through`.

```elixir
defmodule MyApp.TodoList do
  use Ecto.Schema

  schema "todo_lists" do
    field :title
    has_many :todo_items, MyApp.TodoItem

    timestamps()
  end
end

defmodule MyApp.TodoItem do
  use Ecto.Schema

  schema "todo_items" do
    field :description

    timestamps()
  end
end
```

```eex
<%= form_for @todo_list_changeset, todo_list_path(@conn, :create), fn f -> %> <%= text_input f, :title %>
<%= inputs_for f, :todo_items, fn i -> %>
...
<% end %>
<% end %>
```

```elixir
%{"todo_list" => %{
  "title" => "shipping list",
  "todo_items" => %{
    0 => %{"description" => "bread"},
    1 => %{"description" => "eggs"},
  }
}}
```

```elixir
# In MyApp.TodoList
def changeset(struct, params \\ %{}) do
  struct
  |> Ecto.Changeset.cast(params, [:title])
  |> Ecto.Changeset.cast_assoc(:todo_items, required: true)
end

# And then in MyApp.TodoItem
def changeset(struct, params \\ %{}) do
  struct
  |> Ecto.Changeset.cast(params, [:description])
end
```

By calling `Ecto.Changeset.cast_assoc/3` , Ecto will look for a "todo_items" key inside the parameters given on cast, and compare those parameters with the items stored in the todo list struct. Ecto will automatically generate instructions to insert, update or delete todo items such that:

- if a todo item sent as parameter has an ID and it matches an existing associated todo item, we consider that todo item should be updated
- if a todo item sent as parameter does not have an ID (nor a matching ID), we consider that todo item should be inserted
- if a todo item is currenetly associated but its ID was not sent as parameter, we consider the todo item is being replaced and we act according to the `:on_replace` callback. By default `:on_replace` will raise so you choose a behaviour between replacing, deleting, ignoring or nilifying the association

### Polymorphic todo items

The trouble is that `:through` associations are read-only since Ecto does not have enough information to fill in the intermediate schema. This means that, if we still want to use `cast_assoc` to insert a todo list with many todo items directly from the UI, we cannot use the `:through` association and instead must go step by step.

Differently from `has_many :through` , `many_to_many` associations are also writeable.

```elixir
create table(:todo_lists)  do
  add :title
  timestamps()
end

create table(:projects)  do
  add :name
  timestamps()
end

create table(:todo_items)  do
  add :description
  timestamps()
end

create table(:todo_lists_items, primary_key: false) do
  add :todo_item_id, references(:todo_items)
  add :todo_list_id, references(:todo_lists)
  # timestamps()
end

create table(:projects_items, primary_key: false) do
  add :todo_item_id, references(:todo_items)
  add :project_id, references(:projects)
  # timestamps()
end
```

```elixir
defmodule MyApp.TodoList do
  use Ecto.Schema

  schema "todo_lists" do
    field :title
    many_to_many :todo_items, MyApp.TodoItem, join_through: MyApp.TodoListItem

    timestamps()
  end
end

defmodule MyApp.TodoListItem do
  use Ecto.Schema

  schema "todo_list_items" do
    belongs_to :todo_list, MyApp.TodoList
    belongs_to :todo_item, MyApp.TodoItem

    timestamps()
  end
end

defmodule MyApp.TodoItem do
  use Ecto.Schema

  schema "todo_items" do
    field :description

    timestamps()
  end
end
```

```elixir
# In MyApp.TodoList
def changeset(struct, params \\ %{}) do
  struct
  |> Ecto.Changeset.cast(params, [:title])
  |> Ecto.Changeset.cast_assoc(:todo_items, required: true)
end

# And then in MyApp.TodoItem
def changeset(struct, params \\ %{}) do
  struct
  |> Ecto.Changeset.cast(params, [:description])
end
```


## Many to Many and Upserts

### `put_assoc` vs `cast_assoc`

